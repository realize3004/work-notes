#   在window10上调试 Safari
>[原文](https://washamdev.com/debug-a-website-in-ios-safari-on-windows/)
> ps: 一下调试均称为Debug

想在IOS设备的Safari上Debug一个网页(特别是Javascript与CSS)?但却因为没有Mac而感到苦恼?
我刚好遇到这个问题,我花了几个小时尝试其他的Debug方法.
最终我发现了一个非常简单的办法在我的Window10上加载Debug接口,通过这个接口可以显示关于页面在Safari上运行Debug信息.


>更新 2018/06/05 – 我之前在FireFox浏览器上找到了一个使用WebIDE的解决方法,仅需要一个Valence插件.
>
>不知道什么时候,可能是IOS 9把,这个方法失效了,
>
>我最近在尝试一些更加简单的方法让Debug能在Chrome DevTools中运行

这个方案将使用PC电脑上的Chrome浏览器与内建的Chrome DevTools,这些你应该早已轻车熟路.
但调试的内容将来自于Safari中的网页.


根据我在网上阅读的文章来看,这个方法只适用于Window 8或者更高版本.也就说它可能不能再Window 7上运行.


废话不多说,马上进入正文!


# Solution
为了与这篇文章相辅相成,我专门为这个方法录制了一个[视频教程](https://www.youtube.com/watch?time_continue=136&v=A9vA_R3w6eE).
>教程也添加了字幕翻译哦!

1. 在你的Windows 10上安装[iTunes](https://www.apple.com/itunes/download/)<br/><br/>
我已经安装了64-bit版本的iTunes.<br/>
我们主要需要iTunes提供的Apple移动端设备支持功能与对Apple应用的支持.<br/>
事实上在确保了其他应用安装后我删除了iTunes,<br/>
但是你需要安装iTunes来把设备连接至电脑.
所以你需要保证它正确安装,下面是你将会看到的.<br/><br/>
![debug-ios](https://washamdev.com/wp-content/uploads/2016/02/debug-ios-apple-apps-installed.png)


2. 安装[Node.js](https://nodejs.org/en/)<br/><br/>
在安装过程中需要确保勾选了包管理工具(npm,默认是勾选的),<br/>
我们需要用它来安装webkit适配器.


3. 以管理员身份运行PowerShell<br/><br/>
按下window键 + s打开搜索面板,然后搜索`PowerShell`即可,<br/>
在`Windows PowerShell`上右击后以管理员身份运行


4. 安装 `remotedebug-ios-webkit-adapter`<br/><br/>
使用下面提供的PowerShell命令<br/>
`npm install remotedebug-ios-webkit-adapter -g`<br/>
安装完成后,你将会看到`updated 1 package in Xs`信息.<br/><br/>
![powershell](https://washamdev.com/wp-content/uploads/2016/02/debug-ios-apple-powershell-adapter-installed.png)


5. 通过USB将你的IOS设备连接到Window 10电脑.<br/><br/>
如果你之前未曾链接过这个设备,你需要点击信任此设备的链接.


6. 运行`webkit adapter`插件,它将会监听于9000端口.<br/><br/>
暂停运行下面的命令到你的PowerShell上面:<br/>
`remotedebug_ios_webkit_adapter --port=9000`<br/>
你需要运行这个插件通过你的防火墙.
我使用Windows自带的防火墙,所以对话框大概张这个样子.<br/><br/>
![firewall](https://washamdev.com/wp-content/uploads/2018/05/debug-ios-apple-firewall.png)<br/><br/>
一旦运行成功,你将会看到一下信息<br/>
`remotedebug-ios-webkit-adapter is listening on port 9000 followed by iosAdapter.getTargets:`<br/><br/>
![iosAdapter](https://washamdev.com/wp-content/uploads/2016/02/debug-ios-apple-powershell-adapter-running.png)


7. 打开google浏览器,并访问一下地址[chrome://inspect/#devices](chrome://inspect/#devices)<br/><br/>
我们需要添加一个 `network target`,因为我们设置了`adapter`来监听9000端口.
点击`Discover network targets`紧接着的`Configure`<br/><br/>
![configure](https://washamdev.com/wp-content/uploads/2016/02/debug-ios-apple-network-target-configure.png)<br/>
然后我们需要确保`localhost:9000`在这个列表当中:<br/><br/>
![lists](https://washamdev.com/wp-content/uploads/2016/02/debug-ios-apple-add-network-target.png)


8. 在你的iOS设备上开启Web检查工具.<br/><br/>
在你的iOS设备上到`Settings > Safari > Advanced`中开启`Web Inspector`


9. 在你的iOS设备上打开Safari浏览器并且访问你要调试的页面.<br/><br/>
你几乎马上就能看到这个网页出现在你的Chrome中的`the Remote Target`板块下面.<br/><br/>
![remote-target](https://washamdev.com/wp-content/uploads/2016/02/debug-ios-apple-target-found.png)


10. 点击`target`下面的`inspect`.<br/><br/>
搞定!现在你可以调试Safari上的这个网页.但是你调试它是通过Windows电脑的Chrome开发者工具.


完成以上工作,大概也就用了5分钟时间,但是你现在却马上可以调试网站了!


# 使用 iOS 11?
如果想要在iOS11设备上运行,你可能需要一些额外的步骤.<br/>
明显的,`remotedebug-ios-webkit-adapter`当前版本还未支持iOS11.<br/>
用户bdice在`remotedebug-ios-webkit-adapter`的问题反馈中发表了一篇文章关于这个问题.其中说道他是如何在Windows10 上调试iOS 11设备的.<br/>
我做了这方面的测试,一下是具体步骤.<br/>


1. 下载`remotedebug-ios-webkit-adapter`最新发布的ZIP release包.<br/>
我下载的版本是1.8


2. 在一下目录中建立个文件夹名字叫`ios-webkit-debug-proxy-1.8-win64-bin`(这里假设你已经安装了node.js 并且是默认安装路径)<br/>
`%AppData%\npm\node_modules\remotedebug-ios-webkit-adapter\node_modules\vs-libimobile\`


3. 将ZIP文件解压到这个文件夹下面.<br/>
入股你满足我以上的假设与建议的话,这个路径应该是下面这个.<br/>
`%AppData%\npm\node_modules\remotedebug-ios-webkit-adapter\node_modules\vs-libimobile\ios-webkit-debug-proxy-1.8-win64-bin`


4. 编辑`iosAdapter.js`文件.<br/>
从以下路径中打开这个文件.<br/><br/>
`%AppData%\npm\node_modules\remotedebug-ios-webkit-adapter\out\adapters\iosAdapter.js`<br/><br/>
在132行修改这个`proxy`变量,用下面提供的值:<br/><br/>
`const proxy = path.resolve(__dirname, '../../node_modules/vs-libimobile/ios-webkit-debug-proxy-1.8-win64-bin/ios_webkit_debug_proxy.exe');`


当你通过了以上的所有步骤后,请重启Windows PowerShell(注意使用管理员身份),重启Chrome,并重新插拔iOS设备的数据线,只是为了保险起见.<br/>
执行以上步骤之后,返回上面的第6步,然后跳到第9步,你即将看到哦啊你的设备出现在`Remote Targets`当中.


我进行了相关测试,这绝对管用.


# 轮到你了!
你之前是否尝试过在Windows上调试Safari上的网页?<br/>
它是如何运作的?你使用了那些相关的插件呢?<br/>
或者你有任何关于此篇文章的问题吗?比如说想要讨论什么?<br/>
或者对以上解决方法有什么问题想讨论吗?<br/>
我很期待听到你的声音,让我们在下面讨论吧!<br/>


# 部分评论

1. 来自`Sri Harsha S`  三个月前<br />
无法工作,在chrome设备列表中,无法找到ipad.<br/><br/>
作者回复:Sri Harsha,<br/>
如果你在iOS 11设备上运行,你有没有跟着iOS 11而外的步骤操作?<br/>
其他人在此处也肯定了以上的步骤是可以成功在iOS设备上运行.<br/>
所以如果你遗忘了一些步骤或者某些事,你需要重新再一次执行以上问题.<br/>


2. 来自disquschan  三个月前<br/>
确实可以修复在iOS 11上的问题.<br/>
