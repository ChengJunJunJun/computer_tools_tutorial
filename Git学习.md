# GitHub使用教程

## github中常见的命令或者界面选项解释记录

### blame

在GitHub中，`blame` 是一个版本控制系统中常见的操作，它用于查看文件的每一行代码是谁在何时进行的修改。通过使用 `git blame` 命令，你可以查看文件的每一行，了解每次修改的提交信息、作者和修改时间。

这对于追踪代码变更、了解代码的演化历程以及找出特定问题引入的起因都非常有帮助。通过 `blame`，你可以追溯到代码的历史，了解每个贡献者的贡献，以及在何时、何地进行的更改。



## Git 

git的三个概念：提交 commit    仓库 repository    分支 branch

1，初始化git

```
git init
```

2，第一次提交

```
git add -A （提交到暂存区）
git commit -m "提交信息" （提交到信息的意思是每次提交都会有一个名字，描述一下这个提交是什么，找到时候知道是哪一次改了什么文件）
```

3，查看提交的历史

```
git log --stat
git status
```



## 分支

1，从当前节点新建分支

```
git checkout -b <branchname>
```

2，列举所有分支

```
git branch
```

3，单纯的切换到某个分支

```
git checkout <branchname>
```

4，删掉特定的分支

```
git branch -D <branchname>
```

5，合并分支

```
git merge <branchname>
```

6，放弃合并

```
git merge --abort 
```



##  create a new repository on the commom line

```
echo "# bababababba" >> README.md
git init
git add README.md
git commint -m "first commint"
git branch -M main
git remote add origin http:///
git push -u origin main
```

## push an existing repository from the commond line

```
git remote add origin http:///
git branch -M main
git push -u origin main
```





## 常用命令及解释

```bash
git log
commit 3cb84b16b36cbd0daf8c82840c2912101653d516 (HEAD -> main, origin/main, origin/HEAD) # origin/main, origin/HEAD 这两个是一个分支
Author: 程骏 <chengjun.miracle@gmail.com>
Date:   Sat Mar 16 22:44:17 2024 +0800
```

这是一个标准的 `git log` 输出，每行提供了有关 git 仓库中提交历史的信息。

1. `commit 3cb84b16b36cbd0daf8c82840c2912101653d516 (HEAD -> main, origin/main, origin/HEAD)`
   - `commit`: 这是 git 提交的标识。
   - `3cb84b16b36cbd0daf8c82840c2912101653d516`: 这是提交的哈希值，用于唯一标识此次提交。
   - `(HEAD -> main, origin/main, origin/HEAD)`: 这是指向此提交的引用，其中 `HEAD` 表示当前所在的分支，`main` 是当前分支的名字，`origin/main` 和 `origin/HEAD` 是远程仓库的分支。
2. `Author: 程骏 <chengjun.miracle@gmail.com>`
   - `Author`: 提交的作者。
   - `程骏 <chengjun.miracle@gmail.com>`: 提交的作者姓名和邮箱。
3. `Date: Sat Mar 16 22:44:17 2024 +0800`
   - `Date`: 提交的日期和时间。
   - `Sat Mar 16 22:44:17 2024 +0800`: 提交的具体日期和时间，以及时区信息。

```bash
git checkout dell ## 切换分支使用git checkout命令
```



```bash
PS D:\Project_Windows\College_student_innovation_project> git pull
There is no tracking information for the current branch.
Please specify which branch you want to merge with.
See git-pull(1) for details.

    git pull <remote> <branch>

If you wish to set tracking information for this branch you can do so with:

    git branch --set-upstream-to=origin/<branch> dell
```

这个输出显示了在执行 `git pull` 命令时出现的消息，让我逐行解释：

1. `PS D:\Project_Windows\College_student_innovation_project> git pull`
   - 这是你在终端（或命令提示符）中执行的 Git 命令，即 `git pull`。
2. `There is no tracking information for the current branch.`
   - 这一行提示当前分支没有追踪信息。这意味着当前分支没有指定与之关联的远程分支。
3. `Please specify which branch you want to merge with.`
   - 提示你需要指定要与之合并的分支。这是因为 Git 不知道在执行 `git pull` 时应该从哪个远程分支拉取更新。
4. `See git-pull(1) for details.`
   - 提示你可以查看 `git-pull(1)` 的文档以获取更多详细信息。
5. `git pull <remote> <branch>`
   - 提供了 `git pull` 命令的基本格式，其中 `<remote>` 是远程仓库的名称，`<branch>` 是要从中拉取更新的远程分支的名称。
6. `If you wish to set tracking information for this branch you can do so with:`
   - 提示如果你想为当前分支设置追踪信息，可以使用下面的命令进行设置。
7. `git branch --set-upstream-to=origin/<branch> dell`
   - 这是设置追踪信息的命令示例。它告诉 Git 将当前分支 `dell` 设置为追踪 `origin` 远程仓库上的 `<branch>` 分支。这样，当你执行 `git pull` 时，Git 就会知道从哪个远程分支拉取更新。

```bash
git branch --set-upstream-to=origin/main dell #将本地分支与远程分支关联起来
```





要查看本地仓库和远程仓库的关联状态，你可以使用 `git remote` 命令来查看远程仓库的信息，以及 `git branch` 命令来查看本地分支的追踪情况。以下是具体的步骤：

1. 查看远程仓库的信息，包括它们的名称和 URL。执行以下命令：

   ```
   Copy code
   git remote -v
   ```

   这会列出所有远程仓库的名称以及它们的 URL。如果远程仓库已经添加到本地仓库，你会看到它们的信息。

