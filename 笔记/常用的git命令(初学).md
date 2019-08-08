在工作中，经常用到 `git` , 不管托管在 `gitHub` 还是 `gitLab` 或者 `码云`，平时都是用可视化工具进行提交、推送，并没有用太多的命令进行操作。作为一个程序员，当然要学会用命令做东西啦，简单的记录下 `git` 日常命令，如果需要了解更多，请点击文章最下方链接进行访问。

### 配置 GItHub

- 首先进入`gitHub` `ssh`设置页 [https://github.com/settings/keys](https://github.com/settings/keys)
- 如果页面里面已经有了 可以点击 「delete」按钮把这些 `key` 先删除掉
- 点击 `New SSH key` ，进行创建，需要输入`Title` 和 `Key` , 我们目前没有 `key` , 往下看；
- 打开命令行工具
- **复制**并运行 `rm -rf ~/.ssh/*` 把现有的 `ssh key` 都删除掉，**注意不要打错一个字母哦**;
- 按回车三次，直到结束命令
- 运行 `cat ~/.ssh/id_rsa.pub` ，得到一串代码，完整的复制这串代码；
- 粘贴在我们创建的 `gitHub Key` 中，然后点击 `Add SSH key`
- 回到命令行工具，运行 `ssh -T git@github.com` 
- 如果您看到 `Hi jinchao1992! You've successfully authenticated, but GitHub does not provide shell access.` 证明我们生成 `SSH Key` 成功，如果提示别的，重复上述步骤再来一遍；

#### 注意

- 一台电脑只需要一个 `SSH Key`, 如果你换电脑了就需要重新生成 `key`，生成一个新的，再加到 `gitHub` 即可，不需要把之前的删除，可以跟之前的共存，这样我们两台电脑都可以用了；

### 配置 git

一共需要五行命令

- `git config --global user.name 你的英文名`  **设置用户名**
- `git config --global user.email 你的邮箱 ` **设置邮箱**
- `git config --global push.default matching`  **`push` 所有本地分支到远程仓库对应匹配的分支**
- `git config --global core.quotepath false` 使用 **`gitHub` 默认转义**
- `git config --global core.editor "vim"` **设置vim 为git默认编辑器**

### 使用 git

使用 `git` 有三种方式，具体如下：

1. 只在本地使用
2. 将本地仓库上传到 `GitHub`或者 `码云` 等远程仓库；
3. 直接从远程仓库下载 常用 `GitHub`

#### 只在本地使用

------

#### 1.1 初始化仓库

1. 我们首先建立一个测试目录 ：`mkdir git-demo-01`
2. 进入目录 `cd git-demo-01`
3. `git init` 初始化 `git` 会在我们当前的目录里 增加一个 `.git` 隐藏目录
4. `ls -la` 可以具体看到这个目录名字，
5. 在 `git-demo-01` 目录里面添加任意文件，我们先添加两个文件
   - `touch index.html`
   - `mkdir js`
   - `touch js/main.js`

6. 运行 `git status -sb` 可以看到文件前面有两个 ?? 号

   ```javascript
   ## Initial commit on master
   ?? js/
   ?? index.html
   ```

7. 可以使用 `git add` 命令将文件添加到 **暂存区**
   - 我们可以一个一个文件地 `add` ，当然在工作中，我们当然不可能是这样了，也可以一次性 `add`
   - `git add .` 意思是当前目录(.表示当前目录) 里面变动都记在暂存区；

8. 再次运行  `git status -sb` ，可以看到 ?? 变成了 A

   ```javascript
   ## Initial commit on master
   A js/
   A index.html
   ```

   A 的意思就是添加，告诉 `git` ，这些文件我要加在仓库里面；

  9 .  使用 `git commit -m "提交信息"` 可以将我们 `add` 过的内容正式提交 到**本地仓库（.git 就是本地仓库）** ，并可以添加一些注释信息，方便我们日后查看；

- 可以一个个 `commit` , 也可以一次性 `commit`
  - `git commit index.html -m "添加html"`
  - `git commit . -m "添加好多个文件"`
10. 再次运行 `git status -sb` 发现并没有其他改动了，所有文件都提交到本地仓库了
11. 我们还可以使用 `git log` 看到历史变动

#### 1.2 文件改动

如果想继续修改文件，该如何进行呢？

- `open js/main.js` 会使用默认的编辑器打开文件

- 我们在 `main.js` 中写入 `alert("小鱼儿的快乐生活")`

- 运行  `git status -sb` 发现提示中有一个 M

  ```javascript
  ## master
  M js/main.js
  ```

  这个 M 的意思就是 `Modified` ，表示这个文件被修改了

- 我们接着执行`git add 与 git commit -m ` 命令
- 再次运行 `git status -sb` 会发现没有变更了，所有变动都已经提交到本地仓库里面了。`git status -sb` `-sb` 的意思就是显示总结和分支。

#### 1.3 总结

总结下我们用到的git命令

1. `git init`初始化本地仓库 `git`
2. `git status -sb` 显示当前所有文件的状态
3. `git add "文件路径"` 用来将变动的添加到暂存区
4. `git commit -m "信息"` 用来提交本地 `.git` 库
5. `git log` 查看变更历史

#### 将本地仓库上传到 GitHub

------

如何将我们本地的仓库上传到 `github` 上呢？

1. 在 `GitHub` 上新建一个空仓库，名称随意，一般可以跟本地目录名称一致；
    ![](https://user-gold-cdn.xitu.io/2019/7/7/16bcba8162c51b2d?w=998&h=609&f=png&s=105951)

   按照上述截图，创建一个空的仓库

2. 点击创建按钮之后，`GitHub` 可以告诉你后续的操作，如图所示：
3. 运行以下命令
   1. `git remote add origin git@github.com:XXXXXXXXX/git-demo-01.git` 运行
   2. `git push -u origin master` , 运行

#### 直接在 GitHub 创建一个仓库，然后下载到本地

------

1. 在 `GitHub` 上新建一个仓库 `git-demo-02` , 这次可以不用创建空仓库了，而是自带 `README` 和 `Lisence` 的仓库，如下图：
    ![](https://user-gold-cdn.xitu.io/2019/7/7/16bcbac73b600f73?w=881&h=636&f=png&s=100898)
2. 远程仓库创建好了之后，我们可以使用 `git clone` 命令进行下载
3. 如下图所示，获取地址，必须是 `ssh`地址哦：
    ![](https://user-gold-cdn.xitu.io/2019/7/7/16bcbad6caca908c?w=1032&h=622&f=png&s=107228)
4. 打开命令行工具，找需要存放目录的文件夹，运行命令 `git clone "地址"`
5. 进入 `clone` 好的目录，运行 `ls -la` 就可以看到 `.git` 本地仓库了，然后我们就可以使用 `git` 命令

#### 如何上传更新

------

如果我们已经与远程仓库进行了链接，可以一步步运行以下命令就可以上传更新：

- `git add 文件路径`
- `git commit -m "info"`
- `git pull`
- `git push`

如：

1. `cd git-demo-01`
2. `touch index2.html`
3. `git add index2.html`
4. `git commit -m "新建html"`
5. `git pull`
6. `git push`

#### git ignore

------

在项目目录创建 `.gitignore` 文件就可以指定 「哪些文件不上传到远程仓库」, 比如 `.gitignore`

```javascript
/node_modules/
/.vscode/
```

这样就可以避免 `node_modules`  和 `.vscode` 目录上传到 `github`上了， 如果有别的文件夹也不想的话，可以直接在 `.gitignore` 添加；

------

上述就是我们平常用到的一些基本 `git` 命令，非常简单，当然如果需要应付工作中比较复杂的场景，比如代码冲突等，这些是不够的，所以可以看以下的参考文章进行学习；

## 2019.8.8 更新

* `git config --global --list` ，查看当前 `git` 全局配置；
* `git commit -v` ，查看当前更改的内容，并在提交时，可以写入详细内容；
* `git reset --hard '版本号'`  ，回退版本，版本号可以在 `git log` 命令中查到；
* `git reflog` ，查看版本历史，有回退过的 有之前提交的版本历史等；
* `git branch 分支名称` ，新建分支 ；
* `git checkout 分支名称`， 切换分支；
* `git branch -d 分支名称 分支名称` ，删除分支，删除多个分支，需要以空格分割；
* `git merge 分支名称`， 合并分支，合并多个分支需要用空格分割；**注意：合并分支是合并两个分支上不同的东西，并不是把 a 分支 合并到 b 分支**

### 资源

------

- [常用 Git 命令清单](http://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html)
- [读懂 diff - 阮一峰](http://www.ruanyifeng.com/blog/2012/08/how_to_read_diff.html)
- [搭建一个免费的，无限流量的Blog----github Pages和Jekyll入门](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html)
- [Git 菜鸟教程](http://www.runoob.com/git/git-install-setup.html)
- [廖雪峰的 Git 教程](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013743256916071d599b3aed534aaab22a0db6c4e07fd0000)



