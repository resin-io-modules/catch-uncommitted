# Catch-Uncommitted

A simple sh script to error if you have uncommitted or unversioned files in your current directory.

This is designed to be used in your CI process, if you have some generated build output committed, to
ensure that it's up to date. Run your build, then run this script, and it'll fail if there's any
new or changed files that appear.

Checks for new files using git, so this won't complain git ignored files change.

This depends on `/bin/sh` pointing to a sensible shell, and on `git` and `tee` being available
in your `$PATH`.

## Get started

Install it:

```
npm install --save-dev catch-uncommitted
```

Add it to your CI script in package.json:

```
"scripts": {
    "ci": "npm run build && catch-uncommitted"
}
```

Run it:

```
npm run ci

[... your build here ...]

No unexpected changes, all good.
```

## Extra options

### --catch-no-git

When running `catch-uncommitted --catch-no-git`, the script will exit without an
error when git isn't available. This can be useful when you need to run the same
tests in different environments, where some of them do not have git available.

### --skip-node-versionbot-changes

When running `catch-uncommitted --skip-node-versionbot-changes`, the script will
skip checking the `package.json` & the `CHANGELOG.md` for changes, so that it
can work as part of the balenaCI pipeline.
