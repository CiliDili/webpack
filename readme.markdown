<h2>第01节：认识WebPack的作用</h2>

安装WebPack
WebPack的安装，采用的是命令行npm形式的安装。

具体安装方法：

用win+R打开运行对话框，输入cmd进入命令行模式。然后找到你想开始项目的地方，输入下方代码：

mkdir webpack_demo
cd webpack_demo

mkdir webpack_demo
cd webpack_demo
第一句是建立一个文件夹，第二句是进入这个文件夹。这个文件夹就是我们的项目文件目录了，文件夹建立好后，可以通过下面命令安装WebPack。

需要注意的是,你在执行下一步时必须安装node，可以通过 node -v来查看node安装情况和版本，如果没有安装，要先安装node才可以继续进行。

//全局安装
npm install -g webpack

//全局安装
npm install -g webpack
如果你这时安装失败了（出现了报错信息），一般有三种可能：

检查你node的版本号，如果版本号过低，升级为最新版本。
网络问题，可以考虑使用cnpm来安装（这个是淘宝实时更新的镜像）,具体可以登录cnpm的官方网站学习http://npm.taobao.org/。
权限问题，在Liux、Mac安装是需要权限，如果你是Windows系统，主要要使用以管理员方式安装。
注意：全局安装是可以的，但是webpack官方是不推荐的。这会将您项目中的 webpack 锁定到指定版本，并且在使用不同的 webpack 版本的项目中，可能会导致构建失败。

对项目目录进行安装

全局安装完成后，我们还要进行一个项目目录的安装。在用npm安装前，我们先要进行一下初始化，初始化的主要目的是生成package.json文件（这是一个标准的npm说明文件，里面蕴含了丰富的信息，包括当前项目的依赖模块，自定义的脚本任务等等，如果你对此文件还不了解，可以看看node 的相关知识）。

在命令行输入：

npm init

输入完成后,全程回车.这时用dir命令已经可以看到生成的package.json文件了。

输入下面命令进行项目目录的安装：

npm install --save-dev webpack
这里的参数–save是要保存到package.json中，dev是在开发时使用这个包，而生产环境中不使用。

开发环境and生产环境：

开发环境：在开发时需要的环境，这里指在开发时需要依赖的包。
生产环境：程序开发完成，开始运行后的环境，这里指要使项目运行，所需要的依赖包。
查看webpack版本
你安装好后，会想知道你现在webpack版本，在工作中交流时，也会经常问到你，你的打包版本是什么？这时候我们可以用下面的命令进行查看。

webpack -v

可以看到我现在的版本的3.6.0版本，这是目前（2017/10/28）最新的版本了。出现了版本号，也说明你的webpack安装成功了。

<h2>第02节：让你快速上手一个Demo</h2>

