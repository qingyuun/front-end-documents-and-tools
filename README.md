# VSCode 

## 编辑器代码格式化

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
    
      "editor.tabSize": 2,
      "javascript.format.insertSpaceBeforeFunctionParenthesis": false,
      "editor.codeActionsOnSave": {
        "source.fixAll.eslint": true
      }
    }
    
    
    
    ```
    代码格式化配置参考文档
    https://juejin.im/post/5cc58039f265da03775c5a6f
    ```
```

## 编辑器代码格式化 搭配扩展

![image](https://code.jingshonline.net/zhengyan/front-end-documents-and-tools/raw/master/formatEX.jpg)

##