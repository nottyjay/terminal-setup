# 🖥️ terminal-setup

一键配置 macOS 终端环境。新 Mac 跑一个脚本，几分钟搞定完整终端。

**🇬🇧 [English Version](README.md)**

<p align="center">
  <img src="assets/ghostty.png" width="80" alt="Ghostty">
  &nbsp;&nbsp;
  <img src="assets/fish.png" width="80" alt="Fish Shell">
  &nbsp;&nbsp;
  <img src="assets/zsh.png" width="80" alt="Zsh">
  &nbsp;&nbsp;
  <img src="assets/starship.png" width="80" alt="Starship">
</p>

<p align="center">
  <img src="assets/demo-2x.gif" width="600" alt="Demo">
</p>

## 快速开始

```bash
git clone https://github.com/lewislulu/terminal-setup.git
cd terminal-setup && ./setup.sh
```

脚本会让你选 Fish 还是 Zsh。也可以直接指定：

```bash
./setup.sh --fish    # Fish shell
./setup.sh --zsh     # Zsh + 类 Fish 插件
```

一行命令（自动 clone）：

```bash
bash <(curl -fsSL https://raw.githubusercontent.com/lewislulu/terminal-setup/main/setup.sh)
```

## 选择你的 Shell

| | 🐟 Fish | 🐚 Zsh |
|---|---------|---------|
| **POSIX 兼容** | ❌ 自有语法 | ✅ 兼容 |
| **自动补全建议** | ✅ 内置 | ✅ 通过插件 |
| **语法高亮** | ✅ 内置 | ✅ 通过插件 |
| **Node 管理** | fnm（共享） | fnm（共享） |
| **配置文件** | `~/.config/fish/config.fish` | `~/.zshrc` |
| **适合** | 开箱即用，省心 | 写脚本，POSIX 兼容 |

## 工具栈

