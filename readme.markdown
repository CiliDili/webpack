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

<h2>第05节：模块：CSS文件打包</h2>

Webpack在生产环境中有一个重要的作用就是减少http的请求数，就是把多个文件打包到一个js里，这样请求数就可以减少好多.把我们的CSS文件打包。在学习CSS打包之前，需要先对webpack.config.js里的Loaders配置项进行了解。

Loaders
Loaders是Webpack最重要的功能之一，他也是Webpack如此盛行的原因。通过使用不同的Loader，Webpack可以的脚本和工具，从而对不同的文件格式进行特定处理。

简单的举几个Loaders使用例子：

可以把SASS文件的写法转换成CSS，而不在使用其他转换工具。
可以把ES6或者ES7的代码，转换成大多浏览器兼容的JS代码。
可以把React中的JSX转换成JavaScript代码。
注意：所有的Loaders都需要在npm中单独进行安装，并在webpack.config.js里进行配置。下面我们对Loaders的配置型简单梳理一下。

test：用于匹配处理文件的扩展名的表达式，这个选项是必须进行配置的；
use：loader名称，就是你要使用模块的名称，这个选项也必须进行配置，否则报错；
include/exclude:手动添加必须处理的文件（文件夹）或屏蔽不需要处理的文件（文件夹）（可选）；
query：为loaders提供额外的设置选项（可选）。
明白了Loader是什么后，就开始这节课的正题，如何打包CSS文件。

打包CSS文件：
建立index.css文件

要打包CSS你必须先要有个CSS文件，在/src目录下，我们建立一个css文件夹，在文件夹里建立index.css文件。代码内容如下。

#title {
    font-size: 20px;
    color: #bf616a;
}

CSS文件建立好后，需要引入到入口文件中，才可以打包到，这里我们引入到entry.js中。

import css from './css/index.css';

CSS和引入做好后，我们就需要使用loader来解析CSS文件了，这里我们需要两个解析用的loader，分别是style-loader和css-loader。

style-loader:

它是用来处理css文件中的url()等，npm中的网址：https://www.npmjs.com/package/style-loader

用npm install 进行项目安装：

npm install style-loader --save-dev

css-loader：

它是用来将css插入到页面的style标签。npm中的网址：https://www.npmjs.com/package/css-loader

用npm install 进行项目安装：

npm install --save-dev css-loader

两个loader都下载安装好后，我们就可以配置我们loaders了。

loaders配置：

修改webpack.config.js中module属性中的配置代码如下：

   module:{
        rules: [
            {
              test: /\.css$/,
              use: [ 'style-loader', 'css-loader' ]
            }
          ]
    },
这个文件的详细讲解，我们在上面已经提及，如果你还是无法理解可以观看视频。

总结：loader的使用也决定着你webpack水平的高低。

<h2>第06节：插件配置：配置JS压缩</h2>

通过五节课的学习，我相信小伙伴已经对Webpack有所入门。这节课让我们初步了解插件（plugins[ ]）的用法。

压缩JS代码：

现在你写的JS代码，在上线之前，都是需要进行压缩的，在没有webpack和gulp这些工具前，你可能需要找一个压缩软件或者在线进行压缩，在Webpack中可以很轻松的实现JS代码的压缩，它是通过插件的方式实现的，这里我们就先来引入一个uglifyjs-webpack-plugin(JS压缩插件，简称uglify)。

注意：虽然uglifyjs是插件，但是webpack版本里默认已经集成，不需要再次安装。

我们需要在webpack.config.js中引入uglifyjs-webpack-glugin插件

const uglify = require('uglifyjs-webpack-plugin');

引入后在plugins配置里new一个 uglify对象就可以了，代码如下。

plugins:[
    new uglify()
],

这时候在终端中使用webpack进行打包，你会发现JS代码已经被压缩了。


<h2>第07节：插件配置：HTML文件的发布</h2>

---> src文件打包生成dist目录文件

打包HTML文件
我们先把dist中的html文件剪切到src目录中，并去掉我们的JS引入代码（webpack会自动为我们引入JS），因为这才是我们真实工作的目录文件结构。

然后我们配置webpack.config.js文件，先引入我们的html-webpack-plugin插件。

const htmlPlugin= require('html-webpack-plugin');
引入后使用npm进行安装包。

npm install --save-dev html-webpack-plugin

最后在webpack.config.js里的plugins里进行插件配置，配置代码如下。


new htmlPlugin({
    minify:{
        removeAttributeQuotes:true
    },
    hash:true,
    template:'./src/index.html'

})

