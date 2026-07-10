# 任务：macOS 终端 Markdown 渲染预览工具

## 背景
用户需要在 macOS 终端（iTerm2 + zsh）中，用单命令预览 Markdown 文件，要求：
1. **单命令执行**：如 `xxx file.md` 即可打开
2. **真渲染效果**：`# 标题` 不显示 `#` 符号，`**粗体**` 显示为 ANSI 粗体（不是带 `**` 的源码高亮），列表正确缩进
3. **Vim 键位交互**： 上下滚动、`q` 退出、`/` 搜索，内容超屏时自动进入 pager，不直接输出全文，与 less 相似
4. **不串行、不乱码**：排版正确，无 `etMark┄┄` 这类乱码

## 已尝试方案及失败原因

| 工具 | 命令 | 失败表现 | 原因 |
|------|------|----------|------|
| glow | `glow file.md` | 直接输出全文，不进入交互 | tty 检测 bug，stdout 非 tty 时退化 cat 模式 |
| glow | `glow -p file.md` | 排版串行 | `-p` 模式渲染异常 |
| bat | `bat file.md` | 显示 `**` 和 `#` 符号 | bat 是语法高亮器，不是 Markdown 渲染器 |
| mdcat + less | `mdcat file.md \| less -R` | 出现 `etMark┄┄` 乱码 | mdcat 输出 OSC 8 超链接转义序列，与 `less -R` 不兼容 |
| mdcat -p | `mdcat -p file.md` | 未确认 | 待验证，但用户已不信任此路线 |

## 环境信息
- 系统：macOS（Apple Silicon）
- 终端：iTerm2
- Shell：zsh
- `tty`：/dev/ttys000
- `type glow`：/opt/homebrew/bin/glow（无 alias）
- `echo $TERM`：xterm-256color
- Homebrew 已安装

## 约束
- 不接受需要开浏览器/IDE 的方案
- 不接受显示 Markdown 源码符号（`#`、`*`、`-` 等）的方案
- 不接受乱码或排版串行的方案
- 优先单命令，次选 alias 包装
- 效率高，内存占用低

## 待执行方向
1. **自制脚本**：提供一个轻量脚本（Python/Shell 均可），实现单命令真渲染 + 自动进 less（vim 键位），并给出完整的安装步骤

