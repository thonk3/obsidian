Install ngrx
```shell
npm i @ngrx store
```

Import `StoreModule` into `AppModule` using its static method `forRoot()`
- since this is the point where we ==register the root state of the application==

This can be automated using angular cli
```shell
ng add @ngrx/store/latest
```

optionally install this for generating NgRx building blocks through the CLI-schematics
```shell
ng add @ngrx/schematics@latest
```

this also config ngrx schematic collection to be used as defauklt by angular
```
npm i @ngrx/schematics --save-dev
ng config cli.defaultCollection @ngrx/schematics
```

--- 
next chapter [[NilsNgRx - 4 - First Steps]]