minify：是对html文件进行压缩，removeAttrubuteQuotes是却掉属性的双引号。
hash：为了开发中js有缓存效果，所以加入hash，这样可以有效避免缓存JS。 //这是是html 里面的把js文件的引用加上字符串 -->跟js 文件没有半毛钱关系
template：是要打包的html模版路径和文件名称。
上边的都配置完成后，我们就可以在终端中使用webpack，进行打包。你会看到index.html文件已经被打包到我们的dist目录下了，并且自动为我们引入了路口的JS文件。

总结：

html文件的打包可以有效的区分开发目录和生产目录，在webpack的配置中也要搞清楚哪些配置用于生产环境，哪些配置用于开发环境，避免两种环境的配置冲突。


<h2>第08节：图片迈坑：CSS中的图片处理</h2>

在学习Webapck过程中你可能遇到的第一个坑就是CSS中的图片处理。很多webpack新手都在图片的坑中无法自拔（有的小伙伴在开发环境中是可以找到图片的，但是一打包后就找不到图片了，有的小伙伴是不知道如何正确引入html或者css中的图片，导致程序出错

找到图片后在src目录下新建一个images文件夹，把图片放入images文件夹。

在index.html文件中增加一个放置div的标签（需要注意的是这里修改的是src下的index.html文件，不是dist下的，这点新手很容易弄混，要格外注意），代码如下。

<div id="tupian"></div>

编写css文件，把你用的图片作为背景显示。

#tupian{
   background-image: url(../images/manhua.png);
   width:466px;
   height:453px;
}


图片打包需要 --> file-loader、url-loader

安装file-loader和url-loader

npm install --save-dev file-loader url-loader

安装好后我们需要对两个loader进行基本的了解。

<p>file-loader：解决引用路径的问题，拿background样式用url引入背景图来说，我们都知道，webpack最终会将各个模块打包成一个文件，因此我们样式中的url路径是相对入口html页面的，而不是相对于原始css文件所在的路径的。这就会导致图片引入失败。这个问题是用file-loader解决的，file-loader可以解析项目中的url引入（不仅限于css），根据我们的配置，将图片拷贝到相应的路径，再根据我们的配置，修改打包后文件引用路径，使之指向正确的文件。
</p>

<p>url-loader：如果图片较多，会发很多http请求，会降低页面性能。这个问题可以通过url-loader解决。url-loader会将引入的图片编码，生成dataURl。相当于把图片数据翻译成一串字符。再把这串字符打包到文件中，最终只需要引入这个文件就能访问图片了。当然，如果图片较大，编码会消耗性能。因此url-loader提供了一个limit参数，小于limit字节的文件会被转为DataURl，大于limit的还会使用file-loader进行copy。
</p>

配置url-loader

我们安装好后，就可以使用这个loader了，记得在loader使用时不需要用require引入，在plugins才需要使用require引入。

webpack.config.js文件

//模块：例如解读CSS,图片如何转换，压缩
module:{
    rules: [
        {
          test: /\.css$/,
          use: [ 'style-loader', 'css-loader' ]
        },{
           test:/\.(png|jpg|gif)/ ,
           use:[{
               loader:'url-loader',
               options:{
                   limit:500000
               }
           }]
        }
      ]
},
test:/\.(png|jpg|gif)/是匹配图片文件后缀名称。
use：是指定使用的loader和loader的配置参数。
limit：是把小于500000B的文件打成Base64的格式，写入JS。
写好后就可以使用webpack进行打包了，这回你会发现打包很顺利的完成了。具体的Base64的格式，你可以查看视频中的样子。

为什么只使用了url-loader
大家发现我们并没有在webpack.config.js中使用file-loader，但是依然打包成功了。我们需要了解file-loader和url-loader的关系。url-loader和file-loader是什么关系呢？简答地说，url-loader封装了file-loader。url-loader不依赖于file-loader，即使用url-loader时，只需要安装url-loader即可，不需要安装file-loader，因为url-loader内置了file-loader。通过上面的介绍，我们可以看到，url-loader工作分两种情况：

1.文件大小小于limit参数，url-loader将会把文件转为DataURL（Base64格式）；

2.文件大小大于limit，url-loader会调用file-loader进行处理，参数也会直接传给file-loader。

也就是说，其实我们只安装一个url-loader就可以了。但是为了以后的操作方便，我们这里就顺便安装上file-loader。


<h2>第09节：图片迈坑：CSS分离与图片路径处理</h2>

