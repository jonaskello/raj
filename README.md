# Raj

> The best JavaScript framework

```sh
npm install raj
```

[![npm](https://img.shields.io/npm/v/raj.svg)](https://www.npmjs.com/package/raj)
[![Build Status](https://travis-ci.org/andrejewski/raj.svg?branch=master)](https://travis-ci.org/andrejewski/raj)

## Documentation

- `raj/message`: define message and message unions
  - `message([displayName])`: create a message
  - `message.union([displayName, ] messages)`: create a message union
- `raj/runtime`: create generic runtimes
  - `program({init, update, renderer})`
    - `init`: the initial state and optional effect
    - `update(message, state)`: return the new state and optional effect
    - `renderer(state, dispatch)`: use the state and dispatch messages

#### Integrations
- `raj/react`: React bindings
  - `program(React, {init, update, view})`: create a React program
    - `React`: a version of React which has `React.Component`
    - `init(props)`: return the initial state and optional effect
    - `update(message, state)`: return the new state and optional effect
    - `view(state, dispatch)`: return the React view

## Architecture

The data flow is unidirectional.
The update creates a new state and optionally triggers an effect based on the current state and a received message.
The view is a function of state.
The view and any side-effects communicate by dispatching messages.

Building any app follows the same steps:

1. Define your data model with `init(flags)`
1. Define your messages with `message/message.union`
1. Define your behaviors with `update(message, state)`
1. Define your effects as functions which accept a dispatch function
1. Define your view with `view(state, dispatch)`
1. Tie it all together with `program()`

## Examples

- `examples/search`: Dummy search widget where a query updates a list of search results.
- `examples/make-n-model`: Dummy loader where a selected make loads a list of relevant models.
