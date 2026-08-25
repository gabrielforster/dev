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

The `run` script accepts these optional arguments, in any order:

| Arg                    | Effect                                                                 |
|------------------------|------------------------------------------------------------------------|
| `--dry`                | Dry run. Prints what would execute, prefixed with `[DRY_RUN]:`. No changes made. |
| `--filter <list>`      | Comma separated substrings. Only scripts whose path matches at least one are executed. |
| `--filter-out <list>`  | Comma separated substrings. Scripts whose path matches any of them are skipped, even if `--filter` matched. |
| `<filter>`             | Any other positional arg is treated as `--filter`. |

Both flags also accept `--filter=a,b` form. Only one value per flag is honored — the last one wins.

### Examples

```sh
# Preview the full run without executing anything
./run --dry

# Run only the docker script (from scripts/ and after/ combined)
./run docker

# Run docker and neovim
./run --filter docker,neovim

# Run everything except cursor and spotify
./run --filter-out cursor,spotify

# Run everything from scripts/ but nothing from after/
./run --filter-out after

# Preview what running just the neovim setup would do
./run --dry neovim
```

### Languages

Run language installers manually after `asdf` is set up:

```sh
./languages/node
./languages/python
./languages/ruby
```
