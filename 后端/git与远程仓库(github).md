摘要：如果想要通过git和他人分享或者协作开发，那么就需要将数据放到其他人也可以连接的服务器上。本文将介绍Github仓库创建，代码拉取、提交等操作。其中第六小节引用至[掘金**YXi**]("https://juejin.im/post/5deb69266fb9a0160e2a1073")。

### 1.生成SSH key

如果是第一次使用如果没有配置SSH key在向Github推送内容是会报错`git@github.com: Permission denied (publickey)`，设置方式如下:

```powershell
# 设置全局的用户名和邮箱
git config --global user.name your_name
git config --global user.email your_email
# 生成SSH key
ssh-keygen -t rsa -C "youremail@simple.com"
```

之后一路回车，在出现选择是输入y，再一路回车知道生成秘钥。这样会在`User/***/`路径下生成一个`.ssh`文件，打开 **id_rsa.pub**，复制里面的 **key**。之后，登录Github点击 `头像 -> Settings -> SSH and GPG keys -> Add SSH key`添加新的ssh key即可。

### 2.仓库创建

登录Github `点击头像 -> Your repositories ->new`，填写相关信息创建仓库。

![img](https://github.com/defaultw/note/blob/master/FigureBed/createrep20200307161619.png)

### 3.根据提示在本地初始化仓库

![img](https://github.com/defaultw/note/blob/master/FigureBed/init20200307162141.png)

在本地新建文件夹中右键 -> git bash here 在当前目录打开git命令行工具。可以根据Github页面提示初始化仓库和提交、推送内容：

```powershell
git init # 初始化
git add README.md # 添加文件，这里可以写'git add .'代表添加所有的文件
git commit -m "first commit" # 提交并备注信息
# 提交到github
git remote add origin git@github.com:defaultw/test.git
git push -u origin master
```

### 4.提取远程仓库

```powershell
# 从远程仓库下载新分支与数据
git fetch
# 从远程仓库提取数据并尝试合并到当前分支
git merge
```

如果已经配置好了一个远程仓库，并且想要提取更新的数据，我们可以先执行`git fetch [alias]`告诉Git去获取当前本地没有的数据，然后可以执行`git merge [alias]/[branch]`将服务器上的任何更新和并到当前的分支。

### 5.推送到远程仓库

```powershell
# 将本地[branch]分支推送成为[alias]远程仓库上的[branch]分支
git push [alias] [branch]
```

### 6.常见命令

- 初始化一个Git(本地)仓库 (只需初始一次)
 `git init`

- 设置用户名和邮箱 (只需设置一次)
 用户名：`git config --global user.name 你的用户名`
邮箱：`git config --global user.email 你的邮箱`

- 把工作区的文件添加到暂存区  (需按自己的需求添加N次)
 `git add 文件名,文件名····`
 `git add * (把当前工作区所有文件添加到暂存区)`
 `git add ./ (把当前工作区所有文件添加到暂存区)`

- 把暂存区的文件提交，生成一个版本 (需按自己的需求提交N次)
 `git commit -m "说明文字"`

- 查看用户名或邮箱等一系列设置  (可自行修改，按Q键退出)
 `git config --list`

- 查看文件版本
 `git log` (查看分支上都有哪些版本)
 `git log --oneline` (查看分支上的版本，相对简洁)

- 查看文件状态
 `git status`

- 查看文件版本id
 `git reflog`

- 回退版本(一旦回退版本，工作区的代码也会相应改变)
 `git reset --hard HEAD^/commit_id`
 `git reset --hard HEAD^ / HEAD~1` (表示回到上一个版本)
 `git reset --hard HEAD^^ / HEAD~2` (表示回到上上一个版本，依次类推)
 `git reset --hard 版本id` (回到指定的版本，一般用这个)
 **注：本地版本回退之后，远程仓库不回退**

- 回到未来版本(需通过git log查看版本id)
 `git reset --hard 版本id`

- 撤回在暂存区的文件
 `git reset HEAD --` (撤回所有)
 `git reset HEAD -- 文件名` (撤回指定文件)

- 克隆远程仓库的代码到本地
 `git clone 远程仓库地址`
 **注：一般第一次用 git clone 远程仓库地址 进行拷贝，以后都用 git pull 进行拉取**

- 克隆远程仓库指定分支的代码到本地
 `git clone -b 分支名 远程仓库地址`

- 从远程仓库拉取代码到本地(master为主分支)
 `git pull 远程仓库地址 master`
 **注：如果本地仓库与远程仓库同步后，只需输入 git pull 就可以直接进行拉取更新代码**

- 查看执行 git status 的结果的详细信息
 `git diff`

	- 尚未缓存的改动：`git diff`
	- 查看已缓存的改动： `git diff --cached`
	- 查看已缓存的与未缓存的所有改动：`git diff HEAD`
	- 显示摘要而非整个 diff：`git diff --stat`

- 推送本地代码到远程仓库(第一次同步时需输入密码)
 `git push 远程仓库地址 master`

- 一般提交方式

  ```powershell
  # 提交文件
  1. git status  # 查看当前文件状态；
  2. git add .  # 将文件添加到缓冲区（注意：add后面'.'表示全部）；
  3. git commit -m "content"  # 提交文件；
  4. git push origin master  # 将文件提交到远程分支（github）。
  ```

  
