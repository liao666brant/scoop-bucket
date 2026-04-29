# scoop-bucket

这是一个个人维护的 [Scoop](https://scoop.sh/) bucket 仓库，用于在 Windows 上安装和自动更新一些尚未收录到官方 bucket 的命令行工具。

## 添加 bucket

在 PowerShell 中执行：

```powershell
scoop bucket add liao666brant https://github.com/liao666brant/scoop-bucket
```

添加成功后，就可以通过 `scoop install` 安装本仓库中的软件。

## 当前软件包

### oc-go-cc

`oc-go-cc` 是一个 Go 编写的 CLI 代理工具，可以让 Claude Code 通过 Anthropic API 格式访问 OpenCode Go 订阅。

项目地址：

```txt
https://github.com/samueltuyizere/oc-go-cc
```

安装：

```powershell
scoop install oc-go-cc
```

查看版本：

```powershell
oc-go-cc --version
```

初始化配置：

```powershell
oc-go-cc init
```

设置 OpenCode Go API Key：

```powershell
$env:OC_GO_CC_API_KEY = "sk-opencode-your-key"
```

启动代理服务：

```powershell
oc-go-cc serve
```

默认监听地址为：

```txt
http://127.0.0.1:3456
```

然后配置 Claude Code：

```powershell
$env:ANTHROPIC_BASE_URL = "http://127.0.0.1:3456"
$env:ANTHROPIC_AUTH_TOKEN = "unused"
claude
```

## 更新软件

更新 bucket 信息：

```powershell
scoop update
```

更新 `oc-go-cc`：

```powershell
scoop update oc-go-cc
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

`bucket/oc-go-cc.json` 中包含：

- `version`：当前软件版本；
- `architecture`：不同 CPU 架构对应的下载地址；
- `bin`：安装后暴露到命令行的可执行文件；
- `checkver`：用于检查 GitHub Release 最新版本；
- `autoupdate`：用于自动拼接新版本下载地址并更新 hash。

`oc-go-cc` 的 Windows Release 文件名为：

```txt
oc-go-cc_windows-amd64.exe
oc-go-cc_windows-arm64.exe
```

安装时会通过 Scoop 的 `#/oc-go-cc.exe` 规则重命名为统一的：

```txt
oc-go-cc.exe
```

因此安装后可以直接使用：

```powershell
oc-go-cc
```

## 注意事项

- 第一次添加 manifest 时，如果使用了 `releases/latest/download` 和 `hash: skip`，建议尽快运行一次 GitHub Actions，让 Scoop 自动更新到真实版本号和 hash。
- 如果安装失败，优先检查上游 Release 是否包含对应架构的 Windows 文件。
- 如果 `scoop install` 找不到包，确认是否已经执行过 `scoop bucket add`。
- 如果自动更新没有提交变化，通常说明上游没有新版本。

## 常用命令

```powershell
# 添加 bucket
scoop bucket add liao666brant https://github.com/liao666brant/scoop-bucket

# 安装 oc-go-cc
scoop install oc-go-cc

# 更新 bucket 索引
scoop update

# 更新 oc-go-cc
scoop update oc-go-cc

# 卸载 oc-go-cc
scoop uninstall oc-go-cc

# 查看已添加的 bucket
scoop bucket list
```