通过上节课的学习已经能把小图片打包成Base64格式，也对webpack对图片的打包有个基本了解。主要学习两个知识：第一个是把CSS从JavasScript代码中分离出来，第二个是如何处理分离出来后CSS中的图片路径不对问题。

CSS分离:extract-text-webpack-plugin

有些简单的交互页面中，你的JavasScript页面代码会非常少，而大部分代码都在CSS中，这时候项目组长会要求把CSS单独提取出来，方便以后更改。遇到这个需求你不要惊慌，已经有大神为我们准备好了对象的插件（plugin）。

extract-text-webpack-plugin

这个插件就可以完美的解决我们提取CSS的需求，但是webpack官方其实并不建议这样作，他们认为CSS就应该打包到JavasScript当中以减少http的请求数。但现实中的需求往往不是我们前端能控制的，有些需求是我们不能控制的，分离CSS就是这样一个既合理由不合理的需求。

npm install --save-dev extract-text-webpack-plugin

引入：安装完成后，需要先用require引入。

const extractTextPlugin = require("extract-text-webpack-plugin");

设置Plugins：引入成功后需要在plugins属性中进行配置。这里只要new一下这个对象就可以了。

 new extractTextPlugin("/css/index.css")

这里的/css/index.css是分离后的路径位置。这部配置完成后，包装代码：还要修改原来我们的style-loader和css-loader。

修改代码如下。

module:{
        rules: [
            {
              test: /\.css$/,
              use: extractTextPlugin.extract({
                fallback: "style-loader",
                use: "css-loader"
              })
            },
            {
               test:/\.(png|jpg|gif)/ ,
               use:[{
                   loader:'url-loader',
                   options:{
                       limit:500000
                   }
               }]
            }
        ]
},

现在就可以使用webpack进行打包了。

图片路径问题：

利用extract-text-webpack-plugin插件很轻松的就把CSS文件分离了出来，但是CSS路径并不正确，很多小伙伴就在这里搞个几天还是没有头绪，网上也给出了很多的解决方案，我觉的最好的解决方案是使用publicPath解决，我也一直在用。

publicPath：是在webpack.config.js文件的output选项中，主要作用就是处理静态文件路径的。

在处理前，我们在webpack.config.js 上方声明一个对象，叫website。

var website ={

    publicPath:"http://'+ 本机的ip(ipconfig) +'/'+ 在devServer 里面定义的端口号(port) +'"
}

注意，这里的IP和端口，是你本机的ip或者是你devServer配置的IP和端口。

然后在output选项中引用这个对象的publicPath属性。

 //出口文件的配置项
    output:{
        //输出的路径，用了Node语法
        path:path.resolve(__dirname,'dist'),
        //输出的文件名称
        filename:'[name].js',
        publicPath:website.publicPath
    },

配置完成后，你再使用webpack命令进行打包，你会发现原来的相对路径改为了绝对路径，这样来讲速度更快。

总结：我们实现了CSS的分离，并在分离后处理了图片路径不对的问题。处理路径的方法一定要充分理解，因为这在工作中经常用到。

<h2>第10节：图片迈坑：处理HTML中的图片</h2>

在webpack中是建议使用标签<img>来引入图片的，但是我们作前端的人特别热衷于这种写法，国人也为此开发了一个：
html-withimg-loader。他可以很好的处理我们在html 中引入图片的问题。因为是国人开发的，文档都是中文，所以学习起来还是比较简单的。

如何把图片放到指定的文件夹下.

前面的我们打包后的图片并没有放到images文件夹下，要放到images文件夹下，其实只需要配置我们的url-loader选项就可以了。


   module:{
        rules: [
            {
              test: /\.css$/,
              use: extractTextPlugin.extract({
                fallback: "style-loader",
                use: "css-loader"
              })
            },{
               test:/\.(png|jpg|gif)/ ,
               use:[{
                   loader:'url-loader',
                   options:{
                       limit:5000,
                       outputPath:'images/',
                   }
               }]
            }
          ]
    },

这回你再执行打包就可以把图片打包到images文件夹里了。

html-withimg-loader就是我们今天的重点了，这个插件并不是很火，也是我个人喜欢的一个小loader。解决的问题就是在hmtl文件中引入<img>标签的问题。

npm i -D html-withimg-loader

webpack.config.js

{
    test: /\.(htm|html)$/i,
    use:[ 'html-withimg-loader']
}

