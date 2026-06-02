# pweb (redirect package) — Claude Context

## What this is

A thin npm redirect package published under the unscoped name `pweb`. Its only purpose is to let users install the CLI with:

```bash
npm install -g pweb
```

instead of the scoped name `@portableweb/cli`. It declares `@portableweb/cli` as a dependency and re-exports its bin via `bin/pweb.js`.

## Structure

```
pweb-redirect/
  package.json      # name: "pweb", depends on @portableweb/cli
  bin/pweb.js       # one-liner: require("@portableweb/cli")
```

## How it works

`bin/pweb.js` simply `require`s `@portableweb/cli`, which runs that package's `dist/index.js` entry point. No logic lives here.

## What not to change

- Do not add any logic to `bin/pweb.js` — all CLI code lives in `@portableweb/cli`.
- Keep the version of `@portableweb/cli` in `dependencies` in sync with releases. The range `^0.1.0` picks up patch/minor bumps; bump the floor when a new major/minor is released.
- The two bin names (`pweb` and `portableweb`) must match those declared in `@portableweb/cli/package.json`.

## Relation to other packages

- `../cli/` (`@portableweb/cli`) — the real CLI this package wraps.
- `../portableweb-redirect/` (`portableweb`) — the other redirect package, identical in structure but published under the `portableweb` npm name.
- All three packages should be released together. When `@portableweb/cli` cuts a new version, update the dependency in both redirect packages and publish them with matching version bumps.
