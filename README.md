# scoop-bucket

Personal Scoop bucket for installing and auto-updating Windows CLI tools that are not yet available in official Scoop buckets.

[中文文档](README.zh-CN.md)

## Add this bucket

```powershell
scoop bucket add liao666brant https://github.com/liao666brant/scoop-bucket
```

## Install packages

### oc-go-cc

```powershell
scoop install oc-go-cc
```

`oc-go-cc` is a Go CLI proxy that lets you use an OpenCode Go subscription with Claude Code.

After installation:

```powershell
oc-go-cc init
$env:OC_GO_CC_API_KEY = "sk-opencode-your-key"
oc-go-cc serve
```

Configure Claude Code:

```powershell
$env:ANTHROPIC_BASE_URL = "http://127.0.0.1:3456"
$env:ANTHROPIC_AUTH_TOKEN = "unused"
claude
```

### deepseek-tui

```powershell
scoop install deepseek-tui
```

`deepseek-tui` is a terminal-native coding agent for DeepSeek models. The Scoop package installs both `deepseek.exe` and `deepseek-tui.exe` because the dispatcher delegates to the TUI runtime.

After installation:

```powershell
deepseek auth set --provider deepseek
deepseek
```

## Auto update

This bucket uses GitHub Actions to run Scoop `checkver.ps1 -Update` every day.

You can also trigger it manually from:

`Actions` → `Update Scoop manifests` → `Run workflow`
