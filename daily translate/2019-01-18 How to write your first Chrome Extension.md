# 2018-10-27 Optimize Gospel of Backend

## Learned
1.[WebPageTest](https://www.youtube.com/watch?v=OUz-T-mFHWo)

2.[浏览器工作原理](https://github.com/amandakelake/blog/issues/55)

## Problem
1.天国福音在有缓存情况下执行并不慢, 但内存占用却很高
+ 涉及video数据处理时,普遍慢内存高cpu占用大.原因是需要遍历`video`所有数据去处理
```php
 $this->all_videos = $this->vcClient->getData( 'slug_video_map' );
```

+ 在初始化处理分类信息时,调用太多的`gp__`函数,虽然只有几十个,但问题主要出现在`gp__`遍历翻译数组**太慢**
```php
gp__( '心灵港湾', 'page-gospel' )
```

## Solution
1. 将所有操作`video`的方法是用`gp_get_data()`来处理,让其能读到缓存,减少不必要的资源消耗
2. 定义`$this->set_all_videos()`方法,当调用`$this->all_videos`在进行赋值
3. 取消`gp_get_data`中的`functions`
4. 将分类初始化信息分割出来调用缓存,并实现以下方法
```php
	/**
		 * 获取redis缓存数据
		 * 主要解决 gp_get_data 如果在 __construct 中调用时将会出现死循环
		 *
		 * @param $name     模块名
		 * @param array $args 参数
		 *
		 * @return array|mixed|null
		 */
		private function gp_get_cache( $name, $args = array() ) {
			$page_name = 'page-gospel';
			//  1. 判断是否已经存在缓存
			$cache = gp_get_redis( $page_name, $name, $args );
			if ( $cache['status'] ) {
				return $cache['data'];
			}

			//  2. 如果不存在, 调用方法 并 填入到缓存中
			$data = null;
			if ( method_exists( $this, $name ) ) {
				$data = call_user_func( array( $this, $name ), $args );
			} else {
				echo '<pre>';
				print_r( '调用不存在方法' . $name );
				die;
			}

			//  3. 存入缓存
			gp_set_redis( $page_name, $name, $args, $data );

			return $data;
		}
```
