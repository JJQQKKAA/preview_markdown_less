# preview markdown like less

Preview Markdown in iTerm (or any terminal) in a less-like way.

`mdp` is a single-file Python 3 script with no pip dependencies. It renders a practical subset of Markdown to ANSI and automatically opens long output in `less -R`.

## Installation

```sh
cp bin/mdp /opt/homebrew/bin/mdp
chmod +x /opt/homebrew/bin/mdp
```

Or install to any directory already in your `PATH`.

## Usage

```sh
mdp file.md          # preview file.md
mdp                  # read from stdin
cat file.md | mdp
mdp -p file.md       # always open in pager
mdp -c file.md       # disable ANSI colors
mdp -h               # help
```

## Supported Markdown

- Headings (H1–H6), with H1 underlined
- Bold, italic, inline code
- Fenced code blocks with dark background
- Unordered/ordered lists
- Task lists (`- [ ]` / `- [x]`)
- Blockquotes
- Links (URL preserved), images (placeholder with URL)
- Simple tables
- Horizontal rules

## Wrapping

`mdp` wraps lines at the terminal display-width boundary. Spaces are preserved as-is but are not treated as preferred break points. This keeps Chinese text and short English fragments (e.g. `Level 1`, `20K`, `HRBP`) flowing together as one paragraph.

When output fits the terminal height, it prints directly. When it exceeds the screen, it enters `less -R` so you can scroll with Vim keybindings (`j`, `k`, `/`, `q`, etc.).

---

# 像 less 一样预览 Markdown

在 iTerm（或任何终端）中以 less 的方式预览 Markdown。

`mdp` 是一个单文件 Python 3 脚本，零 pip 依赖。它将 Markdown 的一个实用子集渲染为 ANSI，并在内容较长时自动进入 `less -R`。

## 安装

```sh
cp bin/mdp /opt/homebrew/bin/mdp
chmod +x /opt/homebrew/bin/mdp
```

或者安装到任意已在 `PATH` 中的目录。

## 用法

```sh
mdp file.md          # 预览 file.md
mdp                  # 从 stdin 读取
cat file.md | mdp
mdp -p file.md       # 强制进入 pager
mdp -c file.md       # 关闭 ANSI 颜色
mdp -h               # 帮助
```

## 支持的 Markdown

- 标题（H1–H6），H1 带下划线
- 粗体、斜体、行内代码
- 带深色背景的围栏代码块
- 无序/有序列表
- 任务列表（`- [ ]` / `- [x]`）
- 引用块
- 链接（保留 URL）、图片（显示为占位符+URL）
- 简单表格
- 水平分割线

## 换行

`mdp` 按终端显示宽度边界换行。空格会原样保留，但**不会**被当作优先换行点。这样中文段落中夹杂的短英文片段（如 `Level 1`、`20K`、`HRBP`）会保持连在一起，像一整段文本一样连续流动。

当输出高度不超过终端高度时直接输出；超出屏幕时自动进入 `less -R`，可用 Vim 键位滚动（`j`、`k`、`/`、`q` 等）。
