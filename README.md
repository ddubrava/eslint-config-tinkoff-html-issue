## A reproduction for this issue - https://github.com/Tinkoff/linters/issues/180

There are some errors in `AppComponent`.
An error for `.ts` is always emitted, showing that eslint + configuration are ok.
But errors from `.html` are not emitted while `"@tinkoff/eslint-config-angular"` is extended.

That's the issue. This config breaks `.html` pattern, you can't apply any rules there.

To figure out what's the real reason for this: remove `"@tinkoff/eslint-config-angular"` from `extends` array and run `ng lint`.
You will see these errors from `.html`, it's fixed.
Then you can remove `'./internal/html'` from `index.js` in `node_modules`, and it will also fix the issue, even if `"@tinkoff/eslint-config-angular"` is extended. 

So I guess `html.js` with `files: ['*.html']` which is applied for`"files": ["*.ts"]` breaks a configuration.
