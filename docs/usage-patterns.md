# Usage Patterns

This page focuses less on individual functions and more on how Promise fits
into real Roblox code.

## Wrapping asynchronous work

Use `Promise.new` when the underlying operation is asynchronous and you want the
result to be explicit and composable.

```luau
local function loadPlayerData(userId)
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
```

## Transforming results

Use `andThen` when one async result should flow into the next step.

```luau
loadPlayerData(42)
	:andThen(function(profile)
		return profile.Coins
	end)
	:andThen(function(coins)
		print("Coins:", coins)
	end)
```

## Handling failures

Use `catch` when the current boundary is responsible for dealing with rejection.

```luau
loadPlayerData(0)
	:catch(function(err)
		warn("Could not load player data:", err)
	end)
```

## Waiting for multiple tasks

Use combinators when several async tasks belong to one logical flow.

```luau
Promise.all({
	loadInventory(),
	loadStats(),
	loadSettings(),
})
```

Common rules of thumb:

- `all` for "everything must succeed"
- `race` for "first result wins"
- `any` for "first success wins"
- `allSettled` for "show me every result"

## Cancellation

Cancellation matters most when the caller may disappear before the work
completes, such as:

- UI screens closing
- players leaving
- objects being destroyed
- requests being superseded by newer requests

```luau
local p = loadPlayerData(42):timeout(5)
p:cancel()
```

If your executor starts background work, register cleanup with `onCancel`.

## Awaiting in coroutine-based code

If you are inside a coroutine already, `await` is often the cleanest bridge:

```luau
local ok, result = loadPlayerData(42):await()
if ok then
	print(result.Coins)
end
```

Use this sparingly at boundaries where the synchronous style is easier to read.
Inside reusable library code, returning the Promise is usually better.

## Practical Advice

- Return Promises from async APIs instead of yielding unexpectedly.
- Prefer small chains over deeply nested callbacks.
- Add timeouts around external or player-driven operations.
- Catch rejections at ownership boundaries, not everywhere.

## Next

- [Installation](./installation.md)
- [Promise API](./promise.md)

## License

MIT. See `LICENSE`.
