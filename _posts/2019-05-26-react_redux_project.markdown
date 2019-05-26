---
layout: post
title:      "React/Redux Project"
date:       2019-05-26 21:43:57 +0000
permalink:  react_redux_project
---


I finished my React/Redux project the other day, which pretty much brings to an end the full stack web development curriculum. I really tried to showcase as much as I could everything that I learned. For my project I decided to create an appointment scheduler/blog for a fitness website. It's something that I had made in the past before joining the FlatIron school, so I thought I would use it as a means to see how much knowledge I have gained since then. The project required use of ES6, 2 component containers, 5 stateless components, 3 routes, use of React-Router, Redux-thunk middleware, Rails API backend to persist data, Async JS with Promises and a good understanding of data flow.  On top of the required elements for the project I added a login capability (very rudimentary, mostly just to connect to the rails API), css, drawings, and p5.js capability. I felt pretty satisfied and confident with what I made, but a couple of things really required some research in order to tighten up some holes. Async JS with Promises, and data flow of React/Redux.

## React/Redux data flow
Data flow in Redux is unidirectional, meaning that all data follows the same lifecycle pattern making the application more predictable, easier to understand, and normalizaed (don't end up with multiple, independent copies of the same data that are unaware of one another)

React/Redux makes use of actions, reducers and the store in order to update the state according to those actions.

The store's main responsibilities include:

* Holds application state
* Allows access tostate via getState()
* Allows state to be updated via dispatch(action)
* Registers listeners via subscribe(listener)
* Handles unregistering of listeners via the function returned by subscribe(listener)

The data lifecyle in any Redux app follows these 4 steps:

**1. You call store.dispatch(action)**

=> In my React project the actions available are add/deleting BlogPost or Reservation. An action is just a plain object describing what happend. For example:

```
{type: 'ADD_RESERVATION', reservation};
{type: 'DELETE_RESERVATION', reservation};
```

I can call store.dispatch(action) from anywhere in my app, such as in my Admin/Training/BlogContainer. The actions in my app are located in the actions folder within /src, which is where my React code is located.

**2. The Redux store calls the reducer function you gave it**

After you call store.dispatch(action), the store will pass two arguments to the reducer: the current state and the action. For example in my app, If I was 

```
// List of all reservations
let previousState = {
  reservations: []
}

// The action being performed (adding a reservation)
let action = {
  type: 'ADD_RESERVATION',
  payload: 'this is a reservation object'
}

// Your reducer returns the next application state
let nextState = reseravationApp(previousState, action)
```

The reducer is a pure function, such that it only computes the next state, making it predictable.

**3. The root reducer may combine the output of multiple reducers into a single state tree**

Redux ships with a combineReducers() helper function, useful for "splitting' the root reducer into separate functions that each manage one branch of the state tree. In my app it is located in index.js 

```
// combines and uses reducers
import { combineReducers } from 'redux';

const rootReducer = combineReducers({
  blogPosts: blogReducer,
  reservations: reservationReducer
})
```

Even though combineReducers()is very handy, it is not necessary to use.

**4. The Redux store saves the complete state tree returned by the root reducer**

This new tree is now the next state of the app. State can be retrieved using store.getState() or like in my app I used mapStateToProps.

## Async React with Promises

In my react app it fetches data from the Rails API backend where data is persisted. The asynchronous calls to the API require the use of promises to properly handle the asynchronouse computations. A Promise object is simply a wrapper around a value that may or may not be known when teh object is instantiated and provides a method for handling the value after is is known(resolved) or is unavailable for a failure reason(rejected). 

As an example without promises let's look at a code where we print out the current time in the JavaScript console:

```
var currentTime = new Date();
console.log('The current time is: ' + currentTime);
```

Suppose we're making a Happy New Years clock, and want it to be able to synchronize the user's browser with everyone elses using a single time value for everyone so no-one misses the ball dropping ceremony.

Below we have a method that handles getting the current time for the clock called getCurrentTime() that fetches the current time from a remote server. We'll represent this now with a setTimeout() that returns the time.

```
function getCurrentTime() {
  // Get the current 'global' time from an API
  return setTimeout(function() {
    return new Date();
  }, 2000);
}
var currentTime = getCurrentTime()
console.log('The current time is: ' + currentTime);
```

Our console.log() log value will return the timeout handler id, which is definitely not the current time. Traditionally, we can update the code using a callback to get called when the time is available: 

```
function getCurrentTime(callback) {
  // Get the current 'global' time from an API
  return setTimeout(function() {
    var currentTime = new Date();
    callback(currentTime);
  }, 2000);
}
getCurrentTime(function(currentTime) {
  console.log('The current time is: ' + currentTime);
});
```

What if there is an error with the rest? How do we catch the error and define a retry or error state?

```
function getCurrentTime(onSuccess, onFail) {
  // Get the current 'global' time from an API
  return setTimeout(function() {
    // randomly decide if the date is retrieved or not
    var didSucceed = Math.random() >= 0.5;
    if (didSucceed) {
      var currentTime = new Date();
      onSuccess(currentTime);
    } else {
      onFail('Unknown error');
    }
  }, 2000);
}
getCurrentTime(function(currentTime) {
  console.log('The current time is: ' + currentTime);
}, function(error) {
  console.log('There was an error fetching the time');
});
```

Now, what if we want to amke a request based upon the first request's value? As a short example, let's reuse the getCurrentTime() function inside again.

```
function getCurrentTime(onSuccess, onFail) {
  // Get the current 'global' time from an API
  return setTimeout(function() {
    // randomly decide if the date is retrieved or not
    var didSucceed = Math.random() >= 0.5;
    console.log(didSucceed);
    if (didSucceed) {
      var currentTime = new Date();
      onSuccess(currentTime);
    } else {
      onFail('Unknown error');
    }
  }, 2000);
}
getCurrentTime(function(currentTime) {
  getCurrentTime(function(newCurrentTime) {
    console.log('The real current time is: ' + currentTime);
  }, function(nestedError) {
    console.log('There was an error fetching the second time');
  })
}, function(error) {
  console.log('There was an error fetching the time');
});
```

Dealing with asynchronousity in this way can get complex quickly. Using promises , on the other hand helps us avoid a lof of this complexity. 

```
function getCurrentTime(onSuccess, onFail) {
  // Get the current 'global' time from an API using Promise
  return new Promise((resolve, reject) => {
    setTimeout(function() {
      var didSucceed = Math.random() >= 0.5;
      didSucceed ? resolve(new Date()) : reject('Error');
    }, 2000);
  })
}
getCurrentTime()
  .then(currentTime => getCurrentTime())
  .then(currentTime => {
    console.log('The current time is: ' + currentTime);
    return true;
  })
  .catch(err => console.log('There was an error:' + err))
```

This is much cleaner and clear as to what's going on. To catch the value on success, we'll use the then() funciton available on the Promise instance objet. The then() function is called with whatever the return value is of the promise itself. To catch an error that occurs anywhere in the promise chain, we can use the catch() method.

A promise only ever has one of three state at any given time:

* pending
* fulfilled(resolved)
* rejected(error)

if you would like to see my code in action check out my project:

[Monks and Ninjas React App](http://https://github.com/MonksAndNinjas/Monks-and-Ninjas-React-App)
