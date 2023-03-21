> [!Info] Source
> [Official documentation walk through](https://ngrx.io/guide/store/walkthrough)


## Instalation

> [!Info] Source
more info in [ngrx/store Installation Guide](https://ngrx.io/guide/store/install)

Obasic installation of the store to your project [more on ng add](https://angular.io/cli/add)
```shell
## ng add will handle all npm deps
ng add @ngrx/store@latest

## or via npm (needs additonal setup)
npm install @ngrx/store --save
```
this will
1. update `package.json` dependencies with `ngrx/store`
2. runs `npm i` for those dependencies
3. update `app.module.ts` import array with `StoreModule.forRoot({})`

no minimal flag
```
ng add @ngrx/store@latest --no-minimal
```
this will do 1, 2 and additionally
3. create `src/app/reducers` folder, unless `statePath` flag is provided