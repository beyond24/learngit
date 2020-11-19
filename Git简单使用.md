## Git 简单使用

- 关于工作区、暂缓区(stage)、仓库(master)

  

  <img src="https://www.liaoxuefeng.com/files/attachments/919020037470528/0" alt="git-repo" style="zoom:150%;" />

  在本机上修改/创建一个文件相当于track文件到**工作区**

  `git add`：把文件添加进去，实际上就是把文件修改添加到**暂存区**；

  `git commit`：提交更改，我们创建Git版本库时，Git自动为我们创建了唯一一个`master`分    支，所以，现在，`git commit`就是往`master`分支上提交更改。

  `git status`：查看工作区的状态，`comimit` 后显示工作区是“干净的”。



  `git diff`：当**工作区**有改动，**暂存区**为空，diff的对比是**工作区**与**仓库**的共同文件；当**工作区**有改动，**暂存**不为空，diff对比的是**工作区**与**暂存区**的共同文件。

  `git diff --cached` 或 `git diff --staged`：显示**暂存区**(已add但未commit文件)和**仓库**(最后一次commit)之间的所有不相同文件的增删改。

  `git diff HEAD`：显示**工作区**(已track但未add文件)和**暂存区**与**仓库**(最后一次commit)之间的的所有不相同文件的增删改。

  `git diff HEAD~X`或`git diff HEAD`(后面有X个^符号，X为正整数):可以查看最近一次提交的版本与往过去时间线前数X个的版本之间的所有同文件间的增删改。

  `git checkout -- filename`：git add的反向命令，撤销**工作区**修改，即把**暂存区**最新版本转移到**工作区**，

  `git reset head filename`：git commit的反向命令，把**仓库**最新版本转移到**暂存区**。



- 远程仓库

  远程关联本地仓库：

  ```
  git remote add origin https://github.com/beyond24/learngit.git
  ```

  删除关联：

  ```
  git remote rm origin
  ```

  本地内容推送到远程仓库：

  ```
  git push (-u) origin master
  ```

- 分支管理

  查看分支：`git branch`

  创建分支：`git branch <name>`

  切换分支：`git checkout <name>`或者`git switch <name>`

  创建+切换分支：`git checkout -b <name>`或者`git switch -c <name>`

  合并某分支到当前分支：`git merge (--no-ff) (-m 'info') <name>`

  > 合并分支时，加上`--no-ff`参数就可以用普通模式合并，合并后的历史有分支，能	看出来曾经做过合并，而默认的`fast forward`合并就看不出来曾经做过合并

  删除分支：`git branch -d <name>`

- 解决冲突

  Git无法自动合并分支时，就必须首先解决冲突。

  解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交。

  `git log --graph `可以查看分支合并图。
  
- bug分支/feature分支

  `git stash`：保存工作现场

  `git stash pop`：回到工作现场

  `git cherry-pick <commit>`： 把bug提交的修改“复制”到当前分支

  `git branch -D feature-vulcan`：强行删除分支

- 多人协作

  - 查看远程库信息，使用`git remote -v`；
  - 本地新建的分支如果不推送到远程，对其他人就是不可见的；
  - 从本地推送分支，使用`git push origin branch-name`，如果推送失败，先用`git pull`抓取远程的新提交；
  - 在本地创建和远程分支对应的分支，使用`git checkout -b branch-name origin/branch-name`，本地和远程分支的名称最好一致；
  - 建立本地分支和远程分支的关联，使用`git branch --set-upstream branch-name origin/branch-name`；
  - 从远程抓取分支，使用`git pull`，如果有冲突，要先处理冲突。

- rebase、

  `git rebase`

  > rebase操作可以把本地未push的分叉提交历史整理成直线；
  > rebase的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比。

