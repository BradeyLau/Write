> 基本的Linus命令
> 
> `ls/ll`查看目录
> 
> `cat`查看内容
> 
> 'touch'创建文件
> 
> `vi`编辑

# 01. 安装及初始化

```git
//设置用户名和邮箱
git config --global user.name "Your Name" //名字可能有空格
git config --global user.email mail@examole.com
//查看用户名和邮箱
git config --global user.name
config config --global user.email
//设置记住账户密码
git config --global credential.helper store
```

> `Local`:一般省略，只对本地仓库有效

> `--global`:全局配置，对所有仓库生效

> `--system`:系统配置，对所有用户生效

# 02. 新建仓库

```git
git init//初始化当前目录为一个git仓库
git clone <file_name>//
```

> 创建好一个仓库,其中必然包含一个`.git`文件,如果将这个文件删除,那仓库就会变成一个普通的文件夹!

# 03. 工作区域

> 工作区(Working Director)`文件夹`
> 
> `git add`添加到暂存区
> 
> `git rm --cached <file> 将文件取消暂存`
> 
> 暂存区(Staging Area/Index)`等待被提交`
> 
> `git ls-files`查看暂存区的文件
> 
> `git commit`提交到本地仓库,`只会提交暂存区中的文件`
> 
> 本地仓库(Local Repository)

# 04. 文件状态

Untrack(未跟踪):新创建的文件,还没有被git管理起来的状态.

Unstaged(未暂存):修改已有文件.

Unmodified(未修改):已经被git管理起来,但内容没发生变化.

Modified(已修改):修改了文件,但还没有进入暂存区.

Staged(已暂存):已经加入到暂存区.

# 05. 添加和提交文件

`git status`查看仓库状态

`git add .`将当前文件夹添加到暂存区

`git add *.c`把所有.c文件添加到暂存区

`git commit -m "info"`,这个信息会被记录到仓库里面

`git log`查看提交记录

--all 显示所有分支

--pretty=oneline 显示一行

--abbrev-commit 简洁

-graph 图形式

`git reflog`:全部操作记录(提交和回退记录)

# 06. 回退版本

`git reset`的默认参数是`--mixed`

`git reset --soft`回退到某一个版本,并保留工作区和暂存区的所有修改内容

`git reset --hard`回退到某一个版本,丢弃工作区和暂存区的所有修改内容

`git reset --mixed`回退到某一个版本,并保留工作区的修改内容,丢弃暂存区的修改内容

`git reset [参数] commit_id`,id表示提交时的版本id

`git reset HEAD^`回退到上一个版本

> HEAD是一个指针,指向当前分支的最新节点

# 07. 查看差异

`git diff`查看文件在工作区,暂存区以及版本库之间的差异

`git diff`默认比较的是工作区和暂存区之间的差异内容

`git diff HEAD`比较工作区和版本库之间的差异内容

`git diff --cached`比较暂存区和版本库之间的差异内容

`git diff id1 id2`比较两个特定版本之间的差异内容

`git diff HEAD~ HEAD`和上一个版本比较差异内容,`HEAD^`也可以

`git diff HEAD~2 HEAD`和前两个版本比较差异内容

`git diff HEAD~ HEAD <file>`只查看file的差异内容

`git diff <branch_name> <branch_name>`比较分之间的差异内容

# 08. 删除文件

删除文件一般有两种方法.

1. 先在本地工作区中删除文件,然后`git add`更新暂存区

2. `git rm <file>`直接从暂存区和工作区删除

最后记得`git commit`提交到仓库,否则删除的文件还在版本库中

补充:

> `git rm --cached <file>`把文件从暂存区删除,但保留在当前工作区.
> 
> `git rm -r *`递归删除某个目录下的所有子目录和文件夹

命令行指令rm 用于删除文件、目录, rm = remove
-i 删除前提示, y删除, n不删除
-r 删除一个目录(含所有文件), r = repository
-f 强制执行删除操作, f = force
参数可叠加， 如rm -rf \<dir>，直接删除目录

# 09. 忽略文件

.git<font color = "#FF0000">ignore</font>应该忽略那些文件呢?

