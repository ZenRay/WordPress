# WordPress官网429 too many requests无法访问和在线安装更新的解决办法

从2019年10月初开始，国内访问 wordpress.org 官网一直提示 429 Too Many Requests，导致很多时候没办法在线更新WordPress核心、主题和插件，不知道为什么两个多月了，还是没有解决这个问题。

![img](https://static.wpdaxue.com/img/2019/11/20191113163820_wpdaxue_com.jpg)429 Too Many Requests

## 最佳办法

[闪电博](https://www.wbolt.com/plugins/kill-429?invite=2363)最近开发了一个插件 **Kill 429** ，插件通过优化中国境内服务器访问WordPress数据服务器的网络（实际上就是“代--理”），解决429报错问题，快速安装WordPress版本、主题和插件更新。**[点此下载 Kill 429 插件](https://static.wpdaxue.com/img/2013/08/kill-429.1.0.0.zip)**，然后在后台 插件->安装插件 界面上传安装，启用后，就可以正常在线更新WordPress核心、主题和插件了，插件自带了代---理线路，有能力的可以自己修改为自己的线路，在此不做讨论。

![img](https://static.wpdaxue.com/img/2019/12/20191217205829_wpdaxue_com.jpg)

## 其他办法

最近看到 [https://www.wpsilo.com](https://www.wpsilo.com/wordpress-429.html) 的博主搭建了一个 wordpress.org 网站镜像，基本上就是wordpress.org的翻版，download，plugins，themes，showcase，文档都做了镜像。国内用户可以通过下面的网址进行访问：

- WordPress简体中文站： [http://cn.wp101.net](http://wp101.net/) 
- WordPress英文站： [http://wp101.net](http://wp101.net/) 

此外，无法在后台更新wordpress最新版的朋友们，可以把以下代码保存为wpsilo-update.php，并上传到wordpress的插件目录 `wp-content/plugins` ，启用插件。然后在线更新wordpress，更新完之后停用插件，下次更新wordpress再启用插件即可。

> 为方便大家，倡萌已经将下面的代码添加为插件安装包，[点击下载 wpsilo-update.zip](https://static.wpdaxue.com/img/2013/08/wpsilo-update.zip) ，在后台 插件>安装插件 界面上传安装即可。

```php
/*
Plugin Name: wp101.net中文下载镜像
Plugin URI: https://wpsilo.com/wordpress-429.html
Description: wp101.net中文下载镜像
Version: 1.0
Author: wpsilo.com
Author URI: http://wpsilo.com
*/
add_filter('site_transient_update_core', function($value){
	foreach ($value->updates as &$update) {
		if($update->locale == 'zh_CN'){
			$update->download	= 'http://cn.wp101.net/latest-zh_CN.zip';
			$update->packages->full	= 'http://cn.wp101.net/latest-zh_CN.zip';
		}
	}
 
	return $value;
});
```