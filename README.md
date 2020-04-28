# 常用软件

[Adobe 2020 全家桶： 可修改安装位置、安装后登录账号即可使用 地址：百度网盘  提取码：8php](https://pan.baidu.com/s/17BDZnKYxG_NKsnyneSs1lg)
  
    
# 代码规范

[前端开发代码规范](https://code.jingshonline.net/zhengyan/front-end-documents-and-tools/blob/master/CodeFormatting.md)

## Vue 相关文档

[Vue 官方文档：https://vuejs.org/index.html](https://vuejs.org/index.html)
        
[Vue-cli 文档：https://cli.vuejs.org/](https://cli.vuejs.org/)
        
[NUXT官方文档：https://nuxtjs.org/](https://nuxtjs.org/)
        
[VueX官方文档：https://vuex.vuejs.org/](https://vuex.vuejs.org/)

[Vue 相关视频: 百度网盘 提取码：mlw7](https://pan.baidu.com/s/1oUgoWKO_H-i6qd0moxMfvQ)

## PDF 在线预览

[vue-pdf github 仓库地址](https://github.com/FranckFreiburger/vue-pdf)

[vue 使用 vue-pdf 实现在线预览](https://code.jingshonline.net/zhengyan/front-end-documents-and-tools/blob/master/vue-pdf.md)
    
## Node 相关文档

[Node 官方文档：https://nodejs.org/en/](https://nodejs.org/en/)

[Npm 官方文档:https://www.npmjs.com/](https://www.npmjs.com/)

[Node 多版本环境安装 + 多镜像直接切换](https://www.jianshu.com/p/344add85d050)

## UI框架

[Element-UI 官方文档:https://element.eleme.cn/](https://element.eleme.cn/)

[iView 官方文档:https://www.iviewui.com/](https://www.iviewui.com/)

[Ant 官方文档:https://ant.design/index-cn](https://ant.design/index-cn)

[D2 Admin 官方文档:https://fairyever.com/d2-admin/doc/](https://fairyever.com/d2-admin/doc/)

## 小程序

[腾讯开发文档:https://open.tencent.com/](https://open.tencent.com/)

[微信平台文档:https://developers.weixin.qq.com/doc/](https://developers.weixin.qq.com/doc/)

[微信小程序官方文档:https://developers.weixin.qq.com/miniprogram/dev/api/](https://developers.weixin.qq.com/miniprogram/dev/api/)

[QQ小程序官方文档:https://q.qq.com/wiki/develop/miniprogram/frame/](https://q.qq.com/wiki/develop/miniprogram/frame/)

[mpvue 官方文档:http://mpvue.com/](http://mpvue.com/)

[支付宝平台文档:https://docs.open.alipay.com/catalog](https://docs.open.alipay.com/catalog)

[支付宝小程序官方文档:https://docs.alipay.com/mini/developer/](https://docs.alipay.com/mini/developer/)

[百度开发者中心:https://developer.baidu.com/](https://developer.baidu.com/)

[百度小程序官方文档:https://smartprogram.baidu.com/docs/introduction/enter_application/](https://smartprogram.baidu.com/docs/introduction/enter_application/)

[字节跳动开发平台:https://developer.toutiao.com/](https://developer.toutiao.com/)

[字节跳动小程序文档:https://developer.toutiao.com/docs/api/](https://developer.toutiao.com/docs/api/)

## 跨平台开发

[UNI-APP 官方文档:https://uniapp.dcloud.io/](https://uniapp.dcloud.io/)

## 时间日期格式化

[Moment.js 官方文档:https://momentjs.com/](https://momentjs.com/)

## JS 相关文档

[JS 总结](https://juejin.im/post/5e9f0bdce51d4546f5791989)

# VSCode 


### 编辑器代码格式化


```
    {
      // 使能每一种语言默认格式化规则
      "[html]": {
          "editor.defaultFormatter": "esbenp.prettier-vscode"
      },
      "[css]": {
          "editor.defaultFormatter": "esbenp.prettier-vscode"
      },
      "[less]": {
          "editor.defaultFormatter": "esbenp.prettier-vscode"
      },
      "[javascript]": {
          "editor.defaultFormatter": "esbenp.prettier-vscode"
      },
      "[vue]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
      },
      
      /*  prettier的配置 */
      "prettier.printWidth": 100, // 超过最大值换行
      "prettier.tabWidth": 2, // 缩进字节数
      "prettier.useTabs": false, // 缩进不使用tab，使用空格
      "prettier.semi": true, // 句尾添加分号
      "prettier.singleQuote": true, // 使用单引号代替双引号
      "prettier.proseWrap": "preserve", // 默认值。因为使用了一些折行敏感型的渲染器（如GitHub comment）而按照markdown文本样式进行折行
      "prettier.arrowParens": "avoid", //  (x) => {} 箭头函数参数只有一个时是否要有小括号。avoid：省略括号
      "prettier.bracketSpacing": true, // 在对象，数组括号与文字之间加空格 "{ foo: bar }"
      "prettier.disableLanguages": ["vue"], // 不格式化vue文件，vue文件的格式化单独设置
      "prettier.endOfLine": "auto", // 结尾是 \n \r \n\r auto
      "prettier.htmlWhitespaceSensitivity": "ignore",
      "prettier.ignorePath": ".prettierignore", // 不使用prettier格式化的文件填写在项目的.prettierignore文件中
      "prettier.jsxBracketSameLine": false, // 在jsx中把'>' 是否单独放一行
      "prettier.jsxSingleQuote": false, // 在jsx中使用单引号代替双引号
      "prettier.requireConfig": false, // Require a 'prettierconfig' to format prettier
      "prettier.trailingComma": "es5", // 在对象或数组最后一个元素后面是否加逗号（在ES5中加尾逗号）
      // "prettier.tslintIntegration": false, // 不让prettier使用tslint的代码格式进行校验
      // "prettier.eslintIntegration": false, //不让prettier使用eslint的代码格式进行校验
      // "prettier.stylelintIntegration": false, //不让prettier使用stylelint的代码格式进行校验
      // "prettier.parser": "babylon", // 格式化的解析器，默认是babylon
    
      /* Vetur配置 */
      "vetur.format.defaultFormatter.html": "prettier",
      "vetur.format.defaultFormatter.js": "prettier",
      "vetur.format.defaultFormatter.less": "prettier",
      "vetur.format.defaultFormatterOptions": {
        "prettier": {
          "printWidth": 160,
          "singleQuote": true, // 使用单引号
          "semi": true, // 末尾使用分号
          "tabWidth": 4,
          "arrowParens": "avoid",
          "bracketSpacing": true,
          "proseWrap": "preserve" // 代码超出是否要换行 preserve保留
        }
      },
    
      /* 编辑器配置 */
      "editor.tabSize": 2, // tab缩进空格数
      "javascript.format.insertSpaceBeforeFunctionParenthesis": false,
      "editor.codeActionsOnSave": {
        "source.fixAll.eslint": true
      },
      "javascript.updateImportsOnFileMove.enabled": "always",
      "workbench.editor.enablePreview": false,
      "diffEditor.ignoreTrimWhitespace": false, // 打开文件时在新标签打开
      "explorer.compactFolders": false, // 空文件夹自动折叠
      "problems.showCurrentInStatus": true, // 在状态栏显示错误信息
    }
    
    
    
    ```
    代码格式化配置参考文档
    https://juejin.im/post/5cc58039f265da03775c5a6f
    ```
```

### 编辑器代码格式化 搭配扩展

![image](https://raw.githubusercontent.com/qingyuun/front-end-documents-and-tools/master/formatEX.jpg?token=AEZMGN7EJMVDCPU7W434WMK57LT62)

# GIT 操作

``` bash

# 刷新远程分支
$ git remote update origin --prune

# 创建分支
$ git branch <branch-name>

# 切换分支
$ git checkout <branch-name>

# 新建并切换分支
$ git checkout -b <branch-name>

# 删除分支
$ git branch -d <branch-name>

# 删除远程分支
$ git branch -r -d origin/branch-name

# 查看分支
$ git branch

# 查看远程分支
$  git branch -a

# 获取远程更新代码
$ git fetch

# 合并远程代码至本地分支
$ git merge

# 推送至远程分支
$ git push origin <branch-name>

# 查看本次的修改、新建、删除等信息(new file:新建文件，modified:修改文件，deleted: 删除的文件)
$ git status 

# 拉取代码
$ git pull

# 添加所有即将提交的文件
$ git add . 

# 添加某个文件
$ git add fileNamePath

#  提交到本地
$ git commit -'提交的日志'

# 提交到git服务器
$ git push

# 添加所有即将提交的文件并提交到本地 
$ git commit -a -m '提交的日志' 

# 相当于git add . 和 git commi -' '命令的集合，当你使用git commit -a -m ' '命令时，就会执行上述两个操作
$ git commit -a -m 

# 暂存（存储在本地，并将项目本次操作还原）
$ git stash

# 使用上一次暂存，并将这个暂存删除，使用该命令后，如果有冲突，终端会显示，如果有冲突需要先解决冲突（这就避免了冲突提交服务器，将冲突留在本地，然后解决）
$ git stash pop 

# 查看所有的暂存
$ git stash list 

# 清空所有的暂存
$ git stash clear

#  删除某一个暂存，在中括号里面放置需要删除的暂存ID
$ git stash drop [-q|--quiet] [<stash>]

# 使用某个暂存，但是不会删除这个暂存
$ git stash apply 

# 找回清空代码
$ git fsck --lost-found 命令找出刚才删除的分支里面的提交对象。
$ git show 命令查看是否正确，如果正确使用
$ git merge 命令找回

```



# 代码片段

## vscode 代码快捷生成 代码片段

#### NUXT VUEX

```
"print to console":{
	"prefix": "Nuxt Vuex",
	"body": [
		"import * as '' from ''",
		"export const state = () => ({",
		"  courtLevel: [",
				
		"  ]",
		"})",
		"export const mutations = {",
		"  SET_COURT_LEVEL: (state, data) => {",
		"    state.courtLevel = data",
		"  }",
		"}",
		"export const actions = {",
		"  getCourt({ commit }, data) {",
		"",
		"  }",
		"}"
	],
	"description": "nuxt vuex store"
}
```

#### VUE
```
"Print to console": {
    "prefix": "vue",
    "body": [
        "<template>",
        "  <div>",
        "",
        "  </div>",
        "</template>",
        "",
        "<script>",
        "import a from ''",
        "export default {",
        "  name: '',",
        "",
        "  components: {",
        "    a",
        "  },",
        "",
        "  data () {",
        "    return {",
        "",
        "    }",
        "  },",
        "",
        "  watch: {",
        "  },",
        "",
        "  mounted () {",
        "  },",
        "",
        "  methods: {",
        "",
        "  }",
        "}",
        "</script>",
        "",
        "<style lang='scss' scoped>",
        "",
        "</style>",
        ""
    ],
    "description": "Log output to console"
}
```

#### VUE Nuxt
```
"Print to console": {
	"prefix": "vue nuxt",
	"body": [
		"<template>",
		"  <div>",
		"    1",
		"  </div>",
		"</template>",
		"<script>",
		"export default {",
		"  layout: 'userCenter',",
		"  name: 'UserCenterCaseStatistical',",
		"  middleware: 'auth',",
		"  head() {",
		"    return {",
		"      title: '用户中心-案件统计',",
		"      meta: [",
		"        { hid: 'description', name: 'description', content: '京师在线用户中心；jingshonline-usercenter' }",
		"      ]",
		"    }",
		"  },",
		"  components: {",
		"  },",
		"  data() {",
		"    return {",
		"    }",
		"  },",
		"  watch: {",
		"  },",
		"  mounted() {",
		"  },",
		"  methods: {",
		"  }",
		"}",
		"</script>",
		"<style lang='scss' scoped>",
		"</style>",
		""
	],
	"description": "vue nuxt"
}
```

# Other

![image](https://code.jingshonline.net/zhengyan/front-end-documents-and-tools/raw/master/123.jpg)
