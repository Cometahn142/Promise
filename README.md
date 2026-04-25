# Promise

Promise is a Promise library for Roblox (Luau) designed to make asynchronous
code easier to compose, easier to reason about, and easier to cancel.

Roblox's default async style is mostly based on yielding and resuming threads.
That works for small scripts, but it becomes difficult to scale once multiple
async operations need to run together, fail independently, or be cancelled when
their result is no longer needed.

This library takes the Promise approach instead:

- asynchronous work is represented by a value
- that value can be chained and composed
- success and failure are handled explicitly
- cancellation is part of the model

## Why use Promises

Promises help with a few recurring Roblox problems:

- A function may yield unexpectedly, or only sometimes, which makes control
  flow hard to predict.
- Running several async tasks together often turns into nested callbacks or
  repeated success checks.
- Error handling usually ends up split between `pcall`, tuple returns, and
  custom conventions.
- Work that is no longer needed often keeps running unless you clean it up
  manually.

Promises make those cases more uniform. You create a unit of asynchronous work
once, then chain it, combine it, await it, timeout it, or cancel it from one
place.

## Features

- Familiar chaining with `andThen`, `catch`, and `finally`
- Explicit cancellation
- Timeouts and immediate status inspection
- Combinators like `all`, `race`, `any`, `allSettled`, and `some`
- Utility helpers like `each`, `fold`, `retry`, and `retryWithDelay`
- Structured `Promise.Error` values and unhandled rejection hooks

## Installation

```toml
[dependencies]
Promise = "cometahn142/promise@^0.1"
```

## Quick Example

```luau
local Promise = require(Packages.Promise)

local function loadProfile(userId)
	return Promise.new(function(resolve, reject)
		task.delay(1, function()
			if userId <= 0 then
				reject("Invalid user id")
				return
			end

			resolve({
				UserId = userId,
				Coins = 100,
			})
		end)
	end)
end

loadProfile(42)
	:andThen(function(profile)
		print("Loaded profile for", profile.UserId)
		return profile.Coins
	end)
	:andThen(function(coins)
		print("Coins:", coins)
	end)
	:catch(function(err)
		warn("Profile load failed:", err)
	end)
```

## Documentation

- [Installation](./docs/installation.md)
- [Usage Patterns](./docs/usage-patterns.md)
- [Promise API](./docs/promise.md)

## License

MIT. See `LICENSE`.
