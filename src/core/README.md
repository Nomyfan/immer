## `produce` function

## philosophy

Any base state passed into `produce` function is treated as immutable value which is read-only. Based on this, we can pass a freezed object into it.

It has a side effect that's it freeze a state. That says, if we pass a plain object into it as the base state and we do nothing to it, it will return the freezed state.

For example:

```js
import {produce} from "immer"

const baseState = {
	name: "Immer"
}

const nextState = produce(baseState, draft => {})

console.log(baseState === nextState) // true
baseState.name = "baseState" // error
nextState.name = "nextState" // error
```

We can disable this by calling `setAutoFreeze(false)`

### Q&A

Q: Why cannot we mutate and return a new state at the same time? For example:

```js
import {produce} from "immer"

const baseState = {
	name: "Immer"
}

const nextState = produce(baseState, draft => {
	draft.name = "nextState"

	return {name: "newState"}
}) // error
```

A: It's not reasonable to do both.

## patches and inversePatches

In `finalize` function, it will call `generatePatches_` finally to compare the original state and copied state what are removed, added and replaced.

## proxy

TBD

## scope

TBD

## What I think

The most cool and exiting feature I think Immer offered is returning `pathes` and `inversePatches`. Based on this, we can record the operation history accomplishing some features like `undo` and `redo` in an editor.
