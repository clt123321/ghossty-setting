# Ghostty Terminal Setup

> 一套现代化的 macOS 终端配置：**Ghostty + Zoxide + Yazi + Oh-My-Zsh**

GPU 加速终端 + 智能目录跳转 + Vim 风格文件管理器 + 强力 Zsh 配置框架，开箱即用、键盘流、速度起飞。

## 📦 工具栈

| 工具 | 作用 |
|---|---|
| [Ghostty](https://ghostty.org/) | GPU 加速的现代终端模拟器 |
| [Zoxide](https://github.com/ajeetdsouza/zoxide) | 智能目录跳转（cd 的替代） |
| [Yazi](https://yazi-rs.github.io/) | 极速终端文件管理器 |
| [Oh-My-Zsh](https://ohmyzsh.sh/) | Zsh 配置 + 主题 + 插件框架 |

## 📚 文档

- **[terminal-setup.md](./terminal-setup.md)** — 完整安装与配置指南（含全部配置文件内容）
- **[usage-guide.md](./usage-guide.md)** — 使用手册：快捷键速查、入门建议、工作流示例、FAQ

## 🚀 快速开始

```bash
# 1. 安装工具
brew install ghostty zoxide yazi ffmpegthumbnailer poppler

# 2. 安装 Oh-My-Zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# 3. 安装 Zsh 插件
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git \
  ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
git clone https://github.com/zsh-users/zsh-autosuggestions \
  ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

# 4. 复制配置文件（参考 terminal-setup.md 中各文件内容）
mkdir -p ~/.config/ghostty ~/.config/yazi
# 然后把 terminal-setup.md 里的配置块分别写入：
#   ~/.config/ghostty/config
#   ~/.config/yazi/{yazi,keymap,theme}.toml
#   ~/.zshrc

# 5. 重载
source ~/.zshrc
```

## 💡 核心体验

```bash
z proj          # 模糊跳转到含 "proj" 的目录
y               # 启动 yazi 浏览文件，退出后 shell 自动 cd
gst             # = git status（oh-my-zsh git 别名）
Ctrl+`          # 全局唤出 Quake 下拉终端
```

更多用法见 [usage-guide.md](./usage-guide.md)。

## ⚠️ 注意事项

1. **Nerd Font 必装**：agnoster 主题与 yazi 图标需要，推荐 `font-maple-mono-nf-cn` 或 `font-jetbrains-mono-nerd-font`。
2. **Yazi 26.x schema**：本仓库配置已适配新版（`fetchers` 用 `url` + `group`，`filetype` fallback 用 `url`）。旧版 yazi 需回退字段名。
3. **Zoxide 冷启动**：刚装时数据库为空，前几天先用 `cd` 攒历史，之后 `z` 才能精准命中。

## 📄 License

MIT