然后在终端中可以进行打包了。你会发现images被很好的打包了。并且路径也完全正确。 (ps: 也许你打包后也不能出现images文件夹,这是看下.css或.htlm的图片路径使用base64引入到页面的,这是我们需要更改limit的限制即可)

总结：我们通过8,9,10小节来踩webpack图片中的坑,在你工作中遇到图片的问题，也可以返回文章里进行对比查找问题。


<h2>第11节：CSS进阶：Less文件的打包和分离</h2>

Less文件如何打包和分离。Less 是一门 CSS 预处理语言，它扩展了 CSS 语言，增加了变量、Mixin、函数等特性，使 CSS 更易维护和扩展。

要使用Less，我们要首先安装Less的服务，当然也是用npm来进行安装。

npm install --save-dev less

还需要安装Less-loader用来打包使用。 npm install --save-dev less-loader

写loader配置：

安装好后，需要在webpack.config.js里编写loader配置，当然要想正确解析成CSS，还是需要style-loader和css-loader的帮助，但是这两个loader前边已经讲过了，所以在这里就不重复了，如果你还对这两个loader不熟悉，那自行回去补前边的第五节吧。

webpack.config.js

编写一个less文件

引入到我们entery.js文件中

import less from './css/black.less';

这样我们就可以把less文件进行打包了。我们可以使用webpack命令打包试一试。

我们之前讲了extract-text-webpack-plugin这个插件，想把Less文件分离出来的方法跟这个几乎一样，之前的我们在第09节中讲过，这里我们就只讲less的loader配置方法。（此处建议收看视频）

    {
        test: /\.(css|less)/,
        use: extractTextPlugin.extract({
            use: [{
                loader: "css-loader"
            }, {
                loader: "less-loader"
            }],
            // use style-loader in development
            fallback: "style-loader"
        })
    }

配置好后，你会发现less被分离到了index.css文件里。 ---> 用new extractTextPlugin('源文件路径'),进行分离

总结：Less是非常好的CSS扩展，但是Less得转换稍显麻烦，好的是webpack为我们提供了简单轻松的转换方法。


<h2>第12节：CSS进阶：SASS文件的打包和分离</h2>

安装SASS打包的loader

这里需要 在项目目录下用npm安装两个包。node-sass和sass-loader

node-sass：因为sass-loader依赖于node-sass，所以需要先安装

node-sass  --> npm install --save-dev node-sass

sass-loader:  --> npm install --save-dev sass-loader

编写loader配置

需要注意的是loader的加载要有先后顺序。

把SASS文件分离。

    {
        test: /\.(css|less|sass)$/,
        use: extractTextPlugin.extract({
            use: [{
                loader: "css-loader"
            }, {
                loader: "sass-loader"
            }],
            // use style-loader in development
            fallback: "style-loader"
        })
     }
其实整体过程和less的使用差不多，希望你能在工作中开始使用sass，并写出漂亮的css代码。


<h2>第13节：CSS进阶：自动处理CSS3属性前缀</h2>

(我发现这是是有问题的  --> 目前只加了 -webkit- 只做了Chrome和Safari的兼容有什么用!!!!)

/*transform:rotate(7deg);*/
/*-ms-transform:rotate(7deg); 	!* IE 9 *!*/
/*-moz-transform:rotate(7deg); 	!* Firefox *!*/
/*-webkit-transform:rotate(7deg); !* Safari 和 Chrome *!*/
/*-o-transform:rotate(7deg); 	!* Opera *!*/

CSS3已经成了前端的必会技能，但是你一定为那些属性需要加前缀，那些属性不需要加前缀而头疼。如何通过postcss-loader给css3属性自动添加前缀。

为了浏览器的兼容性，有时候我们必须加入-webkit,-ms,-o,-moz这些前缀。目的就是让我们写的页面在每个浏览器中都可以顺利运行。

PostCSS

PostCSS是一个CSS的处理平台，它可以帮助你的CSS实现更多的功能，但是今天我们就通过其中的一个加前缀的功能，初步了解一下PostCSS。

需要安装两个包postcss-loader 和autoprefixer（自动添加前缀的插件）: npm install --save-dev postcss-loader autoprefixer

postCSS推荐在项目根目录（和webpack.config.js同级），建立一个postcss.config.js文件。

postcss.config.js

module.exports = {
    plugins: [
        require('autoprefixer')
    ]
}
这就是对postCSS一个简单的配置，引入了autoprefixer插件。让postCSS拥有添加前缀的能力，它会根据 can i use 来增加相应的css3属性前缀。

