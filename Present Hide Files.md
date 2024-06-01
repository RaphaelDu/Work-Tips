# 在 macOS 上显示隐藏文件

在 macOS 上显示隐藏文件（包括 .git 等以点开头的文件夹），你可以使用以下几种方法：

## 1 使用键盘快捷键：

在 Finder 中，同时按下 Command + Shift + . (点)键，即可快速显示或隐藏隐藏文件。

## 2 通过终端命令临时显示隐藏文件：

打开"终端"（Terminal）应用程序。
输入以下命令并按回车键：
```bash
Copy codedefaults write com.apple.finder AppleShowAllFiles TRUE
```
然后输入以下命令并按回车键，以重启 Finder：
```bash
Copy codekillall Finder
```
隐藏文件将在 Finder 中可见。如果要再次隐藏文件，可以将上述命令中的 TRUE 替换为 FALSE。


