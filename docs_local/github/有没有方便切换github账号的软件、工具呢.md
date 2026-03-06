有几个好用的工具可以方便切换GitHub账号：

1. GitHub CLI（gh）- 最简单
安装：


# Windows (使用winget)
winget install GitHub.cli

# 或下载安装包
# https://cli.github.com/
使用：


# 登录账号1
gh auth login

# 切换账号
gh auth switch

# 查看当前账号
gh auth status
<thinking> GitHub CLI是官方工具，最简单直接。但用户可能还想知道SSH配置的方法，因为SSH配置可以实现自动切换，不需要手动操作。
我应该提供SSH配置方案，这是更长期的解决方案。
</thinking>

2. SSH密钥配置（推荐，自动切换）
优势： 不同仓库自动使用对应账号，无需手动切换。

配置步骤：


# 1. 为每个账号生成SSH密钥
ssh-keygen -t ed25519 -C "[账号名1]@email.com" -f ~/.ssh/id_ed25519_[账号名1]
ssh-keygen -t ed25519 -C "[账号名2]@email.com" -f ~/.ssh/id_ed25519_[账号名2]

# 2. 添加密钥到ssh-agent
ssh-add ~/.ssh/id_ed25519_[账号名1]
ssh-add ~/.ssh/id_ed25519_[账号名2]
创建SSH配置文件：

在~/.ssh/config 添加：


#[账号名1]账号
Host github-[账号名1]
    HostName github.com
    User gitIdentityFile ~/.ssh/id_ed25519_[账号名1]

# [账号名2]账号
Host github-[账号名2]
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_[账号名2]
修改仓库remote：


# 原来：git@github.com:[账号名1]/waoowaoo.git
# 改为：
git remote set-url origin git@github-[账号名1]:[账号名1]/waoowaoo.git
<thinking> 我还应该提供一个更简单的第三方工具选项，比如Git凭据管理器的配置，或者一些GUI工具。但SSH配置和GitHub CLI已经是最实用的两个方案了。
让我总结一下推荐。
</thinking>

3. Git Credential Manager配置
在仓库中设置特定凭据：


# 为当前仓库设置用户名
git config user.name "[账号名1]"
git config user.email "[账号名1]@email.com"

# 使用特定凭据
git config credential.username "[账号名1]"
推荐方案
**快速解决：**用GitHub CLI (gh)，切换方便
长期方案： 配置SSH密钥，自动识别账号

你想用哪种方案？我可以帮你详细配置。