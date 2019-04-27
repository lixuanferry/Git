# Git教程

Git是一个分布式版本控制系统

## 一、安装Git

在Windows上安装完成之后打开“Git Bash”，每个机器需要自报家门：你的名字和Email

	git config --global user.name "Your Name"
	git config --global user.email "email@example.com"

## 二、创建仓库

- 选择一个合适的地方，创建一个空目录：

        mkdir learngit
        cd learngit
        pwd

    `pwd`命令用于显示当前目录。

- 把这个目录变成Git可以管理的仓库：

        git init

## 三、把文件添加到仓库

- 编写一个`readme.txt`文件，放到`learngit`目录下：

        Git is a version control system.
        Git is free software.
- 把文件添加到仓库：

    ```
    git add readme.txt
    ```

- 把文件提交到仓库：

        git commit -m "wrote a readme file"

因为`commit`可以一次提交很多文件，所以你可以多次`add`不同的文件。

## 四、修改文件

- `git status`命令可以查看仓库的当前状态。
- 如果`git status`命令告诉你文件被修改过，使用`git diff`命令可以查看文件具体修改了什么内容：

        git diff readme.txt

- 提交修改是和提交文件同样的两步：

        git add readme.txt
        
        git commit -m "add distributed"

## 五、版本回退

- `git log`命令显示从最近到最远的提交日志，如果嫌输出的信息太多，可以加上`--pretty=oneline`参数：

        git log --pretty=oneline

- 在Git中，用`HEAD`表示当前版本，上一个版本就是`HEAD^`，上上一个版本就是`HEAD^^`，往上100个版本可以写成`HEAD~100`。

- 使用`git reset`命令回退到上一个版本：

        git reset --hard HEAD^

- 如果想要回到最新的版本，需要找到那个版本的`commit id`(版本号)，版本号不需要写全，Git会自动去找：

        git reset --hard 1094a

- `git reflog`命令可以查看历史命令，以便找到未来版本的`commit id`。

## 六、撤销修改

- 当你想直接丢弃工作区的修改，使用`git checkout --readme.txt`命令。
- 如果你已经将文件添加到了暂存区，这时候想丢弃修改，分两步：

        git reset HEAD readme.txt
        
        git checkout --readme.txt

## 七、删除文件

如果一个文件已经提交到版本库中：

- 从版本库中删除文件：

        git rm test.txt
        
        git commit -m "remove test.txt"

- 如果删错了，使用`git checkout --test.txt`命令用版本库中的版本替换工作区中的版本。

## 八、远程仓库

免费Git远程仓库——github

- 在用户主目录下，查看有没有`.ssh`目录，再查看里面是否有`id_rsa`和`id_rsa.pub`两个文件，如果没有则需要创建SSH KEY，然后一路回车，使用默认值，也不需要创建密码：

        ssh-keygen -t rsa -C "youremail@example.com"

- 登录GitHub，打开“Settings”页面中的“SSH and GPG keys”选项，然后点击“New SSH key”按钮，填写任意TItle，在Key文本框里粘贴`id_rsa.pub`文件中的内容。

## 九、添加远程仓库

- 登录GitHub，创建一个远程库，根据GitHub的提示，在本地的`learngit`仓库下运行命令：

        git remote add origin https://github.com/lixuanferry/Git.git

- 把本地库的所有内容推送到远程库，由于远程库是空的，第一次推送`master`分支时，加上了`-u`参数，Git不但会把本地的`master`分支内容推送的远程新的`master`分支，还会把本地的`master`分支和远程的`master`分支关联起来，在以后的推送或者拉取时就可以简化命令：

        git push -u origin master

- 从现在起，只要本地做了修改，就可以通过命令：

        git push origin master

​       把本地`master`分支的最新修改推送至GitHub。