第01节：认识WebPack的作用
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

上节课已经安装好了Webpack到电脑上，这节课就开始一个简单的Demo，让你快速上手和熟悉Webpack的基本用法。

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