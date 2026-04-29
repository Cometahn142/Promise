# Promise

This page summarizes the public API surface of the Promise module.

## Constructors

- `Promise.new(executor)`
- `Promise.defer(executor)`
- `Promise.resolve(value)`
- `Promise.reject(reason)`
- `Promise.try(fn, ...)`

Use these to create Promise values from async executors, immediate values, or code that may throw.

## Adapters

- `Promise.promisify(callback)`
- `Promise.fromEvent(event, predicate?)`
- `Promise.delay(seconds)`

These helpers adapt callback-style or event-style workflows into Promise-based flows.

## Combinators

- `Promise.all(promises)`
- `Promise.some(promises, count)`
- `Promise.race(promises)`
- `Promise.any(promises)`
- `Promise.allSettled(promises)`
- `Promise.each(list, predicate)`
- `Promise.fold(list, reducer, initialValue)`

These functions help coordinate multiple pieces of asynchronous work.

## Retry Helpers

- `Promise.retry(callback, times, ...)`
- `Promise.retryWithDelay(callback, times, seconds, ...)`

These are useful when failures may be temporary.

## Instance Methods

- `andThen(onFulfilled?, onRejected?)`
- `catch(onRejected)`
- `finally(onFinally)`
- `tap(onTap)`
- `andThenCall(callback, ...)`
- `andThenReturn(...)`
- `finallyCall(callback, ...)`
- `finallyReturn(...)`
- `now(rejectionValue?)`
- `timeout(seconds, rejectionValue?)`
- `cancel()`
- `getStatus()`
- `awaitStatus()`
- `expect()`
- `await()`

## Status Constants

- `Promise.Status.Pending`
- `Promise.Status.Fulfilled`
- `Promise.Status.Rejected`
- `Promise.Status.Cancelled`

## Error API

- `Promise.Error.new(options?)`
- `Promise.Error.is(value)`
- `Promise.Error.Kind.ExecutionError`
- `Promise.Error.Kind.AlreadyCancelled`
- `Promise.Error.Kind.NotResolvedInTime`
- `Promise.Error.Kind.TimedOut`

## Hooks

- `Promise.onUnhandledRejection(callback) -> disconnectFn`

Use this when you want central reporting for unhandled rejected Promises.

## Related Docs

- [Installation](./installation.md)
- [Usage Patterns](./usage-patterns.md)

## License

MIT. See `LICENSE`.
