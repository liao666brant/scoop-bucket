# scoop-bucket

Personal Scoop bucket for installing and auto-updating Windows CLI tools that are not yet available in official Scoop buckets.

[中文文档](README.zh-CN.md)

## Add this bucket

```powershell
scoop bucket add liao666brant https://github.com/liao666brant/scoop-bucket
```

## Install packages

### browserskill

```powershell
scoop install browserskill
```

`browserskill` connects shell-capable AI agents such as Codex, Claude Code, and Cursor to a logged-in Chrome or Edge browser. The Scoop package installs the `bsk` CLI; install the [BrowserSkill extension](https://chromewebstore.google.com/detail/hhcmgoofomhgciiibhipgmgkgnoenaoi) separately.

After installation:

```powershell
bsk install-skill
bsk status
```

### nub

```powershell
scoop install nub
```

`nub` is a fast all-in-one Node.js toolkit (runtime, package manager, script runner, and version manager). Homepage: [nubjs.com](https://nubjs.com). Source: [nubjs/nub](https://github.com/nubjs/nub).

## Auto update

This bucket uses GitHub Actions to run Scoop `checkver.ps1 -Update` every day.

You can also trigger it manually from:

`Actions` → `Update Scoop manifests` → `Run workflow`