对postcss.config.js配置完成后，我们还需要编写我们的loader配置。

    {
        test: /\.css$/,
        use: extractTextPlugin.extract({
            fallback: "style-loader",
            use: [
                {
                    loader: 'css-loader',
                    options: { importLoaders: 1 }
                },
                {
                    loader: "postcss-loader"
                }
            ]
        })

    }

总结:postcss还有很多功能，这里给出postcss-loader的github地址：https://github.com/postcss/postcss-loader


<h2>第14节：CSS进阶：消除未使用的CSS</h2>

我们可能无暇关注CSS样式，造成很多CSS的冗余。这节用webpack消除未使用的CSS。


PurifyCSS
使用PurifyCSS可以大大减少CSS冗余，比如我们经常使用的BootStrap(140KB)就可以减少到只有35KB大小。这在实际开发当中是非常有用的。

安装PurifyCSS-webpack
从名字你就可以看出这是一个插件，而不是loader。所以这个需要安装还需要引入。 PurifyCSS-webpack要依赖于purify-css这个包，所以这两个都需要安装。

npm i -D purifycss-webpack purify-css

引入glob

因为我们需要同步检查html模板，所以我们需要引入node的glob对象使用。在webpack.config.js文件头部引入glob。

同样在webpack.config.js文件头部引入purifycss-webpack

const PurifyCSSPlugin = require("purifycss-webpack");

引入完成后我们需要在webpack.config.js里配置plugins。

plugins:[
    //new uglify()
    new htmlPlugin({
        minify:{
            removeAttrubuteQuotes:true
        },
        hash:true,
        template:'./src/index.html'

    }),
    new extractTextPlugin("css/index.css"),

    new PurifyCSSPlugin({
         // Give paths to parse for rules. These should be absolute!
        paths: glob.sync(path.join(__dirname, 'src/*.html')),
    })

]
这里配置了一个paths，主要是需找html模板，purifycss根据这个配置会遍历你的文件，查找哪些css被使用了。

用webpack打包，你会发现没用的CSS已经自动给你删除掉了。在工作中记得一定要配置这个plugins，因为这决定你代码的质量，非常有用。


<h2>第15节：给webpack增加babel支持</h2>

在前端开发中都开始使用ES6的语法了，虽然说webpack3增加了一些ES6的转换支持，但是实际效果不是很好。

Babel是什么？--> Babel其实是一个编译JavaScript的平台，它的强大之处表现在可以通过便宜帮你达到以下目的：

使用下一代的javaScript代码(ES6,ES7….)，即使这些标准目前并未被当前的浏览器完全支持。

Babel的安装与配置:

Babel其实是几个模块化的包，其核心功能位于称为babel-core的npm包中，webpack可以把其不同的包整合在一起使用，对于每一个你需要的功能或拓展，你都需要安装单独的包（用得最多的是解析ES6的babel-preset-es2015包和解析JSX的babel-preset-react包）。

我们先一次性安装这些依赖包


cnpm install --save-dev babel-core babel-loader babel-preset-es2015 babel-preset-react

    {
        test:/\.(jsx|js)$/,
        use:{
            loader:'babel-loader',
            options:{
                presets:[
                    "es2015","react"
                ]
            }
        },
        exclude:/node_modules/
    }

现在你已经可以用webapck转换ES6的语法兼容各个浏览器了。

上面的代码使用了ES6的let声明方法。如果你不使用Babel来进行转换，你会发现打包出来的js代码没有作兼容处理，使用了Babel转换的代码是进行处理过的。

.babelrc配置  --> 提取 babel

虽然Babel可以直接在webpack.config.js中进行配置，

ENV：

现在官方推荐使用的是babel-preset-env,那我们为了紧跟潮流，描述下env的配置方法。

npm install --save-devv babel-preset-env

然后修改.babelrc里的配置文件。其实只要把之前的es2015换成env就可以了。

{
    "presets":["react","env"]
}

总结：在实际工作中还是要安装Babel的，这样能更好的兼容每种浏览器，而把Babel的配置文件分解出来是最好的选择。


<h2>第16节：打包后如何调试</h2>

打包后的调试方式: ---> 生产Source Maps来方便我们的调试。

在使用webpack时只要通过简单的devtool配置，webapck就会自动给我们生产source maps 文件，map文件是一种对应编译文件和源文件的方法，让我们调试起来更简单。

四种选项

在配置devtool时，webpack给我们提供了四种选项。

source-map:在一个单独文件中产生一个完整且功能完全的文件。这个文件具有最好的source map,但是它会减慢打包速度；

