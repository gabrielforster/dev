## DEV

List of scripts I use to setup a brand new Linux machine (Debian/Ubuntu based).

Heavily inspired by @theprimeagen's [Developer Productivity v2](https://frontendmasters.com/workshops/developer-productivity-v2/) course.

## Layout

- `scripts/` — base installers (apt packages, editors, terminals, docker, etc.). Run first.
- `after/` — things that depend on `scripts/` (asdf plugins, aws cli, fonts, dotfiles, browsers). Run after.
- `languages/` — asdf language installers (`node`, `python`, `ruby`). Not invoked by `run`; execute manually once asdf is installed.
- `run` — orchestrator that iterates over `scripts/` then `after/`.

## Usage

Run everything:

```sh
./run
```

### Parameters

The `run` script accepts two optional arguments, in any order:

| Arg        | Effect                                                                 |
|------------|------------------------------------------------------------------------|
| `--dry`    | Dry run. Prints what would execute, prefixed with `[DRY_RUN]:`. No changes made. |
| `<filter>` | Any other positional arg is treated as a filter. Only scripts whose path contains this substring are executed; the rest are skipped. |

Only one filter is honored — the last non-`--dry` arg wins.

### Examples

```sh
# Preview the full run without executing anything
./run --dry

# Run only the docker script (from scripts/ and after/ combined)
./run docker

# Preview what running just the neovim setup would do
./run --dry neovim

# Run only the 'after' hooks matching 'fonts'
./run fonts
```

### Languages

Run language installers manually after `asdf` is set up:

```sh
./languages/node
./languages/python
./languages/ruby
```
