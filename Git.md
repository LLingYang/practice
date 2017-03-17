# Git第二天
## Git基础命令复习
git config --global user.name "自已的名字"
git config --global user.email "自已的邮箱地址"

--global：表示本机只需要配置一次，本地的所有git仓库都是共享该信息的

git init

git status

git add 1.txt
git add 1.txt 2.txt 3.html
git add *

git commit

git log

git checkout -- 1.txt：将暂存区中的文件取出并替换工作目录的文件

git reset HEAD 1.txt：将暂存区的文件取出来，对工作目录的代码不会造成影响

git reset --hard 提交的版本号(可以只写前几位)

## Git基础命令补充
+ 将某个版本的文件从本地主仓库中恢复，取出来的文件替换工作目录的文件
git reset --hard 提交的版本号(可以只写前几位)

+ git reflog 查看历史记录
这些历史记录包括：每一次提交的信息；以及每一次版本回滚的操作

## 设置文件不让git管理
1、在.git同级目录添加一个文件，叫 .gitignore
    创建这个文件名的时候，
        a：文件名：".gitignore."
        b、bash命令：touch .gitignore
2、打开.gitignore进行编辑，一行一行的添加不需要git管理的文件
    可以设置同类型的文件：*.js *.css
    也可以设置整个目录：
        a/*-->a目录下面的所有文件
        a/*.js-->a目录下面的所有js文件

## Github入门
### Github基本使用
1. 注册账号
2. 登录
3. 创建一个仓库：
     a、点击右上角"+"-->"add new repository"
     b、依次输入仓库名称、仓库描述、以及是否为公开的(私密的要钱)，
     c、点击 create repository按钮

### Github跟本地仓库进行交互
#### 将github上某个仓库的内容下载到本地
git clone 远程仓库地址
git clone 远程仓库地址 本地文件夹路径：将远程仓库的内容拷贝到本地指定文件夹
举例：git clone https://github.com/chengxc/test006.github.io.git

#### 将本地仓库的代码提交到git服务器中
a、git push 远程服务器仓库的地址 master

注意点：1、提交到github的时候会提示你输入github的用户名和密码
       2、只能由本地主仓库和远程服务器之间进行交互，如果本地主仓库中没有内容，无法更新到服务器

b、也可以给服务器地址起一个名称，如下：
git remote add origin(变量名) 服务器地址
    git remote remove origin

git push origin master

补充：git remote表示该自命令下面已经添加过的名称

c、git push -u master：默认将本地当前分支与远程服务器某个分支关联，后续的push不需要再次指定远程服务器分支名称
    如果想要提交到远程服务器的指定分支，还是应该提供分支名称

d、获取远程服务器的更新
git pull 服务器地址

e、删除文件1：
rm 文件名
git add 文件名
git commit -m 提交
git push 远程服务器 master

f、删除文件2：
git rm 文件名
git commit -m 提交
git push 远程服务器 master


### Git本地分支映射到github中
1. 在本地创建一个新的分支
2、将代码提交到该分支中
3、git push 远程仓库地址 远程仓库的新分支的名称

### Github搭建静态服务器
1、新建一个仓库，仓库名字：用户名.github.io
    一个用户只能拥有一个自己的网站
2、往该github仓库中添加代码，注意最好给这些目录中添加一个index.html文件
3、直接使用仓库的名字作为网站的地址来访问

## 分支：
### 分支的必要性？

### 分支操作命令：
git branch：查看当前仓库中所有的分支
*：表示当前处于哪一个分支

git branch 名称：创建一个指定的分支

git checkout 分支名称：切换到指定的分支
    切换后的代码就是指定分支的代码

git merge 分支名：将指定分支合并到当前分支下

分支冲突：如果两个合并的分支操作了同样的文件，这时候很可能产生冲突，这样这两个分支在合并的时候就会提示合并出现失败，这时候需要手动解决冲突，解决好冲突之后，重新将代码提交

git branch -d 分支名称：删除指定的分支

### 分支使用说明
1. 在创建分支的时候，一定要对创建的分支所处于的那个分支，要在该分支稳定的时候才能创建；在该分支的代码完全提交之后才能创建新分支

2. 本地分支和远程分支是两个独立体

### 分支使用策略
一般来说master分支中始终保存最稳定的代码，
如果要开发新功能，就新建分支，在该分支中可以获取到此时的master里面的全部内容，然后在该分支中进行开发，开发完毕进行提交，跟master分支进行合并，合并完成删除该分支。

如果开发过程中需要完成其他功能，再次在master分支基础上新建分支，在新分支中完成其他功能，完成之后，进行分支合并，合并之后就把分支删除

### 分支操作流程：
+ 查看分支:git branch
+ 创建分支：git branch 名称
+ 切换到指定分支：git checkout 名称
+ 在该分支下面提交代码：从工作区到暂存区到主仓库
+ 切换到master分支：git checkout master
+ 将指定的分支合并到当前分支下(master)：git merge 名称
+ 删除分支：git branch -d 名称
+ 查看分支：git branch

## Github进阶
### git pull取回远程主机某个分支的更新，再与本地的指定分支合并。
 用法：git pull <远程主机名> <远程分支名>:<本地分支名>
 可以不指定本地的指定分支，默认就是当前处于哪个分支

规则：如果希望将远程的分支更新到本地的指定分支，他们的分支名应该是一一对应的


### git fetch：取回服务器中的指定分支
1. git fetch取回所有分支的更新。
2. 如果只想取回特定分支的更新，可以指定分支名。
    用法：git fetch <远程主机名> <分支名>

备注：取出来的分支可以使用 git branch -a 获取
后续可以根据自己的需求采取分支合并操作

+ 操作步骤：
1、在本地新建仓库
2、pull更新服务器的文件：git pull 服务器地址 master
3、获取远程分支：git fetch 远程服务器地址 分支名
4、查看分支：git branch -a
5、在本地创建新分支：git branch abc
6、切换到指定的分支下：git checkout abc
7、将远程的register分支合并到abc分支：git merge remotes/服务器的仓库名/register


## 比较文件差异
### git diff
1、比较工作目录和暂存区的代码比较
2、如果暂存区没有文件，则将工作区和最近一次提交的代码进行对比

### git diff --cached：将暂存区的文件和工作区的文件进行对比

## SSH
### 对称性加密
###　非对称性加密

### 配置SSH连接github
1. 在本地生成秘钥：ssh-keygen -t rsa
2. 找到秘钥生成的目录，将公钥放到Github中
    a、github点击右上角人物头像
    b、选择settings菜单
    c、选择SSH相关菜单
    d、选择添加一个SSH
    e、输入ssh的名称，已知内容（就是公钥）将公钥放入其中，保存即可
3. 在本地测试 ssh git@github.com看看是否成功
Hi chengxc! You've successfully authenticated, but GitHub does not provide shell access.

4. 提交代码
备注：如果在提交代码的时候github中已经含有内容，最好先更新代码，使用SSH地址进行提交：
git pull --rebase origin master
