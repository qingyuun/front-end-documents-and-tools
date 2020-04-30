# npm 模块管理器

* [npm 模块管理器](#npm-模块管理器)
  *  1 [简介](#简介)
  *  2 [npm init](#npm-init)
  *  3 [npm set](#npm-set)
  *  4 [npm config](#npm-config)
  *  5 [npm info](#npm-info)
  *  6 [npm search](#npm-search)
  *  7 [npm list](#npm-list)
  *  8 [npm install](#npm-install)
     * 8.1 [基本用法](#基本用法)
     * 8.2 [安装不同版本](#安装不同版本)
     * 8.3 [避免系统权限](#避免系统权限)
  *  9 [npm update & npm uninstall](#npm-update-npm-uninstall)
  *  10 [npm run](#npm-run)
     *  10.1 [参数](#参数)
     *  10.2 [scripts 脚本命令最佳实践](#scripts-脚本命令最佳实践)
     *  10.3 [pre- & post- 脚本](#pre-post-脚本)
     *  10.4 [内部变量](#内部变量)
     *  10.5 [通配符](#通配符)
  *  11 [npm link](#npm-link)
  *  12 [npm bin](#npm-bin)
  *  13 [npm adduser](#npm-adduser)
  *  14 [npm publish](#npm-publish)
  *  15 [npm deprecate](#npm-deprecate)
  *  16 [npm owner](#npm-owner)
  *  17 [其他命令](#其他命令)
     *  17.1 [npm home & npm repo](#npm-home-npm-repo)
     *  17.2 [npm outdated](#npm-outdated)
     *  17.3 [npm prune](#npm-prune)
     *  17.4 [npm shrinkwrap](#npm-shrinkwrap)
  

## 简介

{-&nbsp;&nbsp;npm&nbsp;&nbsp;-}&nbsp;&nbsp;有两层含义。一层含义是Node的开放式模块登记和管理系统，网址为[npmjs.com](https://npmjs.com)。另一层含义是Node默认的模块管理器，是一个命令行下的软件，用来安装和管理Node模块。

&nbsp;&nbsp;{-&nbsp;&nbsp;npm&nbsp;&nbsp;-}&nbsp;&nbsp;不需要单独安装。在安装Node的时候，会连带一起安装&nbsp;&nbsp;{-&nbsp;&nbsp;npm&nbsp;&nbsp;-}&nbsp;&nbsp;。但是，Node附带的&nbsp;&nbsp;{-&nbsp;&nbsp;npm&nbsp;&nbsp;-}&nbsp;&nbsp;可能不是最新版本，最好用下面的命令，更新到最新版本。

```

$ npm install npm@latest -g

```
上面的命令中，&nbsp;&nbsp;{-&nbsp;&nbsp;@latest&nbsp;&nbsp;-}&nbsp;&nbsp;表示最新版本，&nbsp;&nbsp;{-&nbsp;&nbsp;-g&nbsp;&nbsp;-}&nbsp;&nbsp;表示全局安装。所以，命令的主干是&nbsp;&nbsp;{-&nbsp;&nbsp;npm install npm&nbsp;&nbsp;-}&nbsp;&nbsp;，也就是使用&nbsp;&nbsp;{-&nbsp;&nbsp;npm&nbsp;&nbsp;-}&nbsp;&nbsp;安装自己。之所以可以这样，是因为&nbsp;&nbsp;{-&nbsp;&nbsp;npm&nbsp;&nbsp;-}&nbsp;&nbsp;本身与Node的其他模块没有区别。

然后，运行下面的命令，查看各种信息。

```

# 查看 npm 命令列表
$ npm help

# 查看各个命令的简单用法
$ npm -l

# 查看 npm 的版本
$ npm -v

# 查看 npm 的配置
$ npm config list -l

```

## npm init

{-&nbsp;&nbsp;npm init&nbsp;&nbsp;-}&nbsp;&nbsp;用来初始化生成一个新的&nbsp;&nbsp;{-&nbsp;&nbsp;package.json&nbsp;&nbsp;-}&nbsp;&nbsp;文件。它会向用户提问一系列问题，如果你觉得不用修改默认配置，一路回车就可以了。

如果使用了&nbsp;&nbsp;{-&nbsp;&nbsp;-f&nbsp;&nbsp;-}&nbsp;&nbsp;（代表force）、&nbsp;&nbsp;{-&nbsp;&nbsp;-y&nbsp;&nbsp;-}&nbsp;&nbsp;（代表yes），则跳过提问阶段，直接生成一个新的&nbsp;&nbsp;{-&nbsp;&nbsp;package.json&nbsp;&nbsp;-}&nbsp;&nbsp;文件。

```

$ npm init -y

```

## npm set

&nbsp;&nbsp;{-&nbsp;&nbsp;npm set&nbsp;&nbsp;-}&nbsp;&nbsp;用来设置环境变量。

```

$ npm set init-author-name 'Your name'
$ npm set init-author-email 'Your email'
$ npm set init-author-url 'http://yourdomain.com'
$ npm set init-license 'MIT'

```

上面命令等于为&nbsp;&nbsp;{-&nbsp;&nbsp;npm init&nbsp;&nbsp;-}&nbsp;&nbsp;设置了默认值，以后执行&nbsp;&nbsp;{-&nbsp;&nbsp;npm init&nbsp;&nbsp;-}&nbsp;&nbsp;的时候，&nbsp;&nbsp;{-&nbsp;&nbsp;package.json&nbsp;&nbsp;-}&nbsp;&nbsp;的作者姓名、邮件、主页、许可证字段就会自动写入预设的值。这些信息会存放在用户主目录的&nbsp;&nbsp;{-&nbsp;&nbsp; ~/.npmrc&nbsp;&nbsp;-}&nbsp;&nbsp;文件，使得用户不用每个项目都输入。如果某个项目有不同的设置，可以针对该项目运行&nbsp;&nbsp;{-&nbsp;&nbsp;npm config&nbsp;&nbsp;-}&nbsp;&nbsp;。


```

$ npm set save-exact true

```

上面命令设置加入模块时，&nbsp;&nbsp;{-&nbsp;&nbsp;package.json&nbsp;&nbsp;-}&nbsp;&nbsp;将记录模块的确切版本，而不是一个可选的版本范围。

## npm config

```
$ npm config set prefix $dir

```

上面的命令将指定的&nbsp;&nbsp;{-&nbsp;&nbsp;$dir&nbsp;&nbsp;-}&nbsp;&nbsp;目录，设为模块的全局安装目录。如果当前有这个目录的写权限，那么运行&nbsp;&nbsp;{-&nbsp;&nbsp;npm install&nbsp;&nbsp;-}&nbsp;&nbsp;的时候，就不再需要&nbsp;&nbsp;{-&nbsp;&nbsp;sudo&nbsp;&nbsp;-}&nbsp;&nbsp;命令授权了。


```

$ npm config set save-prefix ~

```

上面的命令使得&nbsp;&nbsp;{-&nbsp;&nbsp;npm install --save&nbsp;&nbsp;-}&nbsp;&nbsp;和&nbsp;&nbsp;{-&nbsp;&nbsp;npm install --save-dev&nbsp;&nbsp;-}&nbsp;&nbsp;安装新模块时，允许的版本范围从克拉符号（&nbsp;&nbsp;{-&nbsp;&nbsp;^&nbsp;&nbsp;-}&nbsp;&nbsp;）改成波浪号（&nbsp;&nbsp;{-&nbsp;&nbsp;~&nbsp;&nbsp;-}&nbsp;&nbsp;），即从允许小版本升级，变成只允许补丁包的升级。


```

$ npm config set init.author.name $name
$ npm config set init.author.email $email

```
上面命令指定使用&nbsp;&nbsp;{-&nbsp;&nbsp;npm init&nbsp;&nbsp;-}&nbsp;&nbsp;时，生成的&nbsp;&nbsp;{-&nbsp;&nbsp;package.json&nbsp;&nbsp;-}&nbsp;&nbsp;文件的字段默认值。

## npm info

&nbsp;&nbsp;{-&nbsp;&nbsp;npm info&nbsp;&nbsp;-}&nbsp;&nbsp;命令可以查看每个模块的具体信息。比如，查看underscore模块的信息。

```

$ npm info underscore
{ name: 'underscore',
  description: 'JavaScript\'s functional programming helper library.',
  'dist-tags': { latest: '1.5.2', stable: '1.5.2' },
  repository:
   { type: 'git',
     url: 'git://github.com/jashkenas/underscore.git' },
  homepage: 'http://underscorejs.org',
  main: 'underscore.js',
  version: '1.5.2',
  devDependencies: { phantomjs: '1.9.0-1' },
  licenses:
   { type: 'MIT',
     url: 'https://raw.github.com/jashkenas/underscore/master/LICENSE' },
  files:
   [ 'underscore.js',
     'underscore-min.js',
     'LICENSE' ],
  readmeFilename: 'README.md'}
  
```
上面命令返回一个JavaScript对象，包含了underscore模块的详细信息。这个对象的每个成员，都可以直接从info命令查询。

```

$ npm info underscore description
JavaScript's functional programming helper library.

$ npm info underscore homepage
http://underscorejs.org

$ npm info underscore version
1.5.2

```
## npm search

&nbsp;&nbsp;{-&nbsp;&nbsp;npm search&nbsp;&nbsp;-}&nbsp;&nbsp;命令用于搜索npm仓库，它后面可以跟字符串，也可以跟正则表达式。

```

$ npm search <搜索词>

```

下面是一个例子。

```

$ npm search node-gyp
// NAME                  DESCRIPTION
// autogypi              Autogypi handles dependencies for node-gyp projects.
// grunt-node-gyp        Run node-gyp commands from Grunt.
// gyp-io                Temporary solution to let node-gyp run `rebuild` under…
// ...

```
## npm list

&nbsp;&nbsp;{-&nbsp;&nbsp;npm list&nbsp;&nbsp;-}&nbsp;&nbsp;命令以树型结构列出当前项目安装的所有模块，以及它们依赖的模块。

```

$ npm list

```

加上global参数，会列出全局安装的模块。

```

$ npm list -global

```

&nbsp;&nbsp;{-&nbsp;&nbsp;npm list&nbsp;&nbsp;-}&nbsp;&nbsp;命令也可以列出单个模块。

```

$ npm list underscore

```

## npm install

### 基本用法

### 安装不同版本

### 避免系统权限

## npm update & npm uninstall

## npm run

### 参数

### scripts 脚本命令最佳实践

### pre- & post- 脚本

### 内部变量

### 通配符

## npm link

## npm bin

## npm adduser

## npm publish

## npm deprecate

如果想废弃某个版本的模块，可以使用&nbsp;&nbsp;{-&nbsp;&nbsp;npm deprecate&nbsp;&nbsp;-}&nbsp;&nbsp;命令。

$ npm deprecate my-thing@"< 0.2.3" "critical bug fixed in v0.2.3"
运行上面的命令以后，小于&nbsp;&nbsp;{-&nbsp;&nbsp;0.2.3&nbsp;&nbsp;-}&nbsp;&nbsp;版本的模块的&nbsp;&nbsp;{-&nbsp;&nbsp;package.json&nbsp;&nbsp;-}&nbsp;&nbsp;都会写入一行警告，用户安装这些版本时，这行警告就会在命令行显示。

## npm owner

模块的维护者可以发布新版本。&nbsp;&nbsp;{-&nbsp;&nbsp;npm owner&nbsp;&nbsp;-}&nbsp;&nbsp;命令用于管理模块的维护者。

```

# 列出指定模块的维护者
$ npm owner ls <package name>

# 新增维护者
$ npm owner add <user> <package name>

# 删除维护者
$ npm owner rm <user> <package name>

```

## 其他命令

### npm home & npm repo

&nbsp;&nbsp;{-&nbsp;&nbsp;npm home&nbsp;&nbsp;-}&nbsp;&nbsp;命令可以打开一个模块的主页，&nbsp;&nbsp;{-&nbsp;&nbsp;npm repo&nbsp;&nbsp;-}&nbsp;&nbsp;命令则是打开一个模块的代码仓库。

```

$ npm home $package
$ npm repo $package

```

这两个命令不需要模块先安装。

### npm outdated

&nbsp;&nbsp;{-&nbsp;&nbsp;npm outdated&nbsp;&nbsp;-}&nbsp;&nbsp;命令检查当前项目所依赖的模块，是否已经有新版本。

```

$ npm outdated

```
它会输出当前版本（current version）、应当安装的版本（wanted version）和最新发布的版本（latest version）。

### npm prune

&nbsp;&nbsp;{-&nbsp;&nbsp;npm prune&nbsp;&nbsp;-}&nbsp;&nbsp;检查当前项目的&nbsp;&nbsp;{-&nbsp;&nbsp;node_modules&nbsp;&nbsp;-}&nbsp;&nbsp;目录中，是否有&nbsp;&nbsp;{-&nbsp;&nbsp;package.json&nbsp;&nbsp;-}&nbsp;&nbsp;里面没有提到的模块，然后将所有这些模块输出在命令行。

```

$ npm prune

```

### npm shrinkwrap

&nbsp;&nbsp;{-&nbsp;&nbsp;npm shrinkwrap&nbsp;&nbsp;-}&nbsp;&nbsp;的作用是锁定当前项目的依赖模块的版本。

```

$ npm shrinkwrap

```

运行该命令后，会在当前项目的根目录下生成一个&nbsp;&nbsp;{-&nbsp;&nbsp;npm-shrinkwrap.json&nbsp;&nbsp;-}&nbsp;&nbsp;文件，内容是&nbsp;&nbsp;{-&nbsp;&nbsp;node_modules&nbsp;&nbsp;-}&nbsp;&nbsp;目录下所有已经安装的模块，以及它们的精确版本。

下次运行&nbsp;&nbsp;{-&nbsp;&nbsp;npm install&nbsp;&nbsp;-}&nbsp;&nbsp;命令时，&nbsp;&nbsp;{-&nbsp;&nbsp;npm&nbsp;&nbsp;-}&nbsp;&nbsp;发现当前目录下有&nbsp;&nbsp;{-&nbsp;&nbsp;npm-shrinkwrap.json&nbsp;&nbsp;-}&nbsp;&nbsp;文件，就会只安装里面提到的模块，且版本也会保持一致。