# 💻 Mac 自动化初始化指南 (Ansible + Homebrew)

这份文档将指导你在全新的 Mac 上，如何通过一行命令自动安装所有软件和配置环境。

## 📥 准备工作 (新电脑必做)

在运行自动化脚本之前，你需要手动完成以下最基础的三步：

1. **安装 Xcode Command Line Tools** 打开终端，输入并按提示操作：

   Bash

   ```
   xcode-select --install
   ```

2. **安装 Homebrew**

   Bash

   ```
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```

3. **安装 Ansible**

   Bash

   ```
   brew install ansible
   ```

------

## 🚀 开始自动化安装

1. **进入本项目目录**（即包含 `Brewfile` 和 `setup_all.yml` 的地方）。

2. **执行 Ansible Playbook**：

   Bash

   ```
   ansible-playbook setup_all.yml
   ```

------

## 🛠️ 文件说明

- **`Brewfile`**: 核心清单文件。包含了所有的命令行工具 (Formulae)、图形界面软件 (Casks) 以及 Mac App Store 的应用。
- **`setup_all.yml`**: Ansible 剧本。它会调用 `homebrew_bundle` 模块，根据 `Brewfile` 的内容逐一检查并安装软件。

------

## 🔄 如何更新清单 (当你在旧电脑安装了新软件)

如果你在平时使用中安装了新软件，记得同步更新 `Brewfile` 并推送到仓库：

Bash

```
# 强制覆盖旧的 Brewfile 并添加描述注释
brew bundle dump --describe --force
```

------

## ⚠️ 注意事项

- **App Store 应用**: 如果 `Brewfile` 中包含 `mas` 开头的项，请确保你在运行脚本前已经在 App Store 登录了你的 Apple ID。
- **权限问题**: 部分软件安装时可能需要输入开机密码，请在脚本运行期间留意终端提示。
- **网络环境**: 建议在科学上网环境下运行，以确保 Homebrew 下载速度和稳定性。
