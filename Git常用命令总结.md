## Zzz. Git常用命令

### z.1 代码仓库

#### z.1.1 创建仓库

1. 进入需要创建代码库的文件夹

   `cd 文件路径`

2. 创建/初始化仓库

   `git init`

3. 拉取远程仓库到本地（**建议使用**）

   `git clone`

#### z.1.2 添加文件到仓库

1. 添加文件到暂存区

   * 添加单个文件

     `git add 文件名`

   * 添加所有文件

     `git add .`

   *添加的过程中需注意以下两点*

   * .gitignore中指定的文件会被忽略
   * 空目录不会添加

2. 提交到本地仓库

   `git commit` 填写 `commit message` 并保存

   不建议使用`git commit -m "commit message"`,建议提交遵循`commit meassge`规范

3. 查看工作区状态

   `git status`

4. 对比工作区文件变化

   `git diff`

   建议将`beyond compare`配置为`diff`工具，用于`diff`以及`merge`冲突

#### z.1.3 仓库配置

1. 配置全局用户名和邮箱

   个人开发机配置：

   * `git config --global user.name "[name]"`
     * 比如：git config --global **user.name** "shadowbrokerno1@126.com"
   * `git config --global user.email "[email address]"`

   配置当前用户：

   * `git config user.name "[name]"`
   * `git config user.email "[email address]"`

### z.2 代码版本 / 提交切换

**注：这里的版本均为本地仓库版本**

#### z.2.1 查看过去版本 / 提交

1. 提交详情

   `git log`

2. 提交简介

   `git log --pretty=oneline`

#### z.2.2 回退版本 / 提交

1. 回退到当前最新提交

   `git reset --hard HEAD`

2. 回退到上次提交

   `git reset --hard HEAD^`

3. 回退到上n次提交

   `git reset --hard HEAD~n`

4. 回退到某次提交

   `git reset --hard commit-id`

#### z.2.3 重返未来版本

1. 查看历史提交以及被回退的提交（查看所有分支的所有操作记录）

   `git reflog`

   **注意：该记录有时限，且只在本地**

2. 回到未来版本

   `git reset --hard commit-id`

#### z.2.4 撤销修改

1. 工作区文件撤销（没有提交到暂存区 / 没有 git add）

   撤销修改：`git checkout 文件名`

2. 暂存区文件撤销

   将暂存区文件撤销到工作区：`git reset  HEAD  文件不带--hard`

3. 提交到了版本库

   参见***回退版本 / 提交***

#### z.2.5 删除文件

1. 删除文件从版本库中删除文件

   `git rm 文件名`

2. 恢复删除

   参见***撤销修改***

3. 从版本库中删除文件，但是本地不删除该文件

   `git rm --cached 文件名`

#### z.2.6 重命名文件

1. 将**文件 / 文件夹**重命名

   `git mv`

#### z.2.7 暂存修改

参照**分支 - 暂存修改**

#### z.2.8 忽略文件

通过git仓库下的.gitignore文件屏蔽某些中间文件 / 生成文件

### z.3 分支

#### z.3.1 创建与合并分支

1. 创建分支

   * 仅创建分支

     `git branch 分支名`

   * 创建并切换

     `git checkout -b 分支名`

     **注：在本地仓库操作，创建的都是本地分支**

2. 切换分支

   * `git checkout 分支名`
   * `git switch`*早期版本不支持，需使用最新版的git*

3. 合并分支

   * 合并某分支到当前分支：`git merge 分支名`

     注意：合并分支时禁用fast forward:`git merge --no-ff 分支名`

   * `git rebase`

     若无特殊需要不建议使用

4. 删除分支

   * 删除本地分支
     * 删除未合并分支：`git branch -D 分支名`
     * 删除已合并分支：`git branch -d 分支名`

   * 删除远程分支

     * `git push origin -d 分支名`

     * `git push <远程仓库名>  -d 分支名`

       建议界面操作

5. 查看分支

   * 查看当前分支：`git branch`

   * 查看所有分支信息：`git branch -a`

     本地分支为本地分支名；远程分支为 <远程仓库名>/分支名

6. 合并分支，解决分支冲突

   * 将要合并的分支更新到最新 
   * 切换到主分支
   * 合并分支
   * 解决合并时的conflict
   * 提交到版本库
   * 合并成功
   * 查看分支状态
     * `git log --graph`
     * `git log --graph --pretty=oneline --abbrev-commit`

7. 开发完需要提交PR /MR

   通过PR / MR来合并开发分支与主分支

#### z.3.2 暂存修改

1. 暂存工作现场

   `git stash`

2. 恢复工作现场

   * 恢复：`git stash apply`
   * 删除：`git stash drop`
   * 恢复+删除：`git stash pop`

#### z.3.3 多人协作

建议开发遵循或者参照 git 标准工作流，比如 git flow、github flow 或者 gitlab flow

1. 查看远程仓库信息

   * 详细：`git remote -v`
   * 不详细：`git remote`

2. 更新 / 推送远程库

   * 更新远程库信息：`git fetch`

   * 将远程库最新修改更新到本地：`git pull`

     git pull可以认为是git fetch+git merge

   * 将本地修改推送到远程库

     `git push`

     `git push origin 分支名`

3. 本地分支与远程分支交互

   * 使用远程分支 A 创建本地分支：`git checkout -b A origin/A`

     origin 是远程仓库名，若名字一样 origin/A 可以省略

   * 将本地分支与远程分支作关联：`git branch --set-upstream A origin/A`

     提示 no tracking information 错误

### z.4 操作 tag

tag与branch的操作基本一致，因为tag就是一个仅可读的branch

#### z.4.1 查看tag

1. 本地tag

   `git tag`

2. 远程tag

   `git tag -r`

#### z.4.2 操作tag

1. 添加tag

   * 给当前版本添加tag：`git tag 标签名`
   * 给历史版本添加tag：`git tag 标签名 commit-id`

2. 删除tag

   * 删除本地标签：`git tag -d 标签名`
   * 删除远程标签：`git tag 标签名 commit-id`

3. 推送到远程仓库

   * 推送单个tag：`git push origin 标签名`
   * 推送所有未提交的tag：`git push origin --tags`

4. 更新到本地

   `git pull origin --tags`



### z.5 其他生僻命令

*可以使用 git help 查看 git 常用的命令，使用 git help -a 查看 git 可用的所有命令*

### z.6 命令脑图分布

![不开心呀](https://github.com/akui777/image/blob/master/img77720200811110933.png)