---
title: Shell & CLI Fundamentals
created: 2026-07-22
updated: 2026-07-22
type: concept
tags: [shell, cli, linux, bash, powershell]
sources: []
confidence: high
---

# Shell & CLI 基础

## 定义

Shell 是操作系统的**命令行解释器**——你输入命令，它帮你执行。CLI (Command-Line Interface) 是高效操作的根基，尤其对开发者。

## Unix Shell

### Bash (Bourne-Again SHell)

最通用的 Shell，几乎所有 [[linux]] 系统的默认。1989 年发布，POSIX 兼容。

```bash
# 变量
name="world"
echo "Hello $name"

# 管道
cat file.txt | grep "error" | wc -l

# 重定向
ls > output.txt       # stdout 到文件
ls 2> errors.txt      # stderr 到文件
ls &> all.txt         # 都到文件

# 循环
for f in *.txt; do
    echo "Processing $f"
done

# 条件
if [ -f "config.yaml" ]; then
    echo "Config exists"
fi
```

### Zsh

Bash 的超集，macOS 默认 (Catalina+)。Oh My Zsh 插件生态系统丰富。

| 特性 | Bash | Zsh |
|------|------|-----|
| 自动补全 | 基础 | ✅ 强大 |
| 拼写纠正 | ❌ | ✅ |
| 主题 | ❌ | ✅ Oh My Zsh |
| 插件 | ❌ | ✅ 大量社区 |

### Fish (Friendly Interactive SHell)

开箱即用，无需配置——自动建议、语法高亮、Web 配置界面。但不 POSIX 兼容（不能直接跑 bash 脚本）。

## Windows Shell

### PowerShell

```powershell
# 面向对象（不是文本！）
Get-Process | Where-Object { $_.CPU -gt 100 } | Sort-Object CPU -Descending

# 变量
$name = "world"
Write-Output "Hello $name"

# 管道传递对象（不是文本）
Get-ChildItem | ForEach-Object { $_.Name }
```

| 维度 | PowerShell | Bash |
|------|-----------|------|
| 数据 | .NET 对象 | 文本流 |
| 命名 | Verb-Noun | 随意 |
| 脚本 | `.ps1` | `.sh` |
| 跨平台 | ✅ (PowerShell Core) | ✅ (WSL/Git Bash) |

### WSL (Windows Subsystem for Linux)

Windows 上原生运行 [[linux]] 环境。2016 年引入，WSL 2 使用完整 Linux 内核。

```powershell
wsl --install           # 安装 WSL 2 + Ubuntu
wsl ls /home            # 从 Windows 运行 Linux 命令
```

## 必备命令

| 命令 | 用途 |
|------|------|
| `ls` / `dir` | 列出文件 |
| `cd` | 切换目录 |
| `grep` / `findstr` | 文本搜索 |
| `find` / `Get-ChildItem -Recurse` | 文件搜索 |
| `sed` / `awk` | 文本处理 |
| `ps` / `top` / `htop` | 进程管理 |
| `curl` / `wget` | HTTP/文件下载 |
| `chmod` / `chown` | 权限管理 |
| `ssh` | 远程连接 |
| `git` | 版本控制 |
| `docker` / `kubectl` | 容器编排 |
| `|` (pipe) | 串联命令 |
| `>` / `>>` | 重定向 |

## 高级技术

| 技术 | 说明 |
|------|------|
| Subshell | `$(command)` 获取命令输出 |
| Process substitution | `diff <(ls dir1) <(ls dir2)` |
| trap | 捕获信号 (Ctrl+C 清理临时文件) |
| xargs | 将 stdin 转为命令行参数 |
| tee | 同时输出到屏幕和文件 |

## 关系

- [[linux]]
- [[python]] — 脚本替代 Shell
