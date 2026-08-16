# 🛠️ Dev Utilities

A curated collection of handy developer utilities — scripts, snippets, and CLI tools to speed up your daily workflow.

## Motivation

Every developer has their go-to set of scripts and commands. This repo organizes mine in one place so I (and you) can find them fast.

## Current Tools

### `clean_branches.sh` — Git Branch Cleaner
Safely delete local git branches that have already been merged into main. No more `git branch | grep -v main | xargs git branch -D` roulette.

```bash
git branch --merged main | grep -v "^\* main$" | xargs -n 1 git branch -d
```

### `mkcd` — Make & Enter Directory
Create a directory and `cd` into it immediately.

```bash
mkcd() { mkdir -p "$1" && cd "$1"; }
```

### `extract()` — Universal Extract
Works with tar, tar.gz, tar.bz2, zip, rar, 7z, gz, bz2 — no more googling which flag to use.

```bash
extract() {
  if [ -f "$1" ]; then
    case "$1" in
      *.tar.gz)   tar xzf "$1"   ;;
      *.tar.bz2)  tar xjf "$1"   ;;
      *.tar)      tar xf "$1"    ;;
      *.zip)      unzip "$1"     ;;
      *.rar)      unrar x "$1"   ;;
      *.7z)       7z x "$1"      ;;
      *.gz)       gunzip "$1"    ;;
      *.bz2)      bunzip2 "$1"   ;;
      *)          echo "Unknown format: $1" ;;
    esac
  fi
}
```

### `gen_rand()` — Random String Generator
Generate a cryptographically-random string of any length (default 32).

```bash
gen_rand() {
  local length=${1:-32}
  openssl rand -hex "$length"
}
```

## Contributing

Spotted a bug or have a utility worth adding? Open an issue or PR — contributions are welcome.

## License

MIT
