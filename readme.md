## Install

```bash
git clone git@github.com:stoivo/test-typescript-package-exports.git fourth-time
# Cloning into 'fourth-time'...
# Warning: remote port forwarding failed for listen port 52699
# remote: Enumerating objects: 17, done.
# remote: Counting objects: 100% (17/17), done.
# remote: Compressing objects: 100% (13/13), done.
# remote: Total 17 (delta 1), reused 17 (delta 1), pack-reused 0
# Receiving objects: 100% (17/17), 5.77 KiB | 1.92 MiB/s, done.
# Resolving deltas: 100% (1/1), done.

cd fourth-time/dep/
npm install
npm run build
#
# > dep@1.0.0 build
# > tsc -p tsconfig.json

cd ../top/
npm install
npm link ../dep
npm run build
# > top@1.0.0 build
# > tsc -p tsconfig.json

# src/lol.ts:1:19 - error TS2307: Cannot find module 'dep' or its corresponding type declarations.

# 1 import {add} from 'dep';
#                     ~~~~~

# src/lol.ts:2:17 - error TS2307: Cannot find module 'dep/sub' or its corresponding type declarations.

# 2 import sub from 'dep/sub';
#                   ~~~~~~~~~


# Found 2 errors in the same file, starting at: src/lol.ts:1
````

When I open start a node repl I can import just fine
```
node                                                                                                                       18:09:10
Welcome to Node.js v16.13.2.
Type ".help" for more information.
> await import('dep')
[Module: null prototype] { add: [Function: add], sub: [Function: sub] }
> await import('dep/add')
[Module: null prototype] { default: [Function: add] }
>
```
