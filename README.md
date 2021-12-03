# git-setup

本工具会全自动设定 Git 版控环境，并且跨平台支援 Windows, Linux, macOS 等作业系统的命令列环境，尤其针对中文环境经常会出现乱码的问题都会完整的解决。

## 先决条件

- [Node.js](https://nodejs.org/en/) 10.13.0 以上版本
- [Git](https://git-scm.com/) 任意版本 (建议升级到最新版)

## 使用方式

```sh
npx @jiahe/git-setup
```

- 设定过程会询问你的 `user.name` 与 `user.email` 资讯
- Email 会进行格式验证，格式错误会拒绝设定下去
- 所有 Git 设定都会以 `--global` 为主 (`~/.gitconfig`)
- Windows 平台会自动设定 `LC_ALL` 与 `LANG` 使用者环境变数
- Linux, macOS 平台会提醒进行设定

## 设定内容

```sh
git config --global user.name  ${name}
git config --global user.email  ${email}

# 设定打错命令时 3 秒内会自动做出判断
git config --global help.autocorrect 30

# 现在大多编辑器都已经能正确处理 CRLF 字元，不再需要自动转换了！
git config --global core.autocrlf false

# 为了能正确显示 UTF-8 中文字
git config --global core.quotepath false

# 在命令列环境下自动标示颜色
git config --global color.diff auto
git config --global color.status auto
git config --global color.branch auto

# 常用的 Git Alias 命令
git config --global alias.ci   commit
git config --global alias.cm   "commit --amend -C HEAD"
git config --global alias.co   checkout
git config --global alias.st   status
git config --global alias.sts  "status -s"
git config --global alias.br   branch
git config --global alias.re   remote
git config --global alias.di   diff
git config --global alias.type "cat-file -t"
git config --global alias.dump "cat-file -p"
git config --global alias.lo   "log --oneline"
git config --global alias.ls   "log --show-signature"
git config --global alias.ll   "log --pretty=format:'%h %ad | %s%d [%Cgreen%an%Creset]' --graph --date=short"
git config --global alias.lg   "log --graph --pretty=format:'%Cred%h%Creset %ad |%C(yellow)%d%Creset %s %Cgreen(%cr)%Creset [%Cgreen%an%Creset]' --abbrev-commit --date=short"
git config --gloabl alias.sbtime !"for k in `git branch|perl -pe s/^..//`;do echo `git show --pretty=format:\"%Cgreen%ci %Cblue%cr%Creset\" $k|head -n 1`\\\t$k;done|sort"
git config --gloabl alias.sbrtime !"for k in `git branch -r|perl -pe s/^..//`;do echo `git show --pretty=format:\"%Cgreen%ci %Cblue%cr%Creset\" $k|head -n 1`\\\t$k;done|sort"
git config --global alias.alias "config --get-regexp ^alias\."

# 必须是 Windows 平台才会执行以下设定
git config --global alias.ignore '!gi() { curl -sL https://www.gitignore.io/api/$@ ;}; gi'
git config --global alias.iac '!giac() { git init && git add . && git commit -m 'Initial commit' ;}; giac'

# 必须是 Linux/macOS 平台才会执行以下设定
git config --global alias.ignore '!'"gi() { curl -sL https://www.gitignore.io/api/\$@ ;}; gi"
git config --global alias.iac '!'"giac() { git init && git add . && git commit -m 'Initial commit' ;}; giac"


# 必须是 Windows 平台且有安装 TortoiseGit 才会设定 tlog 这个 alias
git config --global alias.tlog "!start 'C:\\PROGRA~1\\TortoiseGit\\bin\\TortoiseGitProc.exe' /command:log /path:."

# 必须是 Windows 平台才会将预设编辑器设定为 notepad
git config --global core.editor notepad
```

## 提供建议

如果您对本工具有任何想法，欢迎到[这里](https://github.com/iamxiaojianzheng/git-setup/issues)留言讨论！
