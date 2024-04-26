### Git 基本知识及命令

---

#### 一、初始化设置

```bash
git config --global user.name "YOur name"                   配置用户名
git config --global user.email "Your email address"			配置邮箱
git config --global credential store						存储配置--避免每次操作输入密码
```

#### 二、创建仓库

```bash
git init <project-name>							创建一个本地仓库（省略pro-name则在当前目录创建）
git clone <url>									从远端拉取一个仓库
```

仓库创建成功后，会在当前目录或`project-name`下生成一个 `.git`目录，如下所示：

<div style="text-align:center">
    <img src="C:\Users\user\Desktop\git_lea\images\.git.png" alt=".git目录">
</div>

每个文件夹和文件的作用如下：

1. `hooks`

   该目录下存放着一些脚本文件，这些脚本在`Git`操作时被调用，如提交、合并等，可以用于自定义和控制`Git`操作。

2. `objects`

   该目录是`Git`版本控制中一个非常重要的目录，负责存储所有版本控制的对象，确保数据的完整性和可靠性。

   > info：该子目录包含一些全局的配置文件和锁定文件；
   >
   > pack：该子目录存储`Git`使用的压缩包，这些压缩包包含了多个对象，用于减少存储空间和提高效率；
   >
   > 哈希：此外，`objects`中还包含着大量的以两个字符为前缀的子目录，如’01‘，’02‘等等。这些子目录用于存储对象的实际数据。每个对象都有一个唯一的`SHA-1`哈希值作为其名字，并存储在对应的子目录中。
   >
   > 在这些哈希目录中，存储了`Git`仓库中的所有对象，包括提交对象、树对象、文件对象等。每个对象都已二进制格式存储在对应的哈希目录中，文件内容经过压缩和哈希计算。

3. `refs`

   该目录是`Git`仓库中存储引用的地方。在`Git`中，引用是指向提交对象（commits）、分支（branches）、标签（tags）等重要对象的指针。

   > heads：该目录存储了所有分支的引用，每个文件名对应一个分支名称，文件内容是该分支最新提交的`SHA-1`哈希值；
   >
   > tags：该目录存储了所有标签的引用，每个文件名对应一个标签名称，文件内容是该标签指向对象的`SHA-1`哈希值；
   >
   > remotes：如果本地仓库与一个或多个远程仓库进行了连接，那么该目录下会有与每个远程仓库相关的引用。每个远程仓库都有一个与其名字对应的子目录，子目录下存储了该远程仓库的分支引用。

   这些引用文件简化了在`Git`仓库中查找和管理分支、标签和远程引用的过程。

4. `config`

   存储了仓库的配置信息，这些信息配置信息可以是全局的、用户级别的，或者特定仓库级别的。

5. `HEAD`

   它指向当前活动的分支（或直接指向特定的提交）。

   > + 指向分支
   >
   >   指向当前工作的分支，如果切换分支，它也会随之更新
   >
   > + 指向提交
   >
   >   如果你检出了一个特定的提交而不是一个分支，`HEAD`会指向该提交的哈希值
   >
   > + 分离头状态
   >
   >   在某些情况下，`HEAD`可能处于’分离头‘状态，这意味着它指向了一个特定的提交，儿童不是一个分支。**此时，任何新的提交都不会更新任何分支。**如果你想在此状态下保存你的更改，你可能需要新建一个分支或切换回现有的分支。

#### 三、四个区域及文件状态

1. 四大区域

   + 工作区（Working Directory）

     本地工作区域，即本地电脑中实际看到的目录

   + 暂存区（Stage / Index）

     暂存区也叫索引，用来临时存放未提交的内容，一般在`.git`目录下的`index`中

   + 本地仓库（Repository）

     `Git`在本地的版本仓库，仓库信息存放在`.git`目录中

   + 远程仓库（Remote Repository）

     托管在远程服务器上的仓库，如`GitHub`、`GitLab`、`Gitee`等

2. 三种文件状态

   + 已修改（Modified）

     修改了但是没有保存到Stage的文件

   + 已暂存（Staged）

     修改了且已保存到Stage的文件

   + 已提交（Committed）

     Stage中的文件提交到本地仓库后的状态

#### 四、文件添加及提交

<div style="text-align:center">
    <img src="C:\Users\user\Desktop\git_lea\images\workflow.png" alt="工作流程">
</div>

1. Working --> Stage

   ```bash
   git add <filename / foldername>					添加一个文件或目录
   git add a.txt b.txt								一次添加多个文件
   git add *.txt									使用通配符添加所有txt文件
   git add --all / git add .                       添加工作区所有文件
   ```

2. Stage --> Working

   ```bash
   git rm --cached <filename>						从Stage中移除
   ```

3. Stage --> Local Repository

   ``` bash
   git commit -m "message"							提交所有Stage中的文件
   ```

4. Else

   ```bash
   git status								查看文件状态，列出还未提交的新的或修改后的文件
   git log --oneline						查看提交历史，--oneline表示简介模式
   ```

5. reset

   ``` bash
   git reset --soft <commit-id>			删除commit记录，Working和Stage保持不变
   git reset --mixed <commit-id> 默认	   删除commit记录，修改Stage到id，Working保持不变	
   git reset --hard <commit-id>			删除commit记录，修改Working和Stage到id
   ```

   







