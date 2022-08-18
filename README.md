# Reproduction of https://github.com/npm/cli/issues/3847

## Steps / Commits
1, Base repo - no dependencies installed

2, Ran `npm install ./packages/package-1 -w apps/app-1`

This returns `npm ERR! Cannot set properties of null (setting 'dev')`

Not sure if this command is incorrect or what the correct version is - but it's what I ran thinking it was how i linked my workspaces

Returning the error suggested i was wrong, so the next commit tries to undo that


## Result
First reaction was to run `npm uninstall ./packages/package-1 -w apps/app-1` - this does nothing and leaves the repo as is

Running any install command e.g. `npm install esbuild -w apps/app-1` - will seemingly succeed but return the same error from now on as the config is broken


## Manual Fix
To manually fix this you can delete `apps/app-1/node_modules/package-1` (lines 23-26) from `package-lock.json` and the `"package-1": "file:packages/package-1"` (line 9) from app-1's `package.json`

After that, install commands for the workspace no longer return errors
