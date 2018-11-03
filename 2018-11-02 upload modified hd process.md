# 2018-11-02 替换线上hd流程记录

1. 上传 `news-pro-modify` 文件夹 至 `/wp-content/themes/news-pro/` 目录下.

2. 修改`functions.php`文件, 在末尾追加一下代码.
```php
//  include news-pro-modify 2018-10-11
include_once( get_stylesheet_directory() . '/news-pro-modify/backend/init.php' );
```

3. 注释`/wp-content/themes/news-pro/js/global.js`文件中的一下代码.
```javascript
    // $( '.content, .sidebar' ).matchHeight({
    //     property: 'min-height'
    // });
```

4. 在后台小工具`Header Right`区块, 设置`image`小工具, 并上传首页Banner 尺寸为 `473px * 287px`.

5. 在后台小工具`Header Right`区块, 设置`Custom HTML`小工具, 设置首页Banner 下方处的最近更新时间.代码如下:
```html
<p class="lastUpdateTime">Update:[last_update_time]</p>
```

6. 在后台小工具`Primary Sidebar`处设置 `AddToAny Follow` 小工具. `Icon Size`为`42`, `Title`为 `FOLLOW US`.

7. 在后台小工具`Primary Sidebar`处设置 `Download App` 小工具. `Title`为`DOWNLOAD APP`.

8. 在后台小工具`Primary Sidebar`处设置 `Genesis - Featured Posts-pro` 小工具. `Title`为`PHOTOS`,并勾选`Photo Carousel`选项.

9. 在后台小工具`Footer 2`处设置 俩`Custom HTML` 小工具. 代码分别如下:
```html
<section class="footer-editorial-board">
	<h2>Editor-in-Chief</h2>
	<p>MASSIMO INTROVIGNE</p>
	<h2>Editor-in-Chief</h2>
	<p>MARCO RESPINTI</p>
</section>
```

```html
<p>CESNUR</p>
<p>Via Confienza 19,</p>
<p>10121 Torino, Ltaly,</p>
<p>Phone: 39-011-541950</p>
```

10. 在后台小工具`Footer 3`处设置 `Custom HTML` 小工具. 代码如下:
```html
<p>
	WE welcome submission of WE welcome submission ofWE welcome submission ofWE welcome submission ofWE welcome submission ofWE welcome submission ofWE welcome submission ofWE welcome submission of
    <a href="mailto:youremailaddress">CONTRIBUTIONs@BITTERWINTER.ORG</a>
    Thank you
</p>
```

11. 在后台小工具`Footer 3`处设置 `MailChimp Sign-Up Form` 小工具.

12. 在后台小工具`Footer 4`处设置 `Archives` 小工具.

12. 在后台小工具`Footer 5`处设置 `AddToAnyFollow` 小工具.

13. 在后台小工具`Footer 5`处设置 `Download App` 小工具. `Icon Size`为`30`.

14. 在后台小工具`Footer 5`处设置 `Custom HTML` 小工具. 代码如下:
```html
    <a href="https://tr.kingdomsalvation.org/android-app.html">
        <img src="https://www.kingdomsalvation.org/wp-content/uploads/app-icon.png" alt="" width="100%">
    </a>
    <a href="https://tr.kingdomsalvation.org/android-app.html">
        <img src="https://www.kingdomsalvation.org/wp-content/uploads/app-icon.png" alt="" width="100%">
    </a>
    <a href="https://tr.kingdomsalvation.org/android-app.html">
        <img src="https://www.kingdomsalvation.org/wp-content/uploads/app-icon.png" alt="" width="100%">
    </a>
```

15. 在后台`Genesis - Simple Edits`处设置网站底部描述:

16. 关掉`Related Posts`与`Wordpress Related Posts`中自动在文章下方输出关联功能.

17. 设置`Related Posts`样式[如图所示](https://drive.google.com/open?id=15S3cXlvTLBkIlb5vtNPXO6f0NMsqBpfY)

18. 设置`Wordpress Related Posts`样式[如图所示](https://drive.google.com/open?id=1D9Xo3z-5iN-5H0TpDh_e_4Fy3kpUfwt5)

19. 修改`/wp-content/themes/news-pro/single.php`,内容如下
    + 删除`itemscope`与`itemtype`属性,避免与`News`结构化数据冲突.
    ```php
    <article id="post-<?php the_ID(); ?>" <?php post_class(); ?>>
    ```
    + 添加一下代码,并删除之前的
    ```php
    <?php
    if ( function_exists( 'wp_related_posts' ) ) {
        wp_related_posts();
    }
    if ( function_exists( 'get_yuzo_related_posts' ) ) {
        get_yuzo_related_posts();
    }
    ?>
    ```

20. 修改`Appearance`->`Customize`->`Site Identity`中的上传logo.