上节课已经安装好了Webpack到电脑上，这节课就开始一个简单的Demo，让你快速上手和熟悉Webpack的基`本用法。

建立基本项目结构
首先进入上节课我们建立的目录,进入后在根目录建立两个文件夹，分别是src文件夹和dist文件夹：

src文件夹：用来存放我们编写的javascript代码，可以简单的理解为用JavaScript编写的模块。
dist文件夹：用来存放供浏览器读取的文件，这个是webpack打包成的文件。
你可以理解成src是源码文件，dist是我们编译打包好的文件；一个用于开发环境，一个用于生产环境。

编写程序文件：
文件夹建立好后，我们在dist文件下手动建立一个index.html文件，并写入下面的代码。

/dist/index.html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Mr>yang_webpack</title>
</head>
<body>
    <div id="title"></div>
    <script src="./bundle.js"></script>
</body>
</html>

这里引入了一个JavaScript的bundle.js文件。这个文件现在还没有，这是用webpack执行打包命令后生产的文件。我们的index.html写好后，接下来在src文件夹下建立entery.js的文件，用于编写我们的JavaScript代码，也是我们的入口文件。

src/entery.js

document.getElementById('title').innerHTML='Hello Webpack--webpack打包';

第一次Webpack打包
Webpack其实是可以在终端（命令行）中使用的，基本使用方法如下：

webpack {entry file} {destination for bundled file}
{entry file}:入口文件的路径，本文中就是src/entery.js的路径；
{destination for bundled file}:填写打包后存放的路径。
注意：在命令行中是不需要写{ }的。
在我写的例子中，终端执行命令如下：

webpack src/entry.js dist/bundle.js

命令执行成功后，会在dist目录下出现bundle.js文件，这时我们就可以在浏览器中预览结果了，网页中显示出了"Hello Webpack--webpack打包"的信息。

总结：

从这个Demo中你会了解到webpack的基本用法和使用过程，并会了命令行打包的方法。

<h2>第03节：配置文件：入口和出口</h2>

上节课通过一个小Demo我们对Webpack有了初步了解，但是上节课的终端打包方案，在实际开发中并不使用，而是使用Webpack的配置文件的方式进行设置。这节课我们就学一下配置文件的大体结构和入口出口文件的配置。

配置文件webpack.config.js
webpack.config.js就是Webpack的配置文件，这个文件需要自己在项目根目录下手动建立。建立好后我们对其进行配置，先看下面的代码（webpack.config.js的基本结构），这是一个没有内容的标准webpack配置模版。
我们要在webpack.config.js的头部引入path，代码如下：

const path = require('path');
module.exports={
    //入口文件的配置项
    entry:{
        entry:'./src/entry.js'
    },
    //出口文件的配置项
    output:{
        //输出的路径，用了Node语法
        path:path.resolve(__dirname,'dist'),
        //输出的文件名称
        filename:'bundle.js' ---> filename:'[name].js'
    },
    //模块：例如解读CSS,图片如何转换，压缩
    module:{},
    //插件，用于生产模版和各项功能
    plugins:[],
    //配置webpack开发服务功能
    devServer:{}
}
entry：配置入口文件的地址，可以是单一入口，也可以是多入口。
output：配置出口文件的地址，在webpack2.X版本后，支持多出口配置。
module：配置模块，主要是解析CSS和图片转换压缩等功能。
plugins：配置插件，根据你的需要配置不同功能的插件。
devServer：配置开发服务功能，后期我们会详细讲解。

这个选项就是配置我们要压缩的文件一般是JavaScript文件（当然也可以是CSS…..）。按照上节课的代码(如果你上节课的代码还没作，那你可以返回去重新作一下)，这里要填写的是src目录下的entery.js文件。

这个代码写完后，可以在终端中直接输入webpack就会进行打包。

在实际开发中我们都是通过配置文件进行打包的，所以必须要掌握好。

多入口、多出口配置

Webpack在版本1的时候很难设置多出口文件，但是在2版本开始就变的很方便了。直接看多入口和多出口的文件配置，然后可以和单一出口对比一下，你会发现这种设置非常简单（只需改动两点配置就可以）。

[name]的意思是根据入口文件的名称，打包成相同的名称，有几个入口文件，就可以打包出几个文件。

总结：

这节课的内容是需要仔细消化的，不求你记住，但是要练习，因为你无论配置任何项目的Webpack都要作这些操作。你可以把本文当作一个字典，在需要的时候进行查询。

<h2>第04节：配置文件： 服务和热更新</h2>

作为一个前端工程师，最大的编程需求之一就是所见即所得的工具，也就是常说的热更新。这节课就学习用webpack3.6版本实现热更新效果。

设置webpack-dev-server
要执行webpack-dev-server是要先用npm install webpack-dev-server –save-dev 来进行下载的。下载好后，需要配置一下devServer。最简单的devServer配置项只有四个。先看一下代码，然后我再作解释。

devServer:{
    //设置基本目录结构
    contentBase:path.resolve(__dirname,'dist'),
    //服务器的IP地址，可以使用IP也可以使用localhost
    host:'localhost',
    //服务端压缩是否开启
    compress:true,
    //配置服务端口号
    port:8888
}

contentBase:配置服务器基本运行路径，用于找到程序打包地址。
host：服务运行地址，建议使用本机IP，这里为了讲解方便，所以用localhost。
compress：服务器端压缩选型，一般设置为开启，如果你对服务器压缩感兴趣，可以自行学习。
port：服务运行端口，建议不使用80，很容易被占用，这里使用了1717.
注意：这里需要使用npm 来进行安装webpack-dev-server了， 命令如下：

npm install webpack-dev-server --save-dev

我们只要在package.json里配置一下scripts选项就可以执行了。

"scripts": {
    "server":"webpack-dev-server"
 },
配置好保存后，在终端里输入 npm  run  server  打开服务器。然后在浏览器地址栏输入http://localhost:8888 -->就可以看到结果了。

支持热更新

在npm run server  启动后，它是有一种监控机制的（也叫watch）。它可以监控到我们修改源码，并立即在浏览器里给我们更新。

注意：这里只是我们的webpack3.6版本支持，在3.5版本时要支持热更新还需要一些其他的操作。因为已经有了成熟的3.6版本，我就不再介绍低版本的操作方法。还有一种情况。如果你都设置好了，但是不进行热更新，可能是你系统的问题，在Linux和Ma上支持良好，在Windows上有时会出现问题。
