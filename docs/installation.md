# Installation

This page covers the practical ways to add Promise to a Roblox project.

## Method 1: Wally

For projects already using Wally, this is the cleanest setup.

```toml
[dependencies]
Promise = "cometahn142/promise@^0.1"
```

After that, install dependencies through your normal Wally workflow and expose
the package through your Rojo project as you would with any other shared module.

## Method 2: Manual

If you are not using a package manager yet, you can still use the library
directly:

1. Create a `ModuleScript` named `Promise`.
2. Copy the contents of `src/init.luau` into it.
3. Place it somewhere your code can require consistently.

This works fine for small projects, prototypes, or local experiments.

## Method 3: Source-controlled submodule or vendor folder

If your project vendors libraries directly into source control, place Promise in
your third-party module folder and sync it through Rojo. This approach is often
useful when you want full control over version bumps and reviewable diffs.

## Verifying the installation

Once installed, this should work:

```luau
local Promise = require(Packages.Promise)

Promise.resolve("ok"):andThen(function(value)
	print(value)
end)
```

If you see `"ok"` in the output, the package is wired correctly.

## Next

- [Usage Patterns](./usage-patterns.md)
- [Promise API](./promise.md)

## License

MIT. See `LICENSE`.
