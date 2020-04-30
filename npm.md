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

&nbsp;&nbsp;{-&nbsp;&nbsp;npm run&nbsp;&nbsp;-}&nbsp;&nbsp;为每条命令提供了&nbsp;&nbsp;{-&nbsp;&nbsp;pre-&nbsp;&nbsp;-}&nbsp;&nbsp;和&nbsp;&nbsp;{-&nbsp;&nbsp;post-&nbsp;&nbsp;-}&nbsp;&nbsp;两个钩子（hook）。以&nbsp;&nbsp;{-&nbsp;&nbsp;npm run lint&nbsp;&nbsp;-}&nbsp;&nbsp;为例，执行这条命令之前，npm会先查看有没有定义prelint和postlint两个钩子，如果有的话，就会先执行&nbsp;&nbsp;{-&nbsp;&nbsp;npm run prelint&nbsp;&nbsp;-}&nbsp;&nbsp;，然后执行&nbsp;&nbsp;{-&nbsp;&nbsp;npm run lint&nbsp;&nbsp;-}&nbsp;&nbsp;，最后执行&nbsp;&nbsp;{-&nbsp;&nbsp;npm run postlint&nbsp;&nbsp;-}&nbsp;&nbsp;。

```

{
  "name": "myproject",
  "devDependencies": {
    "eslint": "latest"
    "karma": "latest"
  },
  "scripts": {
    "lint": "eslint --cache --ext .js --ext .jsx src",
    "test": "karma start --log-leve=error karma.config.js --single-run=true",
    "pretest": "npm run lint",
    "posttest": "echo 'Finished running tests'"
  }
}

```

上面代码是一个&nbsp;&nbsp;{-&nbsp;&nbsp;package.json&nbsp;&nbsp;-}&nbsp;&nbsp;文件的例子。如果执行&nbsp;&nbsp;{-&nbsp;&nbsp;npm test&nbsp;&nbsp;-}&nbsp;&nbsp;，会按下面的顺序执行相应的命令。

```

> pretest
> test
> posttest

```
如果执行过程出错，就不会执行排在后面的脚本，即如果prelint脚本执行出错，就不会接着执行lint和postlint脚本。

下面是一个例子。

```

{
  "test": "karma start",
  "test:lint": "eslint . --ext .js --ext .jsx",
  "pretest": "npm run test:lint"
}

```

上面代码中，在运行&nbsp;&nbsp;{-&nbsp;&nbsp;npm run test&nbsp;&nbsp;-}&nbsp;&nbsp;之前，会自动检查代码，即运行&nbsp;&nbsp;{-&nbsp;&nbsp;npm run test:lint&nbsp;&nbsp;-}&nbsp;&nbsp;命令。

下面是一些常见的&nbsp;&nbsp;{-&nbsp;&nbsp;pre-&nbsp;&nbsp;-}&nbsp;&nbsp;和&nbsp;&nbsp;{-&nbsp;&nbsp;post-&nbsp;&nbsp;-}&nbsp;&nbsp;脚本。

```
> prepublish：发布一个模块前执行。
> postpublish：发布一个模块后执行。
> preinstall：用户执行npm install命令时，先执行该脚本。
> postinstall：用户执行npm install命令时，安装结束后执行该脚本，通常用于将下载的源码编译成用户需要的格式，比如有些模块需要在用户机器上跟本地的C++模块一起编译。
> preuninstall：卸载一个模块前执行。
> postuninstall：卸载一个模块后执行。
> preversion：更改模块版本前执行。
> postversion：更改模块版本后执行。
> pretest：运行npm test命令前执行。
> posttest：运行npm test命令后执行。
> prestop：运行npm stop命令前执行。
> poststop：运行npm stop命令后执行。
> prestart：运行npm start命令前执行。
> poststart：运行npm start命令后执行。
> prerestart：运行npm restart命令前执行。
> postrestart：运行npm restart命令后执行。

```

对于最后一个&nbsp;&nbsp;{-&nbsp;&nbsp;npm restart&nbsp;&nbsp;-}&nbsp;&nbsp;命令，如果没有设置&nbsp;&nbsp;{-&nbsp;&nbsp;restart&nbsp;&nbsp;-}&nbsp;&nbsp;脚本，&nbsp;&nbsp;{-&nbsp;&nbsp;prerestart&nbsp;&nbsp;-}&nbsp;&nbsp;和&nbsp;&nbsp;{-&nbsp;&nbsp;postrestart&nbsp;&nbsp;-}&nbsp;&nbsp;会依次执行stop和start脚本。

