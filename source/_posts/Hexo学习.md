---
title: Hexo学习笔记
abbrlink: 1257
date: 2024-01-01 00:00:00
tags:
---

## 日期 / 时间格式

Hexo 使用 [Moment.js](http://momentjs.com/) 来解析和显示时间。

| 参数             | 描述                                                         | 默认值       |
| :--------------- | :----------------------------------------------------------- | :----------- |
| `date_format`    | 日期格式                                                     | `YYYY-MM-DD` |
| `time_format`    | 时间格式                                                     | `HH:mm:ss`   |
| `updated_option` | 当 Front Matter 中没有指定 [`updated`](https://hexo.io/zh-cn/docs/variables#页面变量) 时 `updated` 的取值 | `mtime`      |

> updated_option
>
> `updated_option` 控制了当 Front Matter 中没有指定 `updated` 时，`updated` 如何取值：
>
> - `mtime`: 使用文件的最后修改时间。这是从 Hexo 3.0.0 开始的默认行为。
> - `date`: 使用 `date` 作为 `updated` 的值。可被用于 Git 工作流之中，因为使用 Git 管理站点时，文件的最后修改日期常常会发生改变
> - `empty`: 直接删除 `updated`。使用这一选项可能会导致大部分主题和插件无法正常工作。
>
> `use_date_for_updated` 选项已经在 v7.0.0+ 中被移除。请改为使用 `updated_option: 'date'`。

`date:` 选项的主要用途是在使用 Git 管理站点内容的时候，因为在这种情况下，文件的最后修改时间经常会改变。举例说，如果你在一个设备上编写了一篇博文，然后推送到 Git 仓库，当你从另一个设备克隆或拉取仓库更新时，文件的最后修改时间就会被更新为你克隆或拉取的那一刻，而不再是你实际上最后一次修改文件的时间。

所以，在此场景下，如果设置 `updated_option` 为 `date:`，Hexo 会将 Front Matter 中的 `date` 字段作为内容更新时间，而不是根据文件系统的文件最后修改时间来判定。这样可以更准确地反映出内容实际上的最后修改时间，而不受 Git 工作流的影响。

因此，如果你的博客内容是在多个设备上通过 Git 共享的，那么选择 `date:` 选项可能会是一个更好的选择。

---

```
$ hexo generate
```

| `-f`, `--force` | 强制重新生成文件 Hexo 引入了差分机制，如果 `public` 目录存在，那么 `hexo g` 只会重新生成改动的文件。 使用该参数的效果接近 `hexo clean && hexo generate` |
| --------------- | ------------------------------------------------------------ |

---

`wordcount is not a function / totalcount is not a function`
報錯`wordcount is not a function`

請檢查是否安裝了`wordcount`插件 `npm i --save hexo-wordcount`

---

`--save` 是一个 `npm install` 的选项，它的作用是将安装的模块保存到 `package.json` 文件的依赖项列表中。

如果你在安装模块时没有使用 `--save`，那么模块将会被安装到你的项目中，但 `package.json` 文件并不会记录这次安装。这意味着，如果你在新的环境下（例如新的开发机器或者服务器）重新依据 `package.json` 运行 `npm install`，那么这个模块并不会被安装。

一般来说，我们推荐在安装新的模块时使用 `--save`，以确保你的 `package.json` 文件始终能够准确地反映你的项目所需的所有依赖项，这对于实现项目的构建、部署、以及在多个环境之间的迁移都非常重要。

另一方面，如果你正在安装的模块只是临时使用，或者只在本地使用而不会影响生产环境，那么可以不使用 `--save` 选项。

---

hexo deploy时出现：ERROR Deployer not found: git

安装 Hexo 配置文件 (`_config.yml`) 中的 `git` 部署器。在 `_config.yml` 文件中，您需要配置 `deploy` 部分，指明使用的部署器类型以及必要的配置信息，如下所示：

```yml
   deploy:
     type: git
     repo: <repository url> # 你的 git 仓库地址
     branch: [branch]  # 通常为 "master" 或 "main"
```

是因为尚未安装 hexo-deployer-git，命令：`npm install hexo-deployer-git --save`

---

在Git中，`git add .` 和 `git add --all` 或者 `git add -A` 都可以用来将改动添加到暂存区，但它们的行为在处理删除操作上有明显的区别。

- `git add .` ： 会将当前目录下（包含子目录）所有新的和修改的文件添加到Git的暂存区，但不会包含已删除的文件。
- `git add --all` 或 `git add -A`：不仅会将所有新的和修改的文件添加到暂存区，同时也会将已删除的文件记录到暂存区。这样做的好处是，在下一次 `git commit` 时，Git将会记录这个删除操作。

这就是为什么当你删除了一些文件，而且你想要Git追踪并记录这个操作时，应该使用 `git add --all` 或 `git add -A`。

*`-A`必须大写？*

是的，`-A` 的确需要大写，所以正确的命令是 `git add -A`。

这个命令会将当前工作区里的所有变化（包括未跟踪的新文件、修改的已经跟踪的文件以及已删除的文件）加入到 Git 的暂存区。

如果你使用小写 `-a`，如 `git add -a`，实际上这个命令是不合法的，Git 会给出错误信息。小写的 `-a` 应当用在 `git commit` 中，作为 `git commit -a`，这会将所有已跟踪且被修改（不包括新文件）的文件提交。这就意味着 `git commit -a` 不会处理新文件，因为它们还没有被 Git 跟踪。

总结一下，`git add -A` 和 `git commit -a` 都是有用的命令，但它们的用途有所不同。大写的 `-A` 应当与 `git add` 一起使用，而小写的 `-a` 则应当与 `git commit` 一起使用。

---

如果你已经使用Hexo相关命令完成网站的发布，但在本地未找到Git的repository和branch，这是有可能的。Hexo是一个静态网站生成器，可以帮助你构建网站并发布到GitHub Pages等地方，但它本身并不会自动创建或管理Git库。

本地未找到repository和branch可能是因为：

1. 还未将文件夹初始化为Git repository。即使你已经使用了`hexo deploy`命令，也需要先用 `git init`命令将网站文件夹初始化为Git repository。
2. 如果你已经进行了`git init`，但还是找不到branch，可能是还未创建任何branch。一个新的Git repository默认会有一个名为 "master" (或在新版的Git中，可能会默认命名为 "main") 的branch。

你可以使用`git branch`命令来查看现有的所有branch，如果还未创建任何branch，你可以按需求创建。

所以，即使你已经使用Hexo发布了网站，可能仍需要手动创建和管理Git repository和branch。这会帮助你更好地管理你的网站源文件，并让你更方便地部署更新。

---

*在butterfly的配置文件中： *

*# Favicon（網站圖標） *

*favicon: /img/favicon.png *

*# Avatar (頭像) *

*avatar:  img: /img/avatar.jpg  *

*effect: false *

*指定路径中的 img 文件夹应该在哪里？*

在 Butterfly 主题的配置文件中，提到的 `/img/favicon.png` 和 `/img/avatar.jpg` 这样的路径，实际上是基于您的 Hexo 博客的 `source` 目录的。

换句话说，它们具体指向的是以下的两个位置：

- `source/img/favicon.png`，这是网站的图标。
- `source/img/avatar.jpg`，这是您的头像。

---

Hexo和Git是两种具有各自独特功能的工具，它们在一些方面有着共性，但在许多方面也大不相同。

1. **共性**：
   - **版本控制**：Hexo和Git的共性之处在于，它们都可以对你创建的项目进行版本控制。每当你对Hexo项目进行提交，或当你在Git中进行提交时，它们都会保存当前的项目状态以供将来查阅。
   - **GitHub支持**：当使用Hexo或Git时，你都可以将你的项目推送到GitHub，这对于进行代码共享和合作非常有用。
2. **异同**：
   - **目的**：Hexo是一个基于Node.js的静态博客框架，其主要目的是用于快速、轻松地创建静态博客网站。而Git则是一个分布式版本控制系统，旨在处理项目（无论大小）的所有内容，并提供协同合作的支持。
   - **工作原理**：在使用Hexo时，你会操作一些特定的命令来创建新的博客文章（例如hexo new "My New Post"），生成静态网页文件（hexo generate），或部署你的网站（hexo deploy）。在Git中，你会执行如add、commit、push等命令以跟踪文件的变化，保存这些变更，以及将这些变更推送到你的远程Git仓库。
   - **使用环境**：Hexo 和 Git 不仅可以同时使用，而且多数情况下它们会一同使用。Hexo 创建的静态网站通常会用 Git 进行版本控制，然后将代码库部署到 GitHub 或者其他代码托管平台。

所以，Hexo和Git虽然都是用来进行版本控制的工具，但它们的功能、使用方法和场景有很大的不同。在你的情况下，很可能你已经用Hexo成功地创建并部署了你的静态博客网站，然后用Vercel来处理你的GitHub仓库来进行在线展示，而Git则被用来管理和跟踪文件的更改。

---

在本地尚无任何分支的情况下：

1. 使用 `git checkout -b main` 本地创建并切换到 main 分支
2. 然后 `git remote add origin git@github.com:用户名/repo名.git` 添加远程库
3. 使用 `git remote -v` 查看是否添加成功（注意：即使远程并无此地址、此库，亦可成功创建）
4. 如果添加远程错误，使用 `git remote remove origin` 删除当前的远程设置，再用 2 法添加
5. 然后 `git add .`，`git commit -m "message"`，`git push -u origin main`



---

该错误是由于你的`pnpm-lock.yaml`文件和`package.json`文件不同步导致的。在持续集成（CI）环境中，`pnpm install`命令默认会使用`--frozen-lockfile`选项，这意味着它期望`pnpm-lock.yaml`文件是最新的，即与`package.json`文件同步。

要解决此问题，您可以在本地环境中运行`pnpm install`，以更新`pnpm-lock.yaml`文件，然后将更新后的文件推送到仓库。

这是一些可能有帮助的命令：

1. 运行 `pnpm install`：这将根据你的`package.json`文件更新你的`pnpm-lock.yaml`文件。

```bash
    pnpm install
```

---

`git push -f -u origin main`

- `git push`：这是一个 Git 命令，用于将本地仓库中的更改推送到远程仓库。
- `-f`：这是一个可选参数，代表 force（强制），在无法正常推送的情况下，强制将更改推送到远程仓库。需要谨慎使用此参数，因为可能会覆盖远程仓库中的改动。
- `-u`：这是一个可选参数，代表 set-upstream（设置上游），使用此参数将使得 Git 跟踪当前分支与指定的远程 branch（分支）之间的关系。以后你在这个分支上拉取（pull）或推送（push）时，就可以不必再明确指定远程 branch。
- `origin`：这通常是**远程仓库的默认别名**，当你克隆一个仓库时，Git 会自动为其创建这个别名。当然，你也可以自定义其他名称。
- `main`：这是你想要推送的**<u>本地</u>** branch 的名称。

有一种稍微安全一些的推送方式叫做 "force with lease"，你可以使用 `git push --force-with-lease` 来进行。这会在远程仓库包含你本地尚未知晓的更改时，阻止推送。这给了你一个机会来了解自己可能会覆盖什么，而不是盲目地覆盖远程的更改。

---

`hexo deploy` 会删除github sourcecode中的”非部署“文件，比如source文件夹，_config文件等。而且它不会触发sourcecode上的Actions（on push）。

也就是说，如果使用了hexo三件套，Github端sourcecode的main分支就会被删除一些重要的（备份用途如source）文件（夹），这时需要紧跟git三件套（add ./commit/push），再把删掉的东西补回来作为备份（实际上对于生成网站倒是没用，也是因此hexo d会删掉它们）。这时要注意的就是千万不能 git reset --hard或者 git pull 后覆盖本地！

---

`hexo new <layout> "文章标题"`中的文章标题如果也有英文双引号，需要加 `\` 转义符，使用反斜杠（\）是告诉命令行解析器，紧跟在它后边的字符（在这个情况下是双引号）应该被视为一个文本字符而不是一个特殊字符。

`hexo new "love u and me \"us\""`

实际上，生成的.md文件标题仍不会显示出标题内的双引号，直接成为` love-u-and-me-us.md`。这是因为Hexo对新文章的标题进行了格式化，将空格和特殊字符都转化为`-`。所以，即使你在控制台命令中输入`love u and me "us"`，实际生成的.md文件名会是`love-u-and-me-us.md`。这样做的目的是为了确保文件名的兼容性和可读性。

然而，实际上在你的.md文件中的标题（位于文件顶部的Front-matter部分）会保持你在`hexo new`命令中输入的原样格式，即`title: love u and me "us"` 。这会是你在网页上看到的标题。

---

安装`hexo-abbrlink`插件其实非常简单，只需要在你的Hexo项目目录中运行以下两条命令：

```bash
npm install hexo-abbrlink --save
```

这条命令会将`hexo-abbrlink`插件安装到你的Hexo项目中，并将依赖信息保存到`package.json`文件（'--save'选项的作用）。

```bash
npm install crc --save
```

这条命令会安装`crc`库，它是`hexo-abbrlink`插件的依赖库。

两条命令执行完后，你需要在项目的`_config.yml`文件中添加`abbrlink`的配置。这是一个基本的配置示例：

```yaml
abbrlink:
    alg: crc32    # 算法可以是 crc16，crc32 或者 md5
    rep: dec      # 表示方式可以是 dec，hex 或者 origin
```

在这个示例中，我们将`alg`(算法)设为了`crc32`，将`rep`(表示方式)设为`dec`。

当你下次运行`hexo new`创建文章时，Hexo会自动在Front-matter中添加`abbrlink`字段，并按照你在`_config.yml`中设置的算法和表示方式生成一个独有的`abbrlink`值。

---

Hexo的网页渲染好像是靠JS。大致猜测了一个简化流程：

- 预处理：通过 Front-matter 和文件属性等获得文章类型、标题、时间等信息
- 渲染：将文章信息以及 Markdown 原文喂给渲染器，转成 HTML
- 生成：将一系列的文章信息和 HTML 喂给主题，产生最终的静态网站

渲染这个很好理解，自带的 `hexo-renderer-marked` 渲染器就是通过 `hexo.extend.renderer.register()` 注册了 Markdown 文件的渲染 ([ref](https://github.com/hexojs/hexo-renderer-marked/blob/master/index.js))，Hexo 会在遇到 .md 等后缀的文件的时候就会调用 [`renderer.js`](https://github.com/hexojs/hexo-renderer-marked/blob/master/lib/renderer.js#L120) 里的对应函数，把 .md 转发到 `marked.Renderer` 完成 Markdown 到 HTML 的转换。

生成静态网站的话，可以认为 Hexo 的主题就是一堆 HTML 模板，Hexo 自己集成了几套模板引擎的接口，主题开发者需要按照一定的目录结构来编写主题。完成所有文章的渲染后，Hexo 把文章数据和 HTML 一并喂给模板引擎，产生的就是一个静态网站。

这么看其实还是非常简单的，而且 Hexo 定义了足够多的 [Filter](https://hexo.io/api/filter)（其实我觉得叫做 Hook 更合适），可以在渲染和生成的前后做很多自定义的事情，这么一来可定制性就基本足够了。

### 初始化 Hexo 博客

使用 `hexo init` 初始化一个新的博客，会产生如下的一个目录结构：

```text
|- .gitignore
|- _config.yml
|- package.json
|- scaffolds/
|- source/
   |- _drafts/
   |- _posts/
|- themes/
   |- landscape/
```

- `.gitignore` 是 Hexo 帮我们创建的，里边包含了 Node.js 相关的文件还有 Hexo 的生成目录等条目
- `_config.yml` 是 [Hexo 的配置文件](https://hexo.io/docs/configuration)
- `package.json` 定义了生成 Hexo 博客的一些基础依赖包
- `scaffolds` 是 `hexo new` 时会用到的模板，与生成的静态网页无关，这里可以删掉
- `source/` 是存储博客正文 Markdown 的目录
- `themes/` 是存储博客主题源码的目录，现在包含的是官方默认的 Landscape 主题

当前目录还不是一个 Git repo......

那来吧，先随便写一个 `README.md` 作为 initial commit 这样：

```shell-session
$ git init
Initialized empty Git repository in .git/
$ echo "# oreo.life-src" > README.md
$ git add README.md
$ git commit -m "Initial commit"
```

然后把我们现在什么都没有的 Hexo 博客提交上去：

```bash
git commit -a -m "Initialize Hexo blog (without theme)"
```

### 使用 git submodules 添加主题

上面提到了，`hexo init` 的时候会在 `themes/landscape` 放一个默认主题。由于我们不用，就把它删了。我们现在要把新的 Fluid 主题加到我们的 Repo 里。

当然可以像 `hexo` 工具一样直接拷贝一份 [Fluid 主题的 release](https://github.com/fluid-dev/hexo-theme-fluid/releases/) 到 `themes/` 下，但是显然「博客的源码包含主题源码的一份拷贝」这件事是非常不合理的，想更新主题版本或者是更换主题的话，会给博客带来一堆不应出现的 commit。于是，我们选择 Git Submodules 来引用 Fluid Repo，这样带来的好处是博客源码只需要记录主题地址和版本 (commit)，其他全部交给 git 来处理，此外博客 Repo 的体积也会相应变小。

直接使用 submodule 命令添加 Fluid 主题源码，并 checkout 到当前的最新版本（需要在 [release 页面](https://github.com/fluid-dev/hexo-theme-fluid/releases/) 查看，本文撰写时为 `v1.8.2`）

```shell-session
$ git submodule add https://github.com/fluid-dev/hexo-theme-fluid themes/fluid
Cloning into 'themes/fluid'...
Resolving deltas: 100% (2849/2849), done.
$ cd themes/fluid
$ git checkout v1.8.2
Note: checking out 'v1.8.2'.
HEAD is now at c5ff53a :label: 发布 1.8.2 版本
```

这样，我们就在 `themes/fluid` 目录添加了一份主题。在博客源码的目录下，我们看到了这样一个 `.gitmodules` 文件：

```ini
[submodule "themes/fluid"]
	path = themes/fluid
	url = https://github.com/fluid-dev/hexo-theme-fluid.git
```

它代表我们在 `themes/fluid` 目录下，以 submodules 的形式添加了 Fluid 源码 Repo。具体指向的是哪个 Commit，感兴趣的话可以研究一下 `.git/modules/themes/fluid/` 里的文件内容，这里不详述。

修改 `_config.yml` 下的 `theme` 字段：

```yaml
theme: fluid
```

然后执行 `hexo generate`，会发现 Hexo 可以正确在 `public` 目录下生成一份带有主题和 Hello World 博文的静态网页。

然后顺手交个代码吧...

```bash
git commit -a -m "Add fluid theme by submodule"
```

## 配置 GitHub Actions

事实上到这里，我们已经实现了「在配置好的环境下，`hexo g` 可以正确生成一份静态网页」这件事。那我们在 GitHub Actions 里做的事情就可以概括成下面的流程了：

1. Clone 博客源码
2. 配置 Node.js 环境
3. 配置 Hexo 环境
4. 使用 `hexo g` 生成静态网页
5. 将 `public/` 目录下的静态网页部署到 GitHub Pages

我们先完成 1-4。

### GitHub Actions 的语法

在这里强烈建议先阅读 [GitHub Actions 官方指南](https://docs.github.com/en/actions/configuring-and-managing-workflows/configuring-a-workflow)。本文不会很详细地介绍 Actions 的基础知识。

{% hideToggle 官方的 Workflow 配置样例 %}

```
name: Greet Everyone
*# This workflow is triggered on pushes to the repository.*
on: [push]
jobs:
  build:
    *# Job name is Greeting*
    name: Greeting
    *# This job runs on Linux*
    runs-on: ubuntu-latest
    steps:
      *# This step uses GitHub's hello-world-javascript-action: https://github.com/actions/hello-world-javascript-action*
      \- name: Hello world
        uses: actions/hello-world-javascript-action@v1
        with:
          who-to-greet: 'Mona the Octocat'
        id: hello
      *# This step prints an output (time) from the previous step's action.*
      \- name: Echo the greeting's time
        run: echo 'The time was ${{ steps.hello.outputs.time }}.'
```

{% endhideToggle %}

看这个 Workflow 配置，其实它非常简单。`name` 定义的是名字，会显示在 Repo 的 Actions 页面；`on` 字段定义的是触发条件，GitHub Actions 定义了一系列的 [Workflow 触发器](https://docs.github.com/en/actions/reference/events-that-trigger-workflows)，例如 Pull Request / Push / 手动触发等；`jobs` 则定义了一个 Workflow 的具体会做什么，我们主要关注 `build/steps` 这个字段。

`build` 也是个名字。`steps` 是一个数组，在执行 `build` 这个任务时，会按照先后顺序触发 `steps` 里的任务。每一项任务可以是使用 `uses` 定义的，调用 GitHub 预置的 (也可以是第三方提供的) 一些函数来进行环境配置、下载源码等操作；也可以是使用 `run` 定义的 Shell 脚本。

### 编写生成博客静态网页的 Workflow 代码

我们先回顾一下需求：在更新博客源码，或者说更新 Markdown 文档时，自动根据博客源码产生静态网页。那翻译成 GitHub 的说法就可以是，「当向 `master` 分支提交代码时，自动触发 Workflow 来生成网页」。那么，配置文件的框架就出来了：

```
name: Generate Hexo Blog
on:
  push:
    branches:
      - master
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      # To fill...
```

下面我们依次向 `jobs/build/steps` 中添加我们的任务。

第一步，我们需要把博客的源码 clone 到运行环境中。使用 GitHub 官方提供的 [`actions/checkout@v2`](https://github.com/actions/checkout) （现已是v4）来 clone 源码：

```
- name: Checkout source
  uses: actions/checkout@v2
  with:
    submodules: 'true'
```

注意，这里如果不指定 Repo 名称，则默认是当前 Repo，也就是博客源码 Repo。此外，由于我们使用了 submoudule 来配置主题，所以 `submodules` 需要设置成 `true`。这里使用字符串的原因是似乎 [官方 README](https://github.com/actions/checkout#usage) 里写的就是个字符串，这里为了避免产生奇奇怪怪的问题所以就 follow 了。

第二步，配置 Node.js 环境。使用 GitHub 官方提供的 [`actions/setup-node@v1`](https://github.com/actions/setup-node) （现已是v4）来配置：

```yaml
- name: Setup Node.js
  uses: actions/setup-node@v1
  with:
    node-version: '12'
```

我们在这里选用最新 LTS，Node.js v12。

第三步，配置 Hexo 环境。首先我们需要安装 Hexo 的命令行工具 `hexo-cli`，此外还需要根据我们 Repo 里的 `package-lock.json` 来安装一个完全一致的 `node_modules` 以还原正确的环境。

```yaml
- name: Setup Hexo environment
  run: |
    npm install -g hexo-cli
    npm ci
```

这里 `run: |` 中的 `|` 是 YAML 的多行字符串语法。

注意，我们这里用的是 `npm ci` 而不是 `npm install`。按照 [官方文档](https://docs.npmjs.com/cli/ci.html)，`npm ci` 会移除现有的 `node_modules` 目录后，按照 `package-lock.json` 的内容来安装依赖包以确保环境完全一致，并且不会修改 `package.json` 和 `package-lock.json`。

到这里，我们就把 Hexo 的环境设置好了。现在我们在当前目录有了博客源码和原始 Markdown 文件、系统中有了 Node.js 和 Hexo、`node_modules` 下有了所有我们需要的依赖，接下来就是：

第四步，生成博客静态网页。

```yaml
- name: Generate pages
  run: |
    hexo generate
    ls -R public/
```

非常简单。到这里就大功告成了。

由于我们还没有添加部署任务，所以先加一个 `ls` 显示 `public/` 下的所有文件，用来确认我们的网页是否被正确生成。

### 将 Workflow 部署到 GitHub Actions

这一步也非常非常简单。把上述 YAML 文件放到 Repo 的 `.github/workflows/` 下，任意命名，保存，提交 Commit。

{% hideToggle 完整的 Workflow 配置文件 %}

```
name: Generate Hexo Blog
on:
  push:
    branches:
      - master
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout source
      uses: actions/checkout@v4
      with:
        submodules: 'true'
    - name: Setup Node.js
      uses: actions/setup-node@v4
      with:
        node-version: '18'
    - name: Setup hexo environment
      run: |
        npm install -g hexo-cli
        npm ci
    - name: Generate pages
      run: |
        hexo generate
        ls -R public/
```

{% endhideToggle %}

然后再添加 Git remote 指向在 GitHub 用于储存博客源码的 Repo 地址（注意不是 Pages 对应的 Repo），执行 `git push` 即可。

稍等片刻，就可以在 Repo 的 Actions 页面下看到一个新触发的任务。不出意外，log 中将显示 Hexo 成功生成了一份静态网页。大功告成~

---

*<u>搭建hexo博客时样式总是报404加载不出来</u>*
对于如何搭建hexo博客网上有很多关于使用hexo + github pages搭建个人博客的博客，按照博客内容也都可以搭建起来。运行后在本地服务器都可以实现访问，但是通过域名访问时却遇到样式加载不出来的问题，查询该问题也没找到清晰的解决方法，在此进行总结。

通过控制台查看样式文件报404，是因为url地址不对。
需要修改_config.yml文件中的url地址和根目录

```
# URL

## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'

url: https://banjingwei.github.io/ban.github.io
root: /ban.github.io/
permalink: :year/:month/:day/:title/
permalink_defaults:
```

开始确认是这里的问题却不清楚url和root分别该是什么
url是github pages给我们分配的网址

root是我们搭建该博客的仓库名!

这样就可以加载到样式文件了，我们的博客也就展现在了我们面前。

---

| 计划        | 存储   | 分钟数（每月） |
| :---------- | :----- | :------------- |
| GitHub Free | 500 MB | 2,000          |

github Free用户private repo使用Actions的限制。（public repo无限制）

---

## 标签外挂：

**note:**

```
{% note [color] [icon] [style] %}
Any content (support inline tags too.io).
{% endnote %}
```

| 名稱  | 用法                                                         |
| ----- | ------------------------------------------------------------ |
| color | 【可选】顔色(default / blue / pink / red / purple / orange / green) |
| icon  | 【可选】可配置自定义icon (只支持 fontawesome 图标, 也可以配置 no-icon ) |
| style | 【可选】可覆盖配置中的 style（simple/modern/flat/disabled）  |

![image-20240108203217051](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240108203217051.png)



**hideToggle:**

```
{% hideToggle display,bg,color %}
content
{% endhideToggle %}
```

| 模块    | 功能                         |
| ------- | ---------------------------- |
| content | 要隐藏的内容                 |
| display | 展开前框中显示的文字（可选） |
| bg      | 框的背景颜色（可选）         |
| color   | 框显示的文字的颜色（可选）   |



**Tab:**

```
{% tabs Unique name, [index] %}
<!-- tab [Tab caption] [@icon] -->
Any content (support inline tags too).
<!-- endtab -->
{% endtabs %}
```

Unique name   : Unique name of tabs block tag without comma.
                Will be used in #id's as prefix for each tab with their index numbers.
                If there are whitespaces in name, for generate #id all whitespaces will replaced by dashes.
                Only for current url of post/page must be unique!
[index]       : Index number of active tab.
                If not specified, first tab (1) will be selected.
                If index is -1, no tab will be selected. It's will be something like spoiler.
                Optional parameter.
[Tab caption] : Caption of current tab.
                If not caption specified, unique name with tab index suffix will be used as caption of tab.
                If not caption specified, but specified icon, caption will empty.
                Optional parameter.
[@icon]       : FontAwesome icon name (full-name, look like 'fas fa-font')
                Can be specified with or without space; e.g. 'Tab caption @icon' similar to 'Tab caption@icon'.
                Optional parameter.



**hideInline:**

格式如下，仅限隐藏文字，content 不能包含英文逗号，可用 `&sbquo;` 代替逗号：

```
{% hideInline content,display,bg,color %}
```

| 模块  | 功能 |
|  ---  | ------  |
| content |要隐藏的文本内容|
| display |展示前按钮显示的文字（可选） |
| bg	     |按钮的背景颜色（可选）            |
| color	|按钮显示的文字的颜色（可选） |

![image-20240108204838112](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240108204838112.png)

点击`别点我`后出现`今日事，今日毕`；点击`上面真秀`后出现`上面太花里胡哨了`。



**hideBlock:**

提供一个`按钮` ，而它可以隐藏`文字` 、`图片` 、`代码块`等，`dispaly` 不能包含英文逗号，可用` &sbquo; `代替：

```
{% hideBlock display,bg,color %}
content
{% endhideBlock %}
```

| 模块    | 功能                         |
| ------- | ---------------------------- |
| content | 要隐藏的内容                 |
| display | 展开前框中显示的文字（可选） |
| bg      | 框的背景颜色（可选）         |
| color   | 框显示的文字的颜色（可选）   |

![image-20240108205805965](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240108205805965.png)

![image-20240108205823228](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240108205823228.png)



**mermaid功能标签：**

使用 mermaid 标签可以绘制 Flowchart（流程图）、Sequence diagram（时序图 ）、Class Diagram（类别图）、State Diagram（状态图）、Gantt（甘特图）和 Pie Chart（圆形图），具体可以查看 [mermaid 文档](https://mermaid-js.github.io/mermaid/#/)
在 Butterfly 的主题配置文档中找到并修改或添加块:

```
mermaid:
  enable: true
  # built-in themes: default/forest/dark/neutral
  theme: default
```

mermaid 标签不允许嵌套于一些隐藏属性的标签外挂（如 tag-hide 內的标签外挂和 tabs 标签外挂），也不能压缩代码，那会导致 mermaid 图示无法正常显示，使用时请留意。

写法：

```
{% mermaid %}
內容
{% endmermaid %}
```

举个例子：

```
{% mermaid %}
pie
    title 项目语言比重
    "Java" : 42.96
    "C#" : 50.05
    "Python" : 10.01
    "Javascript" :  5
{% endmermaid %}
```

效果：

![image-20240108211053582](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240108211053582.png)





**按钮标签 链接按钮标签：**

写法：

```
{% btn [url],[text],[icon],[color] [style] [layout] [position] [size] %}
```

| 参数|功能                                                     |
| ----------|-------------------------------------------------- |
| [url]|链接                                                    |
| [text]|按钮文字                                               |
| [icon]|[可选] 图标                                            |
| [color]|[可选] 按钮背景颜色(默认style时）                     |
|                                 |按钮字体和边框颜色(outline时)|
|                     |default/blue/pink/red/purple/orange/green|
| [style]|[可选] 按钮样式 默认实心                              |
|                                                  |outline/留空|
| [layout]|[可选] 按钮布局 默认为line                           |
|                                                    |block/留空|
| [position]|[可选] 按钮位置 前提是设置了layout為block 默认为左边 |
|                                             |center/right/留空|
| [size]|[可选] 按钮大小                                        |
|                                                   |larger/留空|

---

原本设置的Waline（默认）和Giscus双评论系统，忽然发现Waline在每个页面下的评论框没有了，没法输入任何评论。

改过post.pug和head.pug，甚至还查看了waline.pug，都没有效果。最终通过网页F12检查判断，还是加载地址出了问题。

其实waline的网页加载主要靠3个地址的设置（主题配置文件）：

1. 先设定use什么，我这里采用了双评论系统![image-20240109094438960](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240109094438960.png)
2. 还有两个分别是网页加载的css和js文件，需要在最末的option（其实是 CDN options）相关选项中进行设置

![image-20240109094704820](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240109094704820.png)

保存后再生成网站，waline的评论框就正常加载出来了。



在加载的网页中，Giscus评论亦有报错：

![image-20240109095831098](https://cdn.jsdelivr.net/gh/spritenee/images@main/Pico/202401/image-20240109095831098.png)

这是因为Giscus去获取所述页面的Discussions（实际上就是用户使用Giscus的评论），但没有Discussions，就会报错。无其他影响。

---

**解决网页控制台其他报错：**

1. busuanzi 不蒜子计数，很长时间打开网页就在转圈。F12查看，控制台，显示`ERR_SSL_PROTOCOL_ERROR`。这种一般是指SSL协议（安全证书）出了问题，还以为到期了，结果一番鼓捣下来发现无效。在配置文件的`inject` HEAD里插入`- <script defer src="https://busuanzi.9420.ltd/js"></script>`也无效。
   后来偶然发现（chatGPT提醒）可能是VPN的问题，关掉VPN就不报错！于是，在VPN中添加规则：
   V2rayN --> 设置 --> 路由设置 --> 绕过大陆 --> （domain那个direct），添加`domain:busuanzi.ibruce.info,`，确定即可。

   对了，如果不喜欢busuanzi，将Waline的`pageview: false`改成`true`即可替代busuanzi计数。

   

2. 引入了Google Analytics，在layout.pug文件中的
   ```
   doctype html
   html(lang=config.language data-theme=theme.display_mode class=htmlClassHideAside)
     head
       include ./head.pug
   ```

   下方添加了
   ```
   # script与上方include对齐
       script.
         <!-- Google tag (gtag.js) -->
         (function(){
           var script = document.createElement('script');
           script.src = "https://www.googletagmanager.com/gtag/js?id=G-EEZG901XK6";
           script.async = true;
           document.head.appendChild(script);
         })();
         window.dataLayer = window.dataLayer || [];
         function gtag() { dataLayer.push(arguments); }
         gtag('js', new Date());
         gtag('config', 'G-EEXXXXXXX6');
   ```

   再将`G-EEXXXXXXX6` （Measurment ID）添加到主题_config的
   ```
   # Google Analytics
   # https://analytics.google.com/analytics/web/
   google_analytics: 这里
   ```

   添加好后同样面临着 1 所述问题，需要如上添加两个direct domain:
   `domain:google-analytics.com,
   domain:googletagmanager.com,`

   确定即正常，不再报错。

   

   这么说来，很可能waline评论框不出现也是因为vpn的问题！只是上面是用另一个CDN地址给解决了。

   ---

   将Butterfly主题转换为Submodule（子模块），方便将来主题升级。即，以themes/butterfly文件夹为Butterfly主题的**Git 根目录**，在此新建一个“小天地”，自主完成 git push/pull 相关命令，再配合 Github Actions，实现本地代码少、生成量小的效果，都转移到网上自动部署了。

   1. 进入 themes/butterfly 文件夹，直接在主网站根目录下cmd：
      `git submodule add https://github.com/jerryc127/hexo-theme-butterfly themes/butterfly`
      此命令会在主网站目录的themes文件夹下新建一个butterfly文件夹。

   2. `cd themes/butterfly`
      `git tag` 查看 butterfly 的各个版本（Tag）
      `git checkout 4.12` 签出最新版，现在处于`'detached HEAD'`状态

      `git checkout -b butterfly` 创建并切换到 butterfly 分支
      编辑 butterfly/layout 中的 post.pug 文件，以适应 custom.css 的选择器（中文缩进效果实现），保存
      `git remote set-url origin git@github.com:spritenee/sourcecode.git`，设置 github 远程库地址
      `git add .`

      `git commit -m "将整个butterfly和修改后的post.pug文件push到sourcecode库的butterfly分支"`
      `git push -u origin butterfly`  将本地butterfly分支push到（默认）名为origin的远程库的同名 (butterfly) 分支，并将后者设为上游

   3. 退回到主网站根目录
      `git add .`
      `git commit -m "将刚才的butterfly文件夹和post.pug变更都提交"`
      `git push origin main`

      有个`git submodule update --remote --merge`命令，在主网站根目录下运行，可更新子模块并完成合并。

      {% hideToggle %}

      ​	`git submodule`：这是 Git 子模块命令，子模块允许你将 Git 仓库作为另一个 Git 仓库的子目录。

      ​	`update`：这是一个更新子模块到最新提交的命令。

      ​	`--remote`：使用这个选项，Git 会进入每个子模块，并拉取最新的改动，以更新每个子模块。

      ​	`--merge`：这是合并选项，Git 将尝试合并子模块仓库的上游改动。

      ​	综上所述，`git submodule update --remote --merge` 命令将进入每个子模块，拉取改动并尝试合并它们。
      {% endhideToggle %}

   要想恢复**已损坏**的子模块，或者想将子模块更新到其最新的内容，你可以尝试以下步骤：

   ​	首先，导航到你的主网站根目录
   
   ​	然后初始化子模块（如果还没有初始化）：
   
   ```shell
   git submodule init
   ```
   
   ​	更新子模块：
   
   ```shell
   git submodule update
   ```
   
   以上命令将会克隆子模块（如果还未克隆）并且切换到在你的主项目中为每个子模块记录的提交。
   
   如果你想要更新子模块到远程仓库的最新状态，你需要导航到子项目目录并执行pull命令：
   
   ```shell
   cd themes/butterfly
   git pull origin HEAD
   ```
   
   在Windows操作系统下你可以使用以下命令来删除`themes/butterfly`目录：
   
   ```shell
   rmdir /s /q themes\butterfly
   ```
   
   上述命令说明：
   
   - `/s` 参数会删除指定目录及其所有子目录。
   - `/q` 参数用于安静模式，不会请求确认删除目录树。
   
   
   
   已经成功地克隆了子模块到本地。现在如果你想从 GitHub 的源代码库 `butterfly` 分支拉取更新到本地，可以按照以下步骤操作：
   
   ​	首先，进入你所克隆的子模块目录 `themes/butterfly`：
   
   ```shell
   cd themes\butterfly
   ```
   
   ​	确保你的本地 Git 知道 `butterfly` 分支存在。检查远程引用：
   
   ```shell
   git fetch origin
   ```
   
   ​	切换到 `butterfly` 分支：
   
   ```shell
   git checkout butterfly
   ```
   
   ​	从远程库拉取最新的更新：
   
   ```shell
   git pull origin butterfly
   ```
   
   以上步骤应该可以帮你从 `butterfly` 分支拉取最新的更新。
   
   
   
   想从GitHub的源代码库`butterfly`分支拉取更新到本地，请按照以下步骤操作：
   
   1. 首先，确保你的本地Git仓库已添加了正确的远程仓库：
   
   ```shell
       git remote add upstream https://github.com/your-source-repo-link.git
   ```
   
   ​	在上述命令中，请将`https://github.com/your-source-repo-link.git`替换为实际的源代码库地址。
   
   2. 获取远程仓库的所有分支的更新：
   
   ```shell
       git fetch upstream
   ```
   
   ​	确定你在本地仓库的当前位置，然后切换到你想要更新的分支（例如`butterfly`）：
   
   ```shell
       git checkout butterfly
   ```
   
   ​	将远程仓库的更改合并到本地分支：
   
   ```shell
       git merge upstream/butterfly
   ```
   
   ​	最后，将更改推送到你的GitHub仓库：
   
   ```shell
       git push
   ```
   
   以上步骤应该可以帮你从源代码库的`butterfly`分支拉取最新的更新。
   
   
   
   
   
   custom.css放入**主网站根目录下的self**中，将 _config.butterfly.yml 中的 Inject 设置为：
   
   ```
   inject:
     head:
        - <link rel="stylesheet" href="/self/custom.css">
   ```
   
   主网站_config.yaml中的配置似乎**无效**：
   ```
   # 在这里添加你的自定义样式表
   custom_css:
     - /css/custom.css
   ```
   
   ---
   
   **如何运行ps1脚本?**
   
   运行 PowerShell 脚本的步骤如下：
   
   1. 打开 PowerShell 控制台。在 Windows 中，你可以在开始菜单中搜索 "PowerShell"，然后点击 "Windows PowerShell"。在 Mac 或 Linux 中，你可能需要安装 PowerShell Core，然后在终端中输入 "pwsh" 来打开。
   2. 通过 cd 命令导航到脚本所在的文件夹。例如，如果脚本位于 `D:\Scripts`，那么你需要输入 `cd D:\Scripts`。
   3. 在 PowerShell 中，有一个称为 "执行策略"（Execution Policy）的安全机制，用来控制是否允许运行脚本。在默认情况下，PowerShell 可能不允许运行脚本。为了能运行脚本，你需要通过以下命令来临时改变执行策略：`Set-ExecutionPolicy -ExecutionPolicy Bypass -Scope Process`。这会在当前 PowerShell 进程中，允许运行任何脚本。
   4. 运行脚本。假设你的脚本文件名为 `script.ps1`，你可以通过输入 `.\script.ps1` 来运行脚本。
   5. 当脚本结束时，你可以在 PowerShell 控制台中看到输出结果。
   
   注意，运行非熟悉来源的脚本时一定要小心，确定你理解脚本的功能，并确信它来自可信的来源。
   
   ---
   
   使用`hexo generate --debug`命令可找出生成过程中出现错误的文件。
   
   ---
   
   
