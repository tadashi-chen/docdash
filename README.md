# Docdash
JSDoc 3的模版，保留原有的结构，根据自己的喜好更改布局以及颜色

## 环境配置
安装grunt命令行工具
```
$ npm install -g grunt-cli
```
新建一个jsdoc项目
```
$ mkdir jsdoc_proj
$ cd jsdoc_proj
```
创建package.json文件，需要npm安装几个module在项目里（该过程全部回车跳过即可）
```
$ npm init 
```
安装grunt（上面安装`grunt-cli`只是命令行工具，不具备grunt的环境）
```
$ npm install --save-dev grunt
```
安装grunt的jsdoc插件
```
$ npm install --save-dev grunt-jsdoc
```
下载模版
```
$ cd node_modules
$ git clone https://github.com/tadashi-chen/docdash.git
```

回到`jsdoc_proj`目录，创建`Gruntfile.js`文件，内容如下
```javascript
module.exports = function(grunt) {
    grunt.initConfig({
        jsdoc: {
            dist: {
                src: ["src/*.js"], //源代码文件，在jsdoc_proj目录下创建src文件夹
                options: {
                    destination: "doc", //文档生成所在目录
                    template : "node_modules/docdash", //指定模版为docdash
                    configure: "conf.json" //在配置项里开启markdown插件
                }
            }
        }
    });

    grunt.loadNpmTasks("grunt-jsdoc");

    grunt.registerTask("default", ["jsdoc"]);
}
```

`jsdoc_proj目录下`创建配置文件`conf.json`，内容如下
```json
{
    "tags": {
        "allowUnknownTags": true,
        "dictionaries": ["jsdoc","closure"]
    },
    "source": {
        "includePattern": ".+\\.js(doc)?$",
        "excludePattern": "(^|\\/|\\\\)_"
    },
    "plugins": ["plugins/markdown"],
    "templates": {
        "cleverLinks": false,
        "monospaceLinks": false
    }
}
```

##用法
将js源代码文件放入`jsdoc_proj/src`文件夹
```
$ grunt jsdoc
```
如果js源代码没有语法错误，则命令行最后一行输出`Done.`表示执行成功，这时使用浏览器打开`jsdoc_proj/doc/index.html`即可看到生成的文档。