2. 查看本地分支的追踪情况。执行以下命令：

   ```
   Copy code
   git branch -vv
   ```

   这会列出所有本地分支的名称以及它们是否有追踪关系。如果某个分支有追踪关系，你会看到它们与哪个远程分支关联，以及远程分支的状态（比如远程分支的最新提交和本地分支的差距）。

通过这两个命令的输出，你可以了解本地仓库和远程仓库之间的关联状态。



```bash
PS D:\Project_Windows\College_student_innovation_project> git push
fatal: The current branch dell has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin dell

To have this happen automatically for branches without a tracking
upstream, see 'push.autoSetupRemote' in 'git help config'.
```

这是执行 `git push` 命令后的输出，让我逐行解释：

1. `fatal: The current branch dell has no upstream branch.`
   - `fatal`: 这表示一个致命错误，即操作无法继续进行。
   - `The current branch dell has no upstream branch.`: 这个错误消息说明了当前分支 `dell` 没有指定的上游分支（即追踪分支）。
2. `To push the current branch and set the remote as upstream, use`
   - 这句话提示了如何解决问题的建议。
3. `git push --set-upstream origin dell`
   - 这是建议的解决方案。它告诉你可以使用 `git push --set-upstream origin dell` 命令将当前分支 `dell` 推送到远程仓库 `origin`，并设置远程分支 `origin/dell` 作为当前分支的上游分支（追踪分支）。
4. `To have this happen automatically for branches without a tracking upstream, see 'push.autoSetupRemote' in 'git help config'.`
   - 这是另一个建议，它告诉你可以查看 Git 配置中的 `push.autoSetupRemote` 选项，来设置是否要自动为没有追踪上游分支的分支进行追踪设置。





`push.autoSetupRemote` 是 Git 配置中的一个选项，用于控制在执行 `git push` 命令时是否自动为没有追踪上游分支的分支设置追踪关系。让我详细解释一下：

1. **追踪分支（Upstream Branch）**：

   在 Git 中，每个分支都可以设置一个追踪分支，它表示了当前分支与远程仓库中的哪个分支有关联。当你执行 `git push` 或 `git pull` 命令时，Git 会自动知道应该推送到哪个远程分支，或者从哪个远程分支拉取更新。

2. **push.autoSetupRemote 选项**：

   `push.autoSetupRemote` 选项允许你控制是否在执行 `git push` 时自动为没有追踪上游分支的本地分支设置追踪关系。当该选项被设置为 `true` 时，Git 会在你执行 `git push` 时自动设置远程分支作为当前分支的追踪分支。

3. **如何使用**：

   你可以通过以下命令来查看当前是否启用了 `push.autoSetupRemote` 选项：

   ```
   arduinoCopy code
   git config --get push.autoSetupRemote
   ```

   如果该选项返回 `true`，则表示启用了自动设置远程分支的功能。如果没有启用，你可以通过以下命令来启用它：

   ```
   arduinoCopy code
   git config push.autoSetupRemote true
   ```

   这将会启用自动设置远程分支的功能，当你执行 `git push` 时，Git 将会自动设置远程分支作为当前分支的追踪分支。

设置了 `push.autoSetupRemote` 后，你就不需要手动执行 `git push --set-upstream origin <branch>` 来为每个新分支设置追踪关系了，Git 会在需要时自动为你完成这个任务。







`git push --set-upstream origin main` 和 `git push -u origin main` 都表示将当前分支（假设当前分支是 `main`）推送到远程仓库，并将远程仓库的 `main` 分支设置为当前分支的追踪分支（也就是上游分支）。

`-u` 是 `--set-upstream` 的缩写形式，用于设置追踪分支。这两种写法完全等价，你可以根据个人喜好选择使用其中的一种。







要删除远程仓库 `origin`，可以使用 `git remote` 命令的 `rm` 选项。以下是具体的步骤：

1. 首先，确认你真的想要删除远程仓库 `origin`，因为这会导致你与该远程仓库的所有关联信息被删除。

2. 执行以下命令删除远程仓库 `origin`：

   ```
   bashCopy code
   git remote rm origin
   ```

   这将会从你的本地仓库中移除对远程仓库 `origin` 的引用。

执行完这个命令后，`origin` 远程仓库将不再存在于你的本地仓库中，但请注意，这不会删除远程仓库本身或其中的任何数据，它只是从你的本地仓库中移除了对该远程仓库的引用。



要同时在本地和远程删除分支，可以使用 `git push` 命令的 `--delete` 选项，以及 `git branch` 命令。以下是具体的步骤：

1. 首先，确保你已经切换到要删除的分支上，或者可以直接指定分支名称。

2. 在本地删除分支，可以使用 `git branch -d` 命令。假设要删除的分支名称是 `my_branch`，则执行以下命令：

   ```
   Copy code
   git branch -d my_branch
   ```

   如果分支上有未合并的更改，Git 会给出警告并阻止删除。如果你确定要强制删除未合并的分支，可以使用 `-D` 选项：

   ```
   mathematicaCopy code
   git branch -D my_branch
   ```

3. 然后，使用 `git push` 命令的 `--delete` 选项删除远程分支。假设要删除的远程分支名称也是 `my_branch`，则执行以下命令：

   ```
   perlCopy code
   git push origin --delete my_branch
   ```

   这会将本地的分支删除，并从远程仓库中删除同名的分支。


