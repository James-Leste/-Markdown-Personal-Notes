# Notes {ignore=true}

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [CSS](#css)
  - [Flexbox](#flexbox)
- [MacOS commands](#macos-commands)
  - [Environment variables](#environment-variables)
  - [Command/Bash](#commandbash)
- [Linux Command](#linux-command)
  - [Check Linux	Release Version](#check-linux-release-version)
- [MacOS command line tools](#macos-command-line-tools)
  - [Homebrew](#homebrew)
  - [Tree](#tree)
- [Vim cheat sheet (Often used)](#vim-cheat-sheet-often-used)
  - [often used atomic commands](#often-used-atomic-commands)
  - [often used combination commands](#often-used-combination-commands)

<!-- /code_chunk_output -->
## CSS
### Flexbox
- **flexbox layout**(use on parent elements): `display: flex;`
- **flexbox direction**(either row or column):`flex-direction`
	`row` horizontal direction
	`column` vertical direction
	`column-reverse` horizontal reverse direction
	`row-reverse` vertical reverse direction
- **与row和column相同方向的对齐方式** `justify-content` 
	`space-around`
	`space-between`
	`flex-start`
	`flex-end`
	`center`
- **与row和column垂直的对齐方式**`align-items`
	`stretch` same height(width) for all elements
	`center`
	`baseline`
	`flex-start`
	`flex-end`

---

## MacOS commands
### Environment variables
- make environment configuration file take effect
```bash
	source ~/.bash_profile
```
**happy**

### Command/Bash
- Check ongoing process on a port（进程）
```bash
	lsof -i:8000 # Check processes on a specific port
	kill 85877 # Terminate process with given PID
```
---

## Linux Command
### Check Linux	Release Version
```bash
	cat /etc/*-release
```

---
## MacOS command line tools
### Homebrew
- Homebrew location on machine: `/opt/homebrew`  
	Homebrew command：`brew`

### Tree
- Command: `tree`
	list the file structure of the root directory.

## Vim cheat sheet (Often used)
### often used atomic commands
- save and quit: `:wq`
- undo: `u`
- enter insert mode: `i`
- exit mode: key `esc`

### often used combination commands
- Clear whole document: `gg` + `dg` in normal mode