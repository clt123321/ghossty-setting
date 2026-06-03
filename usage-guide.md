# 🎯 Ghostty 终端套件 — 使用指南

> 配套配置：Ghostty + Zoxide + Yazi + Oh-My-Zsh
> 适合刚配好环境、想快速上手的同学

## 目录

- [入门建议](#入门建议)
- [Ghostty 终端](#ghostty-终端)
- [Oh-My-Zsh](#oh-my-zsh)
- [Zoxide 智能跳转](#zoxide-智能跳转)
- [Yazi 文件管理器](#yazi-文件管理器)
- [三件套联动工作流](#三件套联动工作流)
- [常见问题 FAQ](#常见问题-faq)

---

## 入门建议

**第一周目标**：把肌肉记忆从 `cd` 切换到 `z`，从 Finder 切换到 `y`。

按这个顺序逐步上手，避免一次塞太多键位：

1. **Day 1-2**：先用 Ghostty 跑日常命令，熟悉 `Cmd+T` 新标签、`Cmd+D` 分屏、`` Ctrl+` `` 呼出 Quake 终端。
2. **Day 3-4**：开始用 `z 关键词` 替代 `cd`，每天 cd 至少 5 个不同目录给 zoxide 攒数据。
3. **Day 5-7**：用 `y` 进 yazi 管理文件，强迫自己不开 Finder。先掌握 `hjkl` + `Enter` + `q` 三件事就够了。
4. **第二周**：开始组合用 `gst`/`gco` 等 git 别名，让 zsh-autosuggestions 帮你写命令。

> 💡 **关键认知**：这套工具的价值在"键盘流"，鼠标越少越快。

---

## Ghostty 终端

GPU 加速的现代终端模拟器，配置简洁、速度极快。

### 标签页与分屏

| 快捷键 | 功能 |
|---|---|
| `Cmd+T` | 新建标签页 |
| `Cmd+W` | 关闭当前标签/分屏 |
| `Cmd+Shift+←` / `→` | 上一个 / 下一个标签 |
| `Cmd+D` | 右侧分屏 |
| `Cmd+Shift+D` | 下方分屏 |
| `Cmd+Alt+方向键` | 在分屏间跳转 |
| `Cmd+Shift+E` | 均分所有分屏 |
| `Cmd+Shift+F` | 当前分屏全屏切换 |

### Quake 模式（杀手锏）

`` Ctrl+` ``（Control + 反引号）= 全局热键，从屏幕顶部下拉一个终端，再次按下隐藏。**任何 App 焦点下都能用**，临时跑命令再方便不过。

### 字体与配置

| 快捷键 | 功能 |
|---|---|
| `Cmd +` / `Cmd -` / `Cmd 0` | 字体放大 / 缩小 / 重置 |
| `Cmd+Shift+,` | 重新加载配置（无需重启） |

要改主题？`ghostty +list-themes` 看全部，编辑 `~/.config/ghostty/config` 的 `theme = xxx` 即可。

---

## Oh-My-Zsh

Zsh 的"操作系统"，给原本朴素的 shell 装上主题、插件、补全、历史搜索。

### 已启用的插件

#### 1. `git` — 上百个 git 别名

最常用的：

| 别名 | 等价命令 |
|---|---|
| `gst` | `git status` |
| `gco <branch>` | `git checkout <branch>` |
| `gcb <branch>` | `git checkout -b <branch>` |
| `ga <file>` | `git add <file>` |
| `gaa` | `git add --all` |
| `gcmsg "msg"` | `git commit -m "msg"` |
| `gp` | `git push` |
| `gl` | `git pull` |
| `gd` | `git diff` |
| `glog` | 带图的彩色 log |
| `gba` | `git branch -a` |

> 输入 `alias | grep '^g'` 查看全部 git 别名。

#### 2. `zsh-syntax-highlighting` — 实时语法着色

- 命令存在 → 绿色
- 命令不存在 → 红色
- 字符串引号未闭合 → 红色
- 选项参数 → 不同颜色

**作用**：还没回车就知道有没有打错。

#### 3. `zsh-autosuggestions` — 历史智能补全

灰字提示根据历史记录预测的命令：

- `→` 或 `End` → 接受全部建议
- `Ctrl+→` → 按词接受（更细粒度）
- `Esc` → 忽略

### Agnoster 主题状态栏

```
user@host  ~/path  master ✚ ●
                   └─分支 └─有改动 └─有 stash
```

行末符号：
- `✓` 上条命令成功
- `✘` 上条命令失败（带返回码）

### 历史搜索

| 快捷键 | 功能 |
|---|---|
| `Ctrl+R` | 反向搜索历史命令（再按继续找下一个） |
| `↑` / `↓` | 在历史命令中翻页 |
| `!!` | 重复上条命令（如 `sudo !!`） |
| `!$` | 上条命令最后一个参数 |

---

## Zoxide 智能跳转

> 一句话：**记住你 cd 过哪、cd 多频繁，让你用关键词秒切目录。**

### 核心命令

| 命令 | 功能 |
|---|---|
| `z foo` | 跳转到含 "foo" 的最常用目录 |
| `z foo bar` | 跳转到同时含 "foo" 和 "bar" 的目录 |
| `z foo/` | 末尾加 `/` 强制目录补全 |
| `z -` | 回上一个目录 |
| `zi` | 交互式选择（fzf 风格） |
| `zoxide query --list` | 查看所有记录的目录及评分 |
| `zoxide --version` | 查看版本（注意不是 `z --version`） |

### 关键认知

- **冷启动期**：刚装时数据库为空，`z xxx` 必然失败。**前 3 天请用 `cd`**，让 zoxide 攒数据。
- **匹配规则**：用了"频率 × 时间衰减"算法（叫 frecency），最近常去的优先级最高。
- **自动学习**：每次 `cd` 都会自动记录，无需主动操作。

### 实战例子

```bash
cd ~/Desktop/explore_project/quant_project   # 第 1 次 cd
cd ~/Desktop                                 # 切走
z quant       # ← 一秒切回 quant_project
z exp poxiao  # 多关键字定位 explore_project/poxiao
```

---

## Yazi 文件管理器

终端版 Finder，三栏布局（父目录 / 当前 / 预览），Vim 键位，预览图片/视频/PDF/代码。

### 启动与退出

```bash
y      # 启动（注意是 y，不是 yazi，y 是封装函数）
q      # 退出，shell 自动 cd 到 yazi 最后所在目录
```

> 为什么是 `y`？因为 `.zshrc` 里定义了 `y()` 函数，让退出时能 cd 跟随。直接 `yazi` 不会跟随。

### 移动光标

| 键 | 功能 |
|---|---|
| `h` `j` `k` `l` | 左 下 上 右 |
| `gg` / `G` | 顶部 / 底部 |
| `Ctrl+u` / `Ctrl+d` | 上/下翻半屏 |
| `Enter` | 进入目录 / 用默认程序打开文件 |
| `Backspace` | 返回上级 |

### 文件操作

| 键 | 功能 |
|---|---|
| `Space` | 选中切换（多选） |
| `v` | 进入可视模式批量选择 |
| `Ctrl+a` | 全选 |
| `Esc` | 取消选择 |
| `y` | 复制 |
| `x` | 剪切 |
| `p` | 粘贴 |
| `P` | 强制覆盖粘贴 |
| `d` | 删除到回收站 |
| `D` | 永久删除（**不可恢复**） |
| `a` | 新建文件（结尾加 `/` 是目录） |
| `r` | 重命名 |
| `;` | 在选中文件上跑 shell 命令 |

### 查找与跳转

| 键 | 功能 |
|---|---|
| `/` | 在当前目录搜索 |
| `n` / `N` | 下一个/上一个搜索结果 |
| `f` | 按文件名过滤 |
| `s` | 排序菜单 |
| `z` | **调用 zoxide 跳转**（强强联合！） |
| `Z` | 用 fzf 模糊查找 |
| `cd` | 输入路径跳转 |

### 自定义快捷跳转（已配置）

| 键 | 目录 |
|---|---|
| `gh` | `~`（home） |
| `gc` | `~/.config` |
| `gd` | `~/Downloads` |
| `gw` | `~/work` |
| `gD` | `~/Desktop` |
| `gt` | `/tmp` |

### 视图与预览

| 键 | 功能 |
|---|---|
| `.` | 显示/隐藏隐藏文件 |
| `Tab` | 切换到预览面板 |
| `T` | 显示当前文件类型 |
| `o` | 用 opener（默认程序）打开 |
| `O` | 选择 opener 打开 |

预览支持：图片直渲、PDF、视频缩略图（需 ffmpegthumbnailer）、代码语法高亮、压缩包内容。

### 退出

| 键 | 功能 |
|---|---|
| `q` | 退出（shell 跟随 cd） |
| `Q` | 退出但不跟随 cd |

---

## 三件套联动工作流

### 场景 1：快速进项目改代码

```bash
z myproj          # zoxide 秒切到项目
gst               # oh-my-zsh git 别名查状态
y                 # 进 yazi 找文件
# 在 yazi 里按 Enter 用 VSCode 打开
q                 # 退出 yazi
```

### 场景 2：在多个目录间跳来跳去

```bash
# 拆两个分屏（Cmd+D）
# 左屏：
z backend && npm run dev
# 右屏：
z frontend && npm run dev
```

### 场景 3：临时跑个命令

```
# 任何 App 焦点下按 Ctrl+`
# 弹出 Quake 终端
z target          # 切到目标目录
# 跑命令...
# 再按 Ctrl+` 隐藏
```

### 场景 4：在 yazi 内用 zoxide

进入 yazi 后按 `z`，输入关键词，立即跳转到目标目录继续浏览，比 Finder 快 10 倍。

---

## 常见问题 FAQ

### Q1: `z --version` 报错 "no match found"？

**这不是 bug**。`z` 是 zoxide 的跳转命令，`z xxx` 是"跳到含 xxx 的目录"。
查版本请用：

```bash
zoxide --version
```

### Q2: agnoster 主题显示乱码（` ` 之类的方块）？

缺 Nerd Font。安装：

```bash
brew install --cask font-maple-mono-nf-cn
# 或
brew install --cask font-jetbrains-mono-nerd-font
```

然后修改 `~/.config/ghostty/config` 的 `font-family`。

### Q3: `z xxx` 总是说找不到？

zoxide 数据库没数据。**前 3-7 天先用 `cd` 攒历史**，之后才会有效果。
查看当前历史：`zoxide query --list`

### Q4: yazi 启动后 `q` 退出，但目录没跟随切换？

确保你是用 `y`（小写）启动的，不是 `yazi`。
`y` 是 `.zshrc` 里定义的 wrapper 函数，会读取 yazi 写出的 cwd 文件再 cd。

### Q5: yazi 报 "missing field group" 之类的 TOML 错误？

Yazi 26.x 起 schema 变了。请确保：

- `prepend_fetchers` 用 `url` 而不是 `name`，且必须有 `group = "mgr"`
- `filetype.rules` fallback 用 `url = "*"` 而不是 `name = "*"`

本仓库的配置已适配新版。

### Q6: 想加自己的别名/函数怎么办？

编辑 `~/.zshrc`，在文件末尾加。例如：

```bash
alias ll='ls -lah'
alias k='kubectl'

# 自定义函数
mkcd() { mkdir -p "$1" && cd "$1"; }
```

然后 `source ~/.zshrc` 或重开终端。

### Q7: 配置改坏了想还原？

我们在安装时备份过 `.zshrc`：

```bash
ls ~/.zshrc.bak.*       # 看备份
cp ~/.zshrc.bak.XXXXX ~/.zshrc   # 还原
```

---

## 进阶资源

- [Ghostty 官方文档](https://ghostty.org/docs)
- [Yazi 官方文档](https://yazi-rs.github.io/docs/installation)
- [Zoxide GitHub](https://github.com/ajeetdsouza/zoxide)
- [Oh-My-Zsh 插件列表](https://github.com/ohmyzsh/ohmyzsh/wiki/Plugins)

---

**Happy Hacking! 🚀**
