## issue#2 test case

```bash
git clone https://github.com/talmobi/wrollup_issue_2
cd wrollup_issue_2
npm install
npm run watch
```

Open a new terminal.

Add syntax error to ```bar.js``` and notice a simple syntax parse error (No RangeError: Maximum call stack error)

```
echo "::" > bar.js
```

output:
```
trigger from: /Users/mollie/temp/wrollup_issue_2/bar.js
``` PARSE_ERROR
::
^

PARSE_ERROR: Unexpected token (1:0) in [bar.js]
url: /Users/mollie/temp/wrollup_issue_2/bar.js
starting build error watcher [**/*.js*]
```

Nothing out of the ordinary, now re-add the correct syntax

```
echo "export var bar = 'bar'" > bar.js
```

and notice correct output with no errors:
```
removing global watcher
  watching /wrollup_issue_2/bar.js
  watching /wrollup_issue_2/baz.js
  watching /wrollup_issue_2/foo.js
compiled bundle.js
```

Everyhine OK.

However, install latest rollup version 0.36.1

```
npm install --save-dev rollup@latest
```

close and re-run the watcher

```
npm run watch
```

edit bar.js and notice RangeError: maximum call stack exceed error:

```
echo "::" > bar.js
```

output:
```
trigger from: /Users/mollie/temp/wrollup_issue_2/bar.js
``` PARSE_ERROR
::
^

PARSE_ERROR: Unexpected token (1:0) in [bar.js]
url: /Users/mollie/temp/wrollup_issue_2/bar.js
starting build error watcher [**/*.js*]
RangeError: Maximum call stack size exceeded
    at deepClone (/Users/mollie/temp/wrollup_issue_2/node_modules/rollup/dist/rollup.js:153:20)
    at deepClone (/Users/mollie/temp/wrollup_issue_2/node_modules/rollup/dist/rollup.js:165:18)
    at deepClone (/Users/mollie/temp/wrollup_issue_2/node_modules/rollup/dist/rollup.js:165:18)
    at deepClone (/Users/mollie/temp/wrollup_issue_2/node_modules/rollup/dist/rollup.js:165:18)
    at deepClone (/Users/mollie/temp/wrollup_issue_2/node_modules/rollup/dist/rollup.js:165:18)
    at deepClone (/Users/mollie/temp/wrollup_issue_2/node_modules/rollup/dist/rollup.js:165:18)
    at deepClone (/Users/mollie/temp/wrollup_issue_2/node_modules/rollup/dist/rollup.js:165:18)
    at deepClone (/Users/mollie/temp/wrollup_issue_2/node_modules/rollup/dist/rollup.js:165:18)
    at deepClone (/Users/mollie/temp/wrollup_issue_2/node_modules/rollup/dist/rollup.js:165:18)
    at deepClone (/Users/mollie/temp/wrollup_issue_2/node_modules/rollup/dist/rollup.js:165:18)
build error watcher still ready [**/*.js*]

```