| 组件 | 说明 |
|------|------|
| **[Ghostty](https://ghostty.org)** | GPU 加速终端模拟器 |
| **Fish** 或 **Zsh** | Shell（你选） |
| **[Starship](https://starship.rs)** | 跨 Shell 提示符（Catppuccin Mocha 主题） |
| **MesloLGS NF** | Nerd Font，提供图标和 Powerline 字形 |
| **[bat](https://github.com/sharkdp/bat)** | 带语法高亮和行号的 `cat` |
| **[eza](https://github.com/eza-community/eza)** | 带图标、git 状态、树形视图的 `ls` |
| **[fd](https://github.com/sharkdp/fd)** | 更快更直观的 `find` |
| **[ripgrep](https://github.com/BurntSushi/ripgrep)** | 比 `grep` 快几个数量级 |
| **[fzf](https://github.com/junegunn/fzf)** | 模糊查找器（Ctrl+R / Ctrl+T / Alt+C） |
| **[btop](https://github.com/aristocratos/btop)** | 漂亮的系统监控 |
| **[zoxide](https://github.com/ajeetdsouza/zoxide)** | 智能 `cd`，学习你的习惯 |
| **[jq](https://github.com/jqlang/jq)** | JSON 处理器 |
| **[tldr](https://github.com/tldr-pages/tldr)** | 简化版 man 手册，附带示例 |
| **[delta](https://github.com/dandavison/delta)** | 带语法高亮的 git diff |
| **[lazygit](https://github.com/jesseduffield/lazygit)** | Git 终端 UI |
| **[fnm](https://github.com/Schniz/fnm)** | 快速 Node 版本管理器（Rust 编写） |

## 脚本做了什么

1. 安装 **Homebrew**（如需要）
2. 安装 **Ghostty** 终端
3. 下载 **MesloLGS NF** Nerd 字体
4. 安装你选择的 **Shell** + 插件
5. 通过 Homebrew 安装所有 **CLI 工具**（包括 fzf）
6. 安装 **Starship** 提示符 + Catppuccin Mocha 配置
7. 安装 **fnm** + **Node.js** LTS
8. 部署所有配置文件（已有配置会加时间戳备份）

## 别名 / 缩写

| 快捷方式 | 展开为 |
|----------|--------|
| `ls` | `eza --icons --group-directories-first` |
| `ll` | `eza -la --icons --group-directories-first` |
| `lt` | `eza --tree --icons --level=2` |
| `cat` | `bat` |
| `find` | `fd` |
| `grep` | `rg` |
| `top` | `btop` |
| `lg` | `lazygit` |

## fzf 快捷键

| 按键 | 功能 |
|------|------|
| `Ctrl+R` | 模糊搜索命令历史 |
| `Ctrl+T` | 模糊查找文件（用 `fd` 作为后端） |
| `Alt+C` | 模糊进入目录 |

## fnm — Node 版本管理

```bash
fnm install 22            # 安装 Node 22
fnm install --lts         # 安装最新 LTS
fnm default 22            # 设置默认版本
fnm use 22                # 当前 shell 切换
echo "22" > .node-version # 进入目录自动切换
```

## SSH Key 切换

两种 Shell 配置都内置了 `set-ssh-key` 函数：

```bash
set-ssh-key my-key-name     # 清空 agent，加载 ~/.ssh/my-key-name
set-ssh-key                  # key 不存在时列出所有可用 key
```

> **最佳实践：** 推荐在 `~/.ssh/config` 里用 `Host` 别名 + `IdentitiesOnly yes` 实现自动匹配。`set-ssh-key` 是兜底方案。

---

## 技术选型说明

### 为什么选 Ghostty？

GPU 加速、原生 macOS 应用、启动快、配置格式干净。iTerm2 做了太多事情导致臃肿，Ghostty 走的是现代极简路线。项目还年轻但发展很快。

### 为什么选 Starship 而不是 Powerlevel10k？

- **跨 Shell：** 同一份配置文件 Fish 和 Zsh 都能用。p10k 只支持 Zsh。
- **TOML 配置：** 声明式、可读性强。p10k 的配置是向导生成的一大堆代码。
- **Rust 二进制：** 快速，不依赖任何 Shell 框架。
- **Catppuccin 主题：** 和整个工具栈风格统一。

如果你只用 Zsh 且追求极致 prompt 速度，p10k 的 instant prompt 确实更快。但 Starship 够快了，而且通用性更好。

### 为什么同时提供 Fish 和 Zsh？

不同人有不同需求：

- **Fish：** 最佳开箱体验。自动补全、语法高亮、补全全内置，零配置。但它不兼容 POSIX，`bash` 脚本不能直接跑，有些工具假设你用 POSIX shell。
- **Zsh：** POSIX 兼容，所有 bash 脚本和一行命令都能用。装上插件（autosuggestions + syntax-highlighting）后能达到 Fish 90% 的体验。代价：依赖更多组件。

如果你经常需要跑别人的脚本 → **Zsh**。
如果你追求最干净的 Shell 体验，不介意偶尔 `bash script.sh` → **Fish**。

### 为什么 Zsh 插件用 Homebrew 装？不用 zinit/antidote/sheldon？

总共只有 3 个 Zsh 插件：`zsh-autosuggestions`、`zsh-syntax-highlighting`、`zsh-completions`。

3 个插件用插件管理器是杀鸡用牛刀：

- **zinit：** 原作者弃坑了。社区 fork（zdharma-continuum）在维护，但加了一层复杂度却没有任何收益。Turbo mode 和 ice modifiers 很强大但我们完全用不上。
- **antidote/sheldon：** 好工具，但还是多了一层。多一层就多一个出问题的点。
- **Oh My Zsh：** 是框架不是插件管理器。启动时加载 100+ 文件，慢。
- **Homebrew：** 本来就装了，`brew install` + `.zshrc` 里一行 `source`。更新跟着 `brew upgrade` 走。零额外依赖。

**经验法则：** 插件 < 5 个 → Homebrew 直装。插件 10+ 个 → 考虑 antidote 或 sheldon。

### 为什么选 fnm 而不是 nvm？

| | fnm | nvm |
|---|-----|-----|
| **语言** | Rust | Bash |
| **Shell 启动耗时** | ~1ms | ~200-400ms（或者搞懒加载 hack） |
| **Fish 支持** | ✅ 原生 | ❌ 需要 nvm.fish（社区项目） |
| **Zsh 支持** | ✅ 原生 | ✅ 原生 |
| **自动切换** | ✅ `--use-on-cd`（读 `.node-version`、`.nvmrc`） | ⚠️ 需要额外 hook 脚本 |
| **安装方式** | `brew install fnm` | curl 脚本，会修改 shell rc 文件 |
| **跨 Shell 共享** | ✅ Fish 和 Zsh 共用同一份 Node 安装 | ❌ nvm.fish 和 nvm-sh 存储路径不同 |

核心原因：
1. **速度：** nvm 让 Shell 启动慢 200-400ms。fnm 只加 ~1ms。频繁开终端的人能明显感知。
2. **统一：** 一个工具、一个 Node 安装位置（`~/.local/share/fnm/`），Fish 和 Zsh 用法完全一样。用 nvm 的话，Zsh 要 nvm-sh、Fish 要 nvm.fish——两个不同的工具，存储路径也不兼容。
3. **自动切换：** `fnm env --use-on-cd` 读取项目里的 `.node-version` 或 `.nvmrc`，`cd` 进去自动切版本。不需要额外配置。
4. **nvm.fish 是社区项目**，不是官方 nvm。能用但有自己的怪癖（要配 `nvm_data` 路径、`set --universal nvm_default_version` 等）。

如果你项目里已经有 `.nvmrc` 文件，fnm 可以直接读——完全兼容。

### 为什么选 MesloLGS NF？

- 专为终端设计（等宽、小字号清晰）
- 包含所有 Nerd Font 字形（图标、Powerline、Devicons）
- Powerlevel10k 同款字体——在终端里经过大量实战测试
- 有 Regular/Bold/Italic/Bold Italic 四种字重

替代选择：JetBrains Mono Nerd Font、Fira Code Nerd Font，都不错。MesloLGS 兼容性最广。

### 为什么用 git-delta？

Git 默认 diff 能用但太丑。Delta 加了：
- diff 内语法高亮
- 行号
- 并排对比视图
- 精确到单词的变更高亮
- `n`/`N` 在文件间导航

全局配置——`git diff`、`git log -p`、`git show` 等全部生效。行为不变，只是输出更好看。

### 为什么用 zoxide 而不是原生 cd？

zoxide 学习你最常去的目录。用几天后：

```bash
z proj      # 跳转到 ~/projects（或者你最常访问的包含 "proj" 的路径）
z doc       # 跳转到 ~/Documents
zi          # 配合 fzf 交互式选择
```

带脑子的 `cd`。直接输入完整路径也照常工作。

### 为什么用 fzf？

你能装的最有影响力的 CLI 工具：

- **Ctrl+R：** 模糊搜索命令历史（替代默认的反向搜索）
- **Ctrl+T：** 按文件名模糊查找
- **Alt+C：** 模糊进入任意目录
- 自动集成 `fd`（比 `find` 快，自动忽略 `.gitignore`）

用一周就回不去了。

## License

MIT
