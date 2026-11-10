# clutch-index

The package index for [Egg](https://github.com/femto/egg)'s package manager,
`clutch`. It is a git repository, not a server: it maps package names to the
git repositories that hold them and to their releases.

## Format

One TOML file per package, at `packages/<name>.toml`:

```toml
name = "ansi"
repo = "https://github.com/someone/egg-ansi"

[[release]]
version = "0.1.0"
ref = "a94a8fe5cc..."   # full commit SHA in `repo`
```

- `repo` is a URL anyone can fetch; local paths and `file://` are refused.
- `ref` is always a full commit SHA, never a branch or tag name.
- Releases are listed oldest first. A release is never edited once it is
  merged; a new version is a new `[[release]]`.

## Publishing

Open a pull request that adds or extends `packages/<name>.toml`. A name
belongs to the first accepted pull request that claims it. Removing a
release is a pull request too.

`clutch` reads this repository by default; `CLUTCH_INDEX` overrides it, and a
`file://` URL works for testing.
