# Visual Studio Code

快捷键 | 功能
-----  | -----
`F11` | 全屏
`Ctrl + F2` | 全选当前选中文本
`Shift + Alt + Right Arrow` | 选中括号或引号之间的内容

## Bash 配置

### Git Bash 配置

```json
{
  "terminal.integrated.shell.windows": "D:\\Git\\bin\\bash.exe",
  "terminal.integrated.shellArgs.windows": [
    "--login",
    "-i"
  ],
}
```

### zsh 配置

VSCode 设置参数，注意 zsh 启动时不要设置默认路径，设置后 VSCode 不能进入当前文件夹下。zsh 的安装步骤在 windows 一节中。

```json
{
    "terminal.integrated.shell.windows": "C:\\Windows\\sysnative\\bash.exe"
}
```

## 参考

- [Key Bindings for Visual Studio Code](https://code.visualstudio.com/docs/customization/keybindings)
