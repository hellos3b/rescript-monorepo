This project has a minimal mono-repo setup for rescript to showcase an issue of importing a local package.

To setup, install the dependencies in both packages

```bash
cd packages/bar
npm install
npm run build

cd ../foo
npm install
npm run build
```

At this step, everything should work fine and as expected. But now lets update `Bar.res`. 

In packages/bar, Uncomment the `let function2 = ignore` on line 3 and run `npm build` again. This rebuilds the `bar` package.

Now in packages/foo, uncomment the line that uses `Bar.function2()` and run `npm build` for foo. Note that even though we specify `bar` as a "pinned-dependency", trying to build foo

```
rescript: [3/3] src/Main.cmj
FAILED: src/Main.cmj

  We've found a bug for you!
  /rescript-monorepo/packages/foo/src/Main.res:3:9-21

  1 │ let a = Bar.function1()
  2 │ 
  3 │ let b = Bar.function2()

  The value function2 can't be found in Bar
  
  Hint: Did you mean function1?
```

This error typically causes the VSCode extension to also stop working.

### Workaround

1. Run `npx rescript clean` everytime before building

2. Use the `Rescript: Restart Language Server` command in VSCode to fix the editor extension