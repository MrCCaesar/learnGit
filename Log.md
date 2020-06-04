# 创建版本库
## 创建本地文件夹
```
mkdir learnGit
cd learnGit
```
## 初始化
`git init`
<br/>以下的命令均在工作目录下打开git Bash中输入</br>
# 文件操作

## 文件添加，提交
<br/>在创建的文件下创建文件编辑完成后</br>
`git add <file name>`
<br/>将修改后的文件添加到暂存区</br>

`git commit -m <描述本次做出的修改>`
<br/>将暂存区的文件提交到仓库</br>

`git status`
<br/>获取仓库当前状态</br>

`git diff <文件名>`
<br/>比较文件做出的改变</br>

## 文件版本回退
`git log`
<br/>查看由近到远的提交日志</br>

`git reflog`
<br/>查看命令历史</br>

`git reset --hard <版本号/HEAD>`
<br/>将仓库回复为版本号对应提交后仓库的状态，HEAD表示最新版本，HEAD^为上一版</br>本，依此类推，100个前版本写作HEAD~100；版本号由上两条命令获得</br>

![工作区和版本库](https://www.liaoxuefeng.com/files/attachments/919020037470528/0)


## 文件修改和删除
`git checkout -- <文件名>`
<br/>可以取消工作区的修改</br>

`git reset HEAD <文件名>`
<br/>可以将已经提交到暂存区的文件修改撤销并返回到工作区，然后用上一条命令彻底取消修改</br>

```
git rm <文件名>
git commit -m <message>
```
<br/>可以将版本库中的文件删除，如果在工作区误删文件可以用撤销工作其修改的指令从版本库中回复</br>

# 远程仓库
<br/>在工作目录下执行</br>
`ssh-keygen -t rsa -C "youremail@example.com"`
<br/>可以在对应的目录中找到ssh key</br>将其中的id_rsa.pub文件中的内容复制到github网站中的setting——>SSH Keys——>add SSH key</br>的key栏中</br>
在GitHub中新建一个仓库后，可以用</br>
`git  git remote add origin git@github.com:michaelliao/learngit.git`
<br/>关联本地库和远程库</br>
`git push -u origin master`
<br/>将本地的master分支推送到远程仓库</br>

`git clone <网址>`
<br/>将远程仓库克隆到本地</br>

# 分支管理
## 分支创建与合并
分支可以在不对主分支变动的情况下继续工作，完成工作后可以合并在一起</br>
![master](https://www.liaoxuefeng.com/files/attachments/919022325462368/0)</br>
![创建dev分支](https://www.liaoxuefeng.com/files/attachments/919022363210080/l)</br>
![在dev分支上继续工作](https://www.liaoxuefeng.com/files/attachments/919022387118368/l)</br>
![合并](https://www.liaoxuefeng.com/files/attachments/919022412005504/0)</br>
![删除dev分支](https://www.liaoxuefeng.com/files/attachments/919022479428512/0)</br>

`git checkout -b dev`
<br/>相当于</br>
```
git branch dev
git checkout dev = git switch -c dev
```
<br/>创建分支dev，并切换到分支dev</br>

`git branch`
<br/>查看当前分支</br>

`git merge dev`
<br/>将分支dev合并到主分支master上</br>

`git branch -d dev`
<br/>合并后可以安全的删除分支dev</br>
当合并分支出现冲突时，解决冲突后再合并</br>

`git log --graph`
<br/>可以看到合并分支图</br>

## Debug分支
当手头工作没有完成时，先把工作现场<br/>
`git stash`
<br/>一下，然后去修复bug，修复后，再<br/>
`git stash pop`
<br/>相当于<br/>
```
git stash apply <stashID>
#可指定恢复某一个stash
git stash drop
```
<br/>回到工作现场并清除stash记录<br/>
在master分支上修复的bug，想要合并到当前dev分支，可以用<br/>
`git cherry-pick <commit>`
<br/>命令，把bug提交的修改“复制”到当前分支，避免重复劳动<br/>

## Feature分支
如果要丢弃一个没有被合并过的分支，可以通过<br/>
`git branch -D <name>`
<br/>强行删除,其它同Debug分支类似<br/>

## 多人合作
查看远程库信息，使用<br/>
`git remote -v`
<br/>本地新建的分支如果不推送到远程，对其他人就是不可见的<br/>

从本地推送分支，使用<br/>
`git push origin branch-name`
<br/>如果推送失败，先用<br/>
`git pull`
<br/>抓取远程的新提交<br/>

在本地创建和远程分支对应的分支，使用<br/>
`git checkout -b branch-name origin/branch-name`
<br/>本地和远程分支的名称最好一致<br/>

建立本地分支和远程分支的关联，使用<br/>
`git branch --set-upstream branch-name origin/branch-name`
<br/>从远程抓取分支，使用<br/>
`git pull`
<br/>如果有冲突，要先处理冲突<br/>

# 标签管理
标签也是版本库的一个快照,但是不能移动</br>

`git tag <tagname> commit_id`
</br>用于新建一个标签，默认为HEAD，也可以指定一个commit id</br>

`git tag -a <tagname> -m "blablabla... commit_id`
</br>可以指定标签信息</br>

`git tag`
</br>可以查看所有标签</br>

`git push origin <tagname>`
</br>可以推送一个本地标签</br>

`git push origin --tags`
</br>可以推送全部未推送过的本地标签</br>

`git tag -d <tagname>`
</br>可以删除一个本地标签</br>

`git push origin :refs/tags/<tagname>`
</br>可以删除一个远程标签</br>