cheap-module-source-map:在一个单独的文件中产生一个不带列映射的map，不带列映射提高了打包速度，但是也使得浏览器开发者工具只能对应到具体的行，不能对应到具体的列（符号）,会对调试造成不便。
eval-source-map:使用eval打包源文件模块，在同一个文件中生产干净的完整版的sourcemap，但是对打包后输出的JS文件的执行具有性能和安全的隐患。在开发阶段这是一个非常好的选项，在生产阶段则一定要不开启这个选项。
cheap-module-eval-source-map:这是在打包文件时最快的生产source map的方法，生产的 Source map 会和打包后的JavaScript文件同行显示，没有影射列，和eval-source-map选项具有相似的缺点。
四种打包模式，有上到下打包速度越来越快，不过同时也具有越来越多的负面作用，较快的打包速度的后果就是对执行和调试有一定的影响。

个人意见是，如果大型项目可以使用source-map，如果是中小型项目使用eval-source-map就完全可以应对，需要强调说明的是，source map只适用于开发阶段，上线前记得修改这些调试设置。

简单的配置：

module.exports = {
  devtool: 'eval-source-map',
  entry:  __dirname + "/app/main.js",
  output: {
    path: __dirname + "/public",
    filename: "bundle.js"
  }
}

总结：调试在开发中也是必不可少的，但是一定要记得在上线前一定要修改webpack配置，在打出上线包。


<h2>第17节：实战技巧：开发和生产并行设置</h2>

依赖不同
一个项目中是有开发环境和生产环境的，这两个环境的依赖也是不同的。

开发依赖：只在开发中用来帮助你进行开发，简化代码或者生成兼容设置的依赖包。你可以打开package.json来查看，devDependencies的下面的这些包为开发使用的包。这些包在生产环境中并没有用处。

生产依赖：就是比如我们的js使用了jquery，jquery的程序要在浏览器端起作用，也就是说我们最终的程序也需要这个包，这就是生产依赖。这些包在dependencies中。

npm install jquery --save

安装完成后，它存在于package.json的dependencies中，也就是说它是生产环境需要依赖的包（上线时需要的依赖包）。

安装完成后，它存在于package.json的devDependencies中，也就是说它是开发环境中需要的，上线并不需要这个包的依赖。

安装全部项目依赖包： --> npm install

安装生产环境依赖包：--> npm install --production

配置生产和开发并行

我们在以前的配置中设置了一个变量website，用于静态资源正确找到路径。那如果生产环境和开发环境不一样，而且我们需要来回切换，这时候我们需要更好的设置方法。

修改package.json命令

其实就是添加一个dev设置，并通过环境变量来进行区分，下面是package.json里的值。

 "scripts": {
    "server": "webpack-dev-server --open",
    "dev":"set type=dev&webapck",
    "build": "set type=build&webpack"
  },

修改webpack.config.js文件

可以利用node的语法来读取type的值，然后根据type的值用if–else判断。

    if(process.env.type== "build"){
        var website={
            publicPath:"http://192.168.0.104:1717/"
        }
    }else{
        var website={
            publicPath:"http://cdn.jspang.com/"
        }
    }

Mac下的package.json设置 --> MAC电脑下需要把set换成export，并且要多加一个&符，具体代码如下。

  "scripts": {
    "server": "webpack-dev-server --open",
    "dev":"export type=dev&&webpack",
    "build": "export type=build&&webpack"
  },


<h2>第18节：实战技巧：webpack模块化配置</h2>

这小节 很重要但是讲的很一般,我用白话概括吧!

把你想导出的文件直接 module.exports 进行导出。看哪里有需要 直接进行 import .... from '....js' ! 进行接收。

webpack模块

为了让大家容易看懂，我把webpack.config.js中的entry入口文件进行模块化设置，单独拿出来制作成一个模块。

首先在根目录，新建一个webpack_config文件夹，然后新建entry_webpack.js文件，代码如下：

总结：模块化在实际工作中是必不可少的操作，但是现在的webpack教程还很少讲到，大家一定要重视这节。


<h2>第19节：实战技巧：优雅打包第三方类库</h2>

这一节: 我还是用白话文进行介绍: 分别就是引入jquery 的两种方式:

方式一: 通过 impot $ from 'jquery'  此处的jquery 在node_mmodules 文件里面不需要配置路径;

方式二: 通过 用plugin引入 ProvidePlugin是webpack自带的插件  所以就直接 new ProvidePlugin({$: 'jquery'}) 即可;