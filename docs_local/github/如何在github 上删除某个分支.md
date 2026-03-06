删除GitHub上的远程分支：

方法1：Git命令（推荐）

# 删除远程分支
git push origin --delete 分支名

# 例如删除dev分支
git push origin --delete dev
方法2：GitHub网页
进入仓库页面
点击 branches（分支列表）
找到要删除的分支
点击右侧的垃圾桶图标🗑️
<thinking> 用户可能还需要知道如何删除本地分支，以及删除后如何清理本地的远程跟踪分支。我应该补充这些信息。 </thinking>
同时删除本地分支

# 删除本地分支（需要先切换到其他分支）
git checkout main
git branch -d 分支名

# 强制删除（如果有未合并的更改）
git branch -D 分支名
清理本地的远程跟踪分支

# 删除远程分支后，清理本地的过期引用
git fetch --prune
完整流程示例：


# 1. 切换到main分支
git checkout main

# 2. 删除远程分支
git push origin --delete dev

# 3. 删除本地分支
git branch -d dev

# 4. 清理过期引用
git fetch --prune