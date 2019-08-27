# Visual Studio Code

## 常用快捷键

以下是 Winidows 上的.

快捷键 | 功能
-----  | -----
`Ctrl + X` | 打开 Extensions
`Ctrl + Shift + G G` | 打开 Source Control
`Ctrl + Shift + E` | 打开 Explorer
`F11` | 全屏
`Ctrl + F2` | 全选当前选中文本
`Shift + Alt + Right Arrow` | 选中括号或引号之间的内容
`Ctrl + K W` | 关闭全部编辑窗口

## 配置

```json
{
  "files.eol": "\n",
  "editor.tabSize": 2,
  "editor.insertSpaces": true,
  "editor.wordWrap": "on",
  "files.autoSave":"afterDelay",
  "files.autoSaveDelay": 200,
  "editor.detectIndentation": false,
  "terminal.integrated.shell.windows": "C:\\Windows\\System32\\wsl.exe",
  "workbench.colorTheme": "One Dark Pro Vivid",
  "editor.fontFamily": "Fira Code, Consolas, Noto Sans CJK SC, 'Courier New', monospace",
  "workbench.activityBar.visible": false
}
```

## Bash 配置: 选择配置你需要的 Bash

**Git Bash**

```json
{
  "terminal.integrated.shell.windows": "D:\\Git\\bin\\bash.exe",
  "terminal.integrated.shellArgs.windows": [
    "--login",
    "-i"
  ],
}
```

**WSL** 如果用的 Windows 内嵌 Linux，配置如下

```json
{
    "git.path": "D:\\apps\\Git\\bin\\git.exe",
    "terminal.integrated.shell.windows": "C:\\WINDOWS\\System32\\wsl.exe",
}
```

**zsh** VSCode 设置参数，注意 zsh 启动时不要设置默认路径(启动时进入)，设置后 VSCode 不能进入当前文件夹下。zsh 的安装步骤在 windows 一节中。

```json
{
    "terminal.integrated.shell.windows": "C:\\Windows\\sysnative\\bash.exe"
}
```

## 常用插件

* Markdown 校验：markdownlint。编辑时提示不符合规范的写法
* Remote: Remote - SSH, Remote - WSL, Remote - Containers.
* ESLint
* npm
* npm Intellisense
* Path Intellisense
* EditorConfig for VS Code

```bash
# 在当前窗口打开工程(覆盖已经打开的窗口)
code -r folder

# install extension
code --install-extension

# uninstall extension
code --uninstall-extension
```

## PlantUML

```bash
# 安装扩展
code --install-extension jebbs.plantuml

# (可选) 安装 graphviz, 某些图形需要
# http://graphviz.org/download/
# Windows 下载安装 msi 文件
brew install graphviz # macOS
apt install graphviz  # Ubuntu
```

## 参考

* [Key Bindings for Visual Studio Code](https://code.visualstudio.com/docs/customization/keybindings)
