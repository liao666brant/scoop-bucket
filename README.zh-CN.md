# scoop-bucket

这是一个个人维护的 [Scoop](https://scoop.sh/) bucket 仓库，用于在 Windows 上安装和自动更新一些尚未收录到官方 bucket 的命令行工具。

## 添加 bucket

在 PowerShell 中执行：

```powershell
scoop bucket add liao666brant https://github.com/liao666brant/scoop-bucket
```

添加成功后，就可以通过 `scoop install` 安装本仓库中的软件。

## 当前软件包

### browserskill

`browserskill` 让 Codex、Claude Code、Cursor 等能够执行 Shell 命令的 AI Agent 操作已登录的 Chrome 或 Edge。Scoop 包安装的是 `bsk` CLI；浏览器扩展需要另外安装。

项目地址：

```txt
https://github.com/Tencent/BrowserSkill
```

安装：

```powershell
scoop install browserskill
```

安装浏览器扩展：

```txt
https://chromewebstore.google.com/detail/hhcmgoofomhgciiibhipgmgkgnoenaoi
```

为当前使用的 AI Agent 安装技能：

```powershell
bsk install-skill
```

检查 CLI、后台服务和浏览器扩展连接：

```powershell
bsk status
```

## 更新软件

更新 bucket 信息：

```powershell
scoop update
```

更新单个软件：

```powershell
scoop update browserskill
```

更新所有软件：

```powershell
scoop update *
```

## 自动维护机制

本仓库通过 GitHub Actions 每天自动运行 Scoop 的 `checkver.ps1 -Update`，用于检查上游 GitHub Release 是否发布了新版本。

自动更新流程：

1. 每天定时执行 GitHub Actions；
2. 检查 `bucket/*.json` 中配置的 `checkver`；
3. 如果发现上游有新版本，自动更新 manifest；
4. 根据 `autoupdate` 规则更新下载地址和 hash；
5. 如果文件有变化，自动提交到当前仓库。

也可以手动触发：

```txt
GitHub 仓库 → Actions → Update Scoop manifests → Run workflow
```

## manifest 说明

`bucket/*.json` 中通常包含：

- `version`：当前软件版本；
- `architecture`：不同 CPU 架构对应的下载地址；
- `bin`：安装后暴露到命令行的可执行文件；
- `checkver`：用于检查 GitHub Release 最新版本；
- `autoupdate`：用于自动拼接新版本下载地址并更新 hash。

## 注意事项

- 第一次添加 manifest 时，如果使用了 `releases/latest/download` 和 `hash: skip`，建议尽快运行一次 GitHub Actions，让 Scoop 自动更新到真实版本号和 hash。
- 如果安装失败，优先检查上游 Release 是否包含对应架构的 Windows 文件。
- 如果 `scoop install` 找不到包，确认是否已经执行过 `scoop bucket add`。
- 如果自动更新没有提交变化，通常说明上游没有新版本。

## 常用命令

```powershell
# 添加 bucket
scoop bucket add liao666brant https://github.com/liao666brant/scoop-bucket

# 安装软件
scoop install browserskill

# 更新 bucket 索引
scoop update

# 更新软件
scoop update browserskill

# 卸载软件
scoop uninstall browserskill

# 查看已添加的 bucket
scoop bucket list
```