另外，不能在&nbsp;&nbsp;{-&nbsp;&nbsp;pre&nbsp;&nbsp;-}&nbsp;&nbsp;脚本之前再加&nbsp;&nbsp;{-&nbsp;&nbsp;pre&nbsp;&nbsp;-}&nbsp;&nbsp;，即&nbsp;&nbsp;{-&nbsp;&nbsp;prepretest&nbsp;&nbsp;-}&nbsp;&nbsp;脚本不起作用。

注意，即使Npm可以自动运行&nbsp;&nbsp;{-&nbsp;&nbsp;pre&nbsp;&nbsp;-}&nbsp;&nbsp;和&nbsp;&nbsp;{-&nbsp;&nbsp;post&nbsp;&nbsp;-}&nbsp;&nbsp;脚本，也可以手动执行它们。

```

$ npm run prepublish

```

下面是&nbsp;&nbsp;{-&nbsp;&nbsp;post install&nbsp;&nbsp;-}&nbsp;&nbsp;的例子。

```

{
  "postinstall": "node lib/post_install.js"
}

```

上面的这个命令，主要用于处理从Git仓库拉下来的源码。比如，有些源码是用TypeScript写的，可能需要转换一下。

下面是&nbsp;&nbsp;{-&nbsp;&nbsp;publish&nbsp;&nbsp;-}&nbsp;&nbsp;钩子的一个例子。

```

{
  "dist:modules": "babel ./src --out-dir ./dist-modules",
  "gh-pages": "webpack",
  "gh-pages:deploy": "gh-pages -d gh-pages",
  "prepublish": "npm run dist:modules",
  "postpublish": "npm run gh-pages && npm run gh-pages:deploy"
}

```

上面命令在运行&nbsp;&nbsp;{-&nbsp;&nbsp;npm run publish&nbsp;&nbsp;-}&nbsp;&nbsp;时，会先执行Babel编译，然后调用Webpack构建，最后发到Github Pages上面。