- 系统或软件自动生成的文件

- 编译产生的中间文件或结果文件

- 运行时生成的日志文件,缓存文件,临时文件

- 涉及身份,密码,口令,密钥等敏感信息的文件

> [git匹配规则](https://git-scm.com/docs/gitignore "git官网匹配规则"):
> 
> 从上到下逐行匹配,每一行表示一个忽略模式

# 10. SSH配置和克隆仓库

`HTTPS`:push时需要验证用户名和密码

`SSH`:无需验证用户名和密码,但要配置SSH公钥(推荐)

- 复制仓库SSH链接,在本地`git clone <SSH链接>`,会提示:`Please make sure you have the correct access rights and the repository exists.`请不要担心.

- `cd`到用户根目录下,再`cd .ssh`

- 使用`ssh-key generate -t rsa -b 4096`生成SSH密钥(`-t rsa`指定协议rsa,`-b 4096`指定生成大小为4096)

- 系统提示需要输入密钥的文件名,若第一次使用,直接按回车就好;若第二次使用(之前已经配置过SSH),最好不要直接回车,否则会覆盖掉之前的id_rsa密钥文件,且操作不可逆.

- 此时.ssh文件下多出来两个文件,`id_rsa`是私钥文件,`id_rsa.pub`就是公钥文件

- 打开公钥文件,复制里面的内容

- 回到github网页,点击头像进入`settings`,点击左侧`SSH and GPG keys`,在右侧点击`New SSH key`,将公钥粘贴进去,Title任意输入即可

- 最后点击 <font color = "#008000">Add SSH key</font> 就成功地把公钥添加到github上了.

> 如果你的.ssh文件夹里有多个密钥文件,那还要增加一步配置
> 
> 创建一个config文件,并把这5行内容添加进去

```git
# github
Host github.com
HostName github.com
PreferredAuthentications publicksy
IdentityFile ~/.ssh/<new id_rsa file name>
```

意思是:当我们访问github时,指定使用<new id_rsa file name>这个密钥

# 11. 本地仓库和远程仓库

git是一种分布式的版本控制系统.本地仓库和远程仓库是相互独立的,我们可以在本地仓库中做任何修改,这并不会影响到远程仓库;同样远程仓库的修改也不会影响到我们本地仓库.

**我们需要一种机制来同步本地仓库和远程仓库的修改内容**

`git push`:把本地仓库的修改推送到远程仓库

`git pull`:把远程仓库的修改拉取到本地仓库

# 12. 关联本地仓库和远程仓库

`git remote add <shortname> <url>`:为本地仓库添加一个远程仓库

> 以本人的博客为例:
> 
> `git remote add origin git@github.com:BradeyLau.github.io.git`(origin是远程仓库的别名(默认))
> 
> `git remote -v`:查看当前本地仓库对应的远程仓库的别名和地址
> 
> `git branch -M main`:指定分支的名称为main,一般默认的分支就是main,所以这一步可以省略
> 
> `git push [-f] -u origin main`:将本地的main分支和远程的origin仓库的main分支关联起来,-f强制覆盖---set-upstream表示推送的同时建立连接(绑定)

其实`git push -u origin main:main`是完整的命令,`-u`是upstream的缩写,意思是把本地仓库和别名为origin的远程仓库关联起来(如果远端仓库不是空的)

main:main就是把本地仓库的main分支推送给远程仓库的main分支,如果他们的名字相同的话,我们可以省略,只写一个main就可以了.

<font color="red">git push origin master</font>:把本地的master分支推送到远端的origin仓库,master分支不是init就有的,是在第一次commit才有的

<font color="red">git push --set-upstream origin master:master</font>

当有了链接之后就可以直接git push了

`git branch -vv`可以查看本地本质和远程分支的对应关系

`git pull <远程仓库名> <远程分支名>:<本地分支名>`

# 13.分支使用流程

- [ ] 待补充内容

# 14.抓取和拉取

抓取:`git fetch [remote name] [branch name]`:将远端的分支抓取到本地,但不会合并

合并:`git merge origin/master`

拉去:`git pull`:抓取加合并

# 15.解决合并冲突

待补充
