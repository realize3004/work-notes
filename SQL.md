# 记录SQL常用代码

1.
```mysql
UPDATE wp_options SET option_value = replace(option_value, 'https://www.target.com', 'http://www.localhost.com') WHERE option_name = 'home' OR option_name = 'siteurl';

UPDATE wp_posts SET guid = replace(guid, 'https://www.target.com','http://www.localhost.com');

UPDATE wp_posts SET post_content = replace(post_content, 'https://www.target.com', 'http://www.localhost.com');

UPDATE wp_postmeta SET meta_value = replace(meta_value,'https://www.target.com','http://www.localhost.com');


# -----------------------------------

UPDATE wp_users SET user_pass = '$P$BT8IGTho0ovRaL6yv7QspkL/lvVIt9/';



# -----------------------------------
# admin / admin

UPDATE wp_users SET user_login='admin', user_nicename='admin', user_pass = '$P$BhQSP48BFMtyK9IaYD/yds0dEQRkCx/';
```
