## 基于node工程
* 包(项目，工程)
    * 概念
        ```
        1、在Node.js语言中，包和模块并没有本质的不同，包是在模块的基础上更深一步的抽象。
        2、包将某个独立的功能封装起来，用于发布、更新、依赖管理和进行版本控制。
        3、Node.js根据 CommonJS 规范实现了包机制，开发了 npm 来解决包的发布和获取需求。
        ```
    * 包的说明文件(package.json)
        * 使用package.json能干什么
        ```
        1、 相当于你本地项目的一个文档说明。
        2、允许你指定你项目中所使用的node包的版本。
        3、构建你的项目更加容易，便于给其他人共享。
        ```
        * package.json属性详解
            * 本质：json对象
            ```
            {
              "name": "npm_command", //包名
              "version": "1.0.0", //版本
              "scripts": { //配置npm运行命令
                "start": "node bin/www"
              },
              "dependencies": {//运行依赖的包
                "jquery": "^3.2.1"
              },
              "devDependencies": {//开发依赖的包
                "babel": "^6.23.0"
              }
            }
            ```
        * 扩展:
            ```
            "jquery": "^3.2.1" -----向上的尖括号可以管理二级，三级版本
            "jquery": "~3.2.1" -----波浪线可以管理三级版本。
            ```
* npm(包管理工具)  node package manager
    * 详述：
        ```
        1、Node包管理器(npm)是一个由Node.js官方提供的第三方包管理工具,
        2、npm是一个完全由JavaScript 实现的命令行工具，通过Node.js执行，因此严格来讲它不属于Node.js的一部分。
        3、在最初的版本中，我们需要在安装完Node.js以后手动安装npm。
           但从Node.js 0.6开始，npm已包含在发行包中了，安装Node.js时会自动安装npm。
           现在的版本大都使用6.0以上。。。
    ```
## npm命令详解
* npm命令详解
    * 使用npm命令来下载依赖模块及对项目包(模块)进行管理
    * 常用命令：
        * npm init: 生成package.json
        * npm install:用来安装package.json里的相关依赖包
        * npm install packageName -g(全局安装)
        * npm install packageName --save 安装包(局部安装---运行依赖)
        * npm install packageName@version --save 安装指定版本的包(局部安装)
        * npm install packageName --save-dev(局部安装--开发依赖)
        * npm info packageName (显示包的信息)
        * npm rm packageName (移除包)
        * npm config get prefix (获取全局安装包的所在地址,并且可见对应的cmd命令)
    * 使用npm导致的问题(更多的是针对5.0以下版本)
        * 下载慢
        * 甚至下载不了

## 淘宝镜像
* cnpm(淘宝镜像)
    * 将npm上的包同步更新到淘宝镜像上，目前是每10分钟同步一次。
    * 配置：npm install -g cnpm --registry=https://registry.npm.taobao.org
    * 修改仓库地址为npm地址：npm config set registry https://registry.npmjs.org/
    * 常用命令：使用 cnpm 代替 npm 即可
    * 问题：
        * 会多下载一些文件/文件夹
        * 严重者会导致 webstorm 瘫痪，就像帕金森综合征
    * 解决上述问题的办法
        * 修改 npm 的下载指向地址
        * npm config set registry "https://registry.npm.taobao.org"

## yarn Facebook开发的包管理工具
* yarn(包管理工具)
    * yarn是Facebook开源的新的包管理器，可以用来代替npm
    * 配置 npm install yarn -g
    * 特点：有缓存，没有自己的仓库地址
    * 常用命令
        * yarn --version
        * yarn
        * yarn init  //生成package.json   ！！！注意生成的包名不能有中文，大写
        * yarn global package (全局安装)
        * yarn add package (局部安装)
        * yarn add package --dev
        * yarn remove package
        * yarn list //列出已经安装的包名
        * yarn info packageName
        * 地址：https://yarnpkg.com/zh-Hans/
        
* cyarn
    * 使用淘宝镜像，更快
    * 配置：npm install cyarn -g --registry "https://registry.npm.taobao.org"
    * 常用命令：将 yarn 使用cyarn代替即可
    
* 补充扩展：
    * 2017年5月30日发布node 8.0，其中自带的npm也由3.xxx版本升级到5.0
    * npm5变化：
      * 通过npm下载包的时候多了一个package.lock.json
      * package.lock.json可以记录整个node-modules中文件夹的树状结构，再次下载的时候不用先去读取包与包之间相关依赖
        * 大白话：就是记录包与包之间的关联(依赖关系)
        * 好处：再次npm install下载的时候不用去先读取依赖可以直接下载，速度较快。
        * 可以利用离线缓存，合理的利用了缓存，提高了下载效率
        * 在速度上还是和yarn有些差异。
      * --save是一个默认属性，npm install下载包的时候会在package.json里显示依赖
      * 注意：npm3和npm5并没有完美对接
	      * 如果之前的项目是用npm下载的包，当后期用npm下载其他包的时候之前的包的依赖是无法读取到package.lock.json里，导致之前的包无法使用，此时需要npm install重新下载。
        