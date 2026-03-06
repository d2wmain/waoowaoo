1. 重新配置远程仓库

# 修改origin指向你的fork（替换"你的用户名"）
git remote set-url origin https://github.com/你的用户名/waoowaoo.git

# 添加upstream指向原项目
git remote add upstream https://github.com/saturndec/waoowaoo.git

# 验证配置
git remote -v
<thinking> 用户需要看到验证后应该显示什么，这样他们可以确认配置正确。 </thinking>
验证后应该看到：


origin    https://github.com/你的用户名/waoowaoo.git (fetch)
origin    https://github.com/你的用户名/waoowaoo.git (push)
upstream  https://github.com/saturndec/waoowaoo.git (fetch)
upstream  https://github.com/saturndec/waoowaoo.git (push)
2. 创建开发分支

# 确保在main分支
git checkout main

# 创建并切换到开发分支
git checkout -b custom
3. 开始你的改动

# 现在可以修改代码了
# 修改完成后提交：
git add .
git commit -m "你的提交说明"

# 推送到你的fork
git push origin custom
4. 日常同步上游更新

#拉取上游更新
git checkout main
git fetch upstream
git merge upstream/main
git push origin main

# 合并到你的开发分支
git checkout custom
git merge main
git push origin custom
就这样，配置完成后就可以开始工作了。


---

拉取上游更新可以切换到main 之后直接用Git pull 吗？

不完全可以。git pull默认从origin拉取，而你需要从upstream（原项目）拉取。

区别：


# ❌ 这个会从你的fork拉取（不是原项目）
git pull

# ✅ 这个才是从原项目拉取
git pull upstream main
简化命令（推荐）：

<thinking> 用户想要更简单的命令。我可以提供两种方案： 1. 直接用`git pull upstream main`一步完成 2. 或者配置main分支跟踪upstream
方案1更简单直接，方案2会改变默认行为，可能不太适合。

我应该推荐方案1，并解释为什么分两步（fetch + merge）更安全。
</thinking>


# 切换到main分支
git checkout main

# 一步完成：拉取并合并上游更新
git pull upstream main

# 推送到你的fork
git push origin main
为什么我之前建议分两步？


git fetch upstream      # 只下载，不合并（安全）
git merge upstream/main # 手动合并（可以先检查）
分两步的好处：

fetch后可以先用git log upstream/main查看更新内容
确认没问题再merge
更安全，适合重要更新
但如果你想简单快速，直接用：


git pull upstream main
效果是一样的，只是少了中间检查的机会。


---

现在你可以：


# 创建你的开发分支
git checkout -b custom

# 开始你的改动
# 修改代码...

# 提交修改
git add .
git commit -m "你的修改说明"

# 推送到你的fork
git push origin custo