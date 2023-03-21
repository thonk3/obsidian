`@ngrx` library also provide a debugging tool `@ngrx/store-devtools` that is compatible with the browser extension `Redux DevTools`

Installation is fairly simple, either install it into the app via the cli
```shell
npm i @ngrx/store-devtools
## or
ng add @ngrx/store-devtools@latest
```

to be able to use this, `StoreDevtoolsModule` also needed to be also imported inside your `app.module.ts`
and pass into a config object into its `instrument()` option.

The Devtools gives you the following features:
- `Inspector`
- `Log monitor`
- `Chart`
- `Time-Traveling`
- `Dispatcher`
- `Export / Import`
- `Lock / Persist`

> also include some notes about how to implement this for prod release, may be useful to see later

--- 
next chapter [[NilsNgRx - 6 - File Structure and Naming]]
