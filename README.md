## 回退版本
* HEAD 指向的版本就是当前版本，因此，Git允许我们在版本历史之间穿梭，使用命令 `git reset --hard commit_id`;
* 穿梭前，可以使用 `git log` 查看提交的历史记录，以便确定要回退的版本;
* 要重返未来，用`git reflog`查看命令历史，以便自己确定要回到未来的那个版本;

## 工作区和暂存区
* 暂存区是Git非常重要的概念，弄明白了暂存区，就弄明白了Git很多操作是做什么;

*git 是通过的文件修改从而管理整个工作区的工作情况

## 撤销修改
* 场景1: 当你该乱了工作区的内容，想直接丢弃工作区的修改时，可以用 `git checkout -- <file>`;  
* 场景2: 当你不但改乱了工作区的内容，还添加到了暂存区，这时候想丢弃修改要分两个步骤： 1: `git reset HEAD <file>`撤回到场景1；2: 在使用场景1的操作进行回退;  
* 场景3: 已经提交了不合适的修改到版本库时，想要撤销本次提交，可以使用 `git reset commit_id --hard` 回退版本；  

## 删除文件
* `git checkout`其实使用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以"一键还原";  
* `git rm`用于删除一个文件，如果他一个文件已经被提交到版本库，那你永远不要怕担心误删,但是要小心，但是只能恢复到最新的版本，你会丢失最提交后的修改内容;  

## 关联远程仓库
* 关联远程仓库，使用命令` git remote add origin git@server-name:path/repo-name.git`, 关联远程仓库时必须给远程仓库取个名字，一般都用 `origin`;
* 将本地的分支与远程分支进行绑定, 使用命令 `git push --set-upstream origin main`;
* 分支的重命名命令, 使用命令 `git branch -M <name>`;

## 分支管理
* 查看分支，`git branch`;
* 创建分支, `git branch <name>`;
* 切换分支, `git checkout <name> | git switch <name>`;  
* 创建以及切换分支: `git checkout -b <name> | git switch -c <name>`;
* 合并某分支到当前分支: `git merge <name>`;
* 删除某分支: `git branch -d <name>`;

## 分支合并
当分支无法进行合并时，这时候需要我们进行手动合并，解决冲突之后再次进行提交，使用 `git log --graph`命令可以看到分支的合并图.

## 分支管理策略
* 首先，master分支是非常稳定的，一般用来发布新的版本，不能用来干活。
* dev分支是不稳定，所有的工作开展都放在dev分支上,到某个节点，才能把dev分支合并到master分支。
* bug分支与master分支进行同步，该分支用来紧急修复线上的bug；
* feature分支，每个功能的特性分支，应该是从dev分支克隆出来，开发完成之后合并到dev分支;

tip: 分支进行合并时，可以加上`--no-ff`参数，用于表示不采用`fast forward`模式进行合并，从而可以显示合并的历史。

## bug 分支
修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；  
当前分支工作没有完成的时候，可以使用`git stash`来保存现场，然后去修复bug, bug修复完成之后，再切回分支，然后使用`git stash pop`来恢复现场。  
在master分支修复的bug，提交之后会有一个commit_id,从而也可使用`git cherry-pick commit_id`将改次提交带到其他的分支;  