以上都是npm相关操作的钩子，如果安装某些模块，还能支持Git相关的钩子。下面以[husky](https://github.com/typicode/husky)模块为例。

```

$ npm install husky --save-dev

```

安装以后，就能在&nbsp;&nbsp;{-&nbsp;&nbsp;package.json&nbsp;&nbsp;-}&nbsp;&nbsp;添加&nbsp;&nbsp;{-&nbsp;&nbsp;precommit&nbsp;&nbsp;-}&nbsp;&nbsp;、&nbsp;&nbsp;{-&nbsp;&nbsp;prepush&nbsp;&nbsp;-}&nbsp;&nbsp;等钩子。

```

{
    "scripts": {
        "lint": "eslint yourJsFiles.js",
        "precommit": "npm run test && npm run lint",
        "prepush": "npm run test && npm run lint",
        "...": "..."
    }
}

```

类似作用的模块还有&nbsp;&nbsp;{-&nbsp;&nbsp;pre-commit&nbsp;&nbsp;-}&nbsp;&nbsp;、&nbsp;&nbsp;{-&nbsp;&nbsp;precommit-hook&nbsp;&nbsp;-}&nbsp;&nbsp;等。

### 内部变量

scripts字段可以使用一些内部变量，主要是package.json的各种字段。

比如，package.json的内容是&nbsp;&nbsp;{-&nbsp;&nbsp;{"name":"foo", "version":"1.2.5"}&nbsp;&nbsp;-}&nbsp;&nbsp;，那么变量&nbsp;&nbsp;{-&nbsp;&nbsp;npm_package_name&nbsp;&nbsp;-}&nbsp;&nbsp;的值是foo，变量&nbsp;&nbsp;{-&nbsp;&nbsp;npm_package_version&nbsp;&nbsp;-}&nbsp;&nbsp;的值是1.2.5。

```

{
  "scripts":{
    "bundle": "mkdir -p build/$npm_package_version/"
  }
}

```

运行&nbsp;&nbsp;{-&nbsp;&nbsp;npm run bundle&nbsp;&nbsp;-}&nbsp;&nbsp;以后，将会生成&nbsp;&nbsp;{-&nbsp;&nbsp;build/1.2.5/&nbsp;&nbsp;-}&nbsp;&nbsp;子目录。

&nbsp;&nbsp;{-&nbsp;&nbsp;config&nbsp;&nbsp;-}&nbsp;&nbsp;字段也可以用于设置内部字段。

```

  "name": "fooproject",
  "config": {
    "reporter": "xunit"
  },
  "scripts": {
    "test": "mocha test/ --reporter $npm_package_config_reporter"
  }
  
```

上面代码中，变量&nbsp;&nbsp;{-&nbsp;&nbsp;npm_package_config_reporter&nbsp;&nbsp;-}&nbsp;&nbsp;对应的就是reporter。

### 通配符

npm的通配符的规则如下。

```

> * 匹配0个或多个字符= 

> 匹配1个字符

> [...] 匹配某个范围的字符。如果该范围的第一个字符是!或^，则匹配不在该范围的字符。

> !(pattern|pattern|pattern) 匹配任何不符合给定的模式

> ?(pattern|pattern|pattern) 匹配0个或1个给定的模式

> +(pattern|pattern|pattern) 匹配1个或多个给定的模式

> *(a|b|c) 匹配0个或多个给定的模式

> @(pattern|pat*|pat?erN) 只匹配给定模式之一

> ** 如果出现在路径部分，表示0个或多个子目录。

```

## npm link

开发NPM模块的时候，有时我们会希望，边开发边试用，比如本地调试的时候，&nbsp;&nbsp;{-&nbsp;&nbsp;require('myModule')&nbsp;&nbsp;-}&nbsp;&nbsp;会自动加载本机开发中的模块。Node规定，使用一个模块时，需要将其安装到全局的或项目的&nbsp;&nbsp;{-&nbsp;&nbsp; node_modules &nbsp;&nbsp;-}&nbsp;&nbsp;目录之中。对于开发中的模块，解决方法就是在全局的&nbsp;&nbsp;{-&nbsp;&nbsp;node_modules&nbsp;&nbsp;-}&nbsp;&nbsp;目录之中，生成一个符号链接，指向模块的本地目录。

&nbsp;&nbsp;{-&nbsp;&nbsp;npm link&nbsp;&nbsp;-}&nbsp;&nbsp;就能起到这个作用，会自动建立这个符号链接。

请设想这样一个场景，你开发了一个模块&nbsp;&nbsp;{-&nbsp;&nbsp;myModule&nbsp;&nbsp;-}&nbsp;&nbsp;，目录为&nbsp;&nbsp;{-&nbsp;&nbsp;src/myModule&nbsp;&nbsp;-}&nbsp;&nbsp;，你自己的项目&nbsp;&nbsp;{-&nbsp;&nbsp;myProject&nbsp;&nbsp;-}&nbsp;&nbsp;要用到这个模块，项目目录为&nbsp;&nbsp;{-&nbsp;&nbsp;src/myProject&nbsp;&nbsp;-}&nbsp;&nbsp;。首先，在模块目录&nbsp;&nbsp;{-&nbsp;&nbsp;（src/myModule）&nbsp;&nbsp;-}&nbsp;&nbsp;下运行&nbsp;&nbsp;{-&nbsp;&nbsp;npm link&nbsp;&nbsp;-}&nbsp;&nbsp;命令。

```

src/myModule$ npm link

```

上面的命令会在NPM的全局模块目录内，生成一个符号链接文件，该文件的名字就是&nbsp;&nbsp;{-&nbsp;&nbsp;package.json&nbsp;&nbsp;-}&nbsp;&nbsp;文件中指定的模块名。

```

/path/to/global/node_modules/myModule -> src/myModule

```
这个时候，已经可以全局调用&nbsp;&nbsp;{-&nbsp;&nbsp;myModule&nbsp;&nbsp;-}&nbsp;&nbsp;模块了。但是，如果我们要让这个模块安装在项目内，还要进行下面的步骤。

切换到项目目录，再次运行&nbsp;&nbsp;{-&nbsp;&nbsp;npm link&nbsp;&nbsp;-}&nbsp;&nbsp;命令，并指定模块名。

```

src/myProject$ npm link myModule

```
上面命令等同于生成了本地模块的符号链接。

```

src/myProject/node_modules/myModule -> /path/to/global/node_modules/myModule

```

然后，就可以在你的项目中，加载该模块了。

```

var myModule = require('myModule');

```

这样一来，&nbsp;&nbsp;{-&nbsp;&nbsp;myModule&nbsp;&nbsp;-}&nbsp;&nbsp;的任何变化，都可以直接反映在&nbsp;&nbsp;{-&nbsp;&nbsp;myProject&nbsp;&nbsp;-}&nbsp;&nbsp;项目之中。但是，这样也出现了风险，任何在&nbsp;&nbsp;{-&nbsp;&nbsp;myProject&nbsp;&nbsp;-}&nbsp;&nbsp;目录中对&nbsp;&nbsp;{-&nbsp;&nbsp;myModule&nbsp;&nbsp;-}&nbsp;&nbsp;的修改，都会反映到模块的源码中。

如果你的项目不再需要该模块，可以在项目目录内使用&nbsp;&nbsp;{-&nbsp;&nbsp;npm unlink&nbsp;&nbsp;-}&nbsp;&nbsp;命令，删除符号链接。

```

src/myProject$ npm unlink myModule

```

## npm bin

&nbsp;&nbsp;{-&nbsp;&nbsp;npm bin&nbsp;&nbsp;-}&nbsp;&nbsp;命令显示相对于当前目录的，Node模块的可执行脚本所在的目录（即.bin目录）。

```

# 项目根目录下执行
$ npm bin
./node_modules/.bin

```

## npm adduser

&nbsp;&nbsp;{-&nbsp;&nbsp;npm adduser&nbsp;&nbsp;-}&nbsp;&nbsp;用于在npmjs.com注册一个用户。

```

$ npm adduser
Username: YOUR_USER_NAME
Password: YOUR_PASSWORD
Email: YOUR_EMAIL@domain.com

```

## npm publish

&nbsp;&nbsp;{-&nbsp;&nbsp;npm publish&nbsp;&nbsp;-}&nbsp;&nbsp;用于将当前模块发布到&nbsp;&nbsp;{-&nbsp;&nbsp;npmjs.com&nbsp;&nbsp;-}&nbsp;&nbsp;。执行之前，需要向&nbsp;&nbsp;{-&nbsp;&nbsp;npmjs.com&nbsp;&nbsp;-}&nbsp;&nbsp;申请用户名。

```

$ npm adduser

```

如果已经注册过，就使用下面的命令登录。

```

$ npm login

```

登录以后，就可以使用&nbsp;&nbsp;{-&nbsp;&nbsp;npm publish&nbsp;&nbsp;-}&nbsp;&nbsp;命令发布。

```

$ npm publish

```

如果当前模块是一个beta版，比如&nbsp;&nbsp;{-&nbsp;&nbsp;1.3.1-beta.3&nbsp;&nbsp;-}&nbsp;&nbsp;，那么发布的时候需要使用&nbsp;&nbsp;{-&nbsp;&nbsp;tag&nbsp;&nbsp;-}&nbsp;&nbsp;参数，将其发布到指定标签，默认的发布标签是&nbsp;&nbsp;{-&nbsp;&nbsp;latest&nbsp;&nbsp;-}&nbsp;&nbsp;。

```

$ npm publish --tag beta

```

如果发布私有模块，模块初始化的时候，需要加上&nbsp;&nbsp;{-&nbsp;&nbsp;scope&nbsp;&nbsp;-}&nbsp;&nbsp;参数。只有npm的付费用户才能发布私有模块。

```

$ npm init --scope=<yourscope>

```

如果你的模块是用ES6写的，那么发布的时候，最好转成ES5。首先，需要安装Babel。

```

$ npm install --save-dev babel-cli@6 babel-preset-es2015@6

```

然后，在&nbsp;&nbsp;{-&nbsp;&nbsp;package.json&nbsp;&nbsp;-}&nbsp;&nbsp;里面写入&nbsp;&nbsp;{-&nbsp;&nbsp;build&nbsp;&nbsp;-}&nbsp;&nbsp;脚本。

```

"scripts": {
  "build": "babel source --presets babel-preset-es2015 --out-dir distribution",
  "prepublish": "npm run build"
}

```

运行上面的脚本，会将&nbsp;&nbsp;{-&nbsp;&nbsp;source&nbsp;&nbsp;-}&nbsp;&nbsp;目录里面的ES6源码文件，转为&nbsp;&nbsp;{-&nbsp;&nbsp;distribution&nbsp;&nbsp;-}&nbsp;&nbsp;目录里面的ES5源码文件。然后，在项目根目录下面创建两个文件&nbsp;&nbsp;{-&nbsp;&nbsp;.npmignore&nbsp;&nbsp;-}&nbsp;&nbsp;和&nbsp;&nbsp;{-&nbsp;&nbsp;.gitignore&nbsp;&nbsp;-}&nbsp;&nbsp;，分别写入以下内容。

```

// .npmignore
source

// .gitignore
node_modules
distribution

```

## npm deprecate

如果想废弃某个版本的模块，可以使用&nbsp;&nbsp;{-&nbsp;&nbsp;npm deprecate&nbsp;&nbsp;-}&nbsp;&nbsp;命令。

```

$ npm deprecate my-thing@"< 0.2.3" "critical bug fixed in v0.2.3"

```

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