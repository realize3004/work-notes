#   如何创建一个Chrome extension

>[原文](https://medium.freecodecamp.org/how-to-create-and-publish-a-chrome-extension-in-20-minutes-6dc8395d7153)

有没有想过创建Chrome extension会是怎么样的?在这里我会告诉你它有多简单,跟着这些步骤走你的想法将会变成现实!并且你可以立刻发布一个真正的`extension`在Chrome商店中.

# 什么是Chrome Extension?
Chrome Extension 允许你添加一些功能到Chrome浏览器上,而不需要修改页面源代码.这很厉害,因为你可以用Web开发者最熟悉的核心知识`CSS`,`HTML`,`Javascript`来为Chrome开发一个新插件.如果你曾经有开发网页的经验,那么开发一个插件甚至比你吃一顿饭还快.你唯一需要学习的事是如何使用Chrome提供出来的`Javascript API`添加一些功能到Chrome上.

如果你还没有开发页面的经验,我建议还是先通过一些免费的资源去学习如何开发,比如 [freeCodeCamp](https://www.freecodecamp.org/)

# 你想开发什么功能?
在你开发之前,你需要对你想要开发的功能有个大致的想法.它并不需要是一些开创性的想法,我们可以仅仅为了好玩去开发.在这篇文章中,我将会告诉你我的想法还有如何在一个Chrome Extension中实现它.
>所以也就是你在如果是看着这篇文章跟着尝试开发,你并不需要什么想法...只需要跟着作者做就行.但是在你要独立开发时,你就需要一些想法了

# 计划
我用过[Unsplash](https://chrome.google.com/webstore/detail/unsplash-instant/pejkokffkapolfffcgbmdmhdelanoaih)这个插件一段时间,这使我通过[Unsplash](https://chrome.google.com/webstore/detail/unsplash-instant/pejkokffkapolfffcgbmdmhdelanoaih)在新的`TAB`上得到一些不错的背景.
后来我使用[Muzli](https://muz.li/)插件代替的它,这使得默认的`TAB`变成了可以从整个互联网中获取关于设计新闻与例子的页面.

让我们使用这俩插件的灵感,来开发一个新的,这一次比较适合于电影爱好者.我的想法是在每次你打开新的`TAB`时显示一些关于电影的背景图片.
当滚动它时,将会得到一些热门电影与电视节目的好消息.

# 步骤1: 设置一些东西
第一步是创建一个`manifest`文件,名字叫做`manifest.json`.
这是一个Json格式的包含属性的元数据文件,比如像你的插件名,描述,版本号之类的.
在这个文件中,我们将会告诉chrome这个插件将会处理什么与需要哪些权限.

针对于这个`movie`插件,我们需要控制`activeTab`的权限.所以我们的`manifest.json`文件看起来像这样:

```json
    {
     // manifest版本, 不需要做改动
     "manifest_version": 2,
     // 插件名
     "name": "RaterFox",
     // 描述
     "description": "The most popular movies and TV shows in your   default tab. Includes ratings, summaries and the ability to watch trailers.",
     // 插件版本
     "version": "1",
     // 作者名
     "author": "Jake Prins",
     "browser_action": {
       "default_icon": "tab-icon.png",
       "default_title": "Have a good day"
      },
     // url地址覆盖
     "chrome_url_overrides" : {
      "newtab": "newtab.html"
     },
     "permissions": ["activeTab"]
    }
```

正如你所见的一样,`newtab.html`将会是一个`HTML`文件,它将会在每次新的`TAB`打开时被渲染.
要想实现它我们必须要有控制`activeTab`的权限,所以当用户尝试安装这个插件时,
他将会得到一个关于此插件所需的权限警告.

![warn](https://cdn-images-1.medium.com/max/1600/1*jMmZo8AUvcf01GMxTnXqZg.png)

另外比较有趣的事是关于`manifest.json`内的`browser actions`.
在这个例子中我们使用它设置了标题,但这里有很多的参数.例如,每当你点击地址栏中这个插件的图标时要弹出一个页面,你需要做的事像这样:
```json
"browser_action": {
  "default_popup": "popup.html",
 },
```
现在,`popup.html` 将会在弹出窗口里面被渲染,这个弹窗是为了响应用户点击浏览器的行为而创建.



