yii2-helpers: 助手类,通用上传类
==================

安装:
------------
使用 [composer](http://getcomposer.org/download/) 下载:
```
# 旧版本:
composer require --prefer-dist moxuandi/yii2-helpers:"~0.1"

# 最新发布版:
composer require --prefer-dist moxuandi/yii2-helpers:"*"

# 开发版:
composer require --prefer-dist moxuandi/yii2-helpers:"dev-master"
```


用法示例:
-----
```php
// 判断当前服务器操作系统, eg: 'Linux'或'Windows'.
echo Helper::getOs();

// 获取当前微妙数, eg: 1512001416.3352.
echo Helper::microtime_float();

// 格式化文件大小, eg: '1.46 MB'.
echo Helper::byteFormat(1532684);

// 获取图片的宽高值, eg: ['width'=>1366, 'height'=>768].
echo Helper::getImageInfo('uploads/image/201707/1512001416.jpg');

// 获取指定格式的文件路径: eg: 'uploads/image/201707/1512001416.jpg'.
echo Helper::getFullName('img.jpg', 'uploads/image/{yyyy}{mm}/{time}', 'jpg');

// 获取指定文件路径的文件名部分: eg: '1512001416.jpg'.
echo Helper::getFileName('uploads/image/201707/1512001416.jpg');

// 获取文件的扩展名, eg: 'jpg'.
echo Helper::getExtension('uploads/image/201707/1512001416.jpg');

// 通过字符串替换, 获取缩略图路径. eg: 'uploads/thumb/201707/1512001416.jpg'
echo Helper::getThumb('uploads/image/201707/1512001416.jpg');

// 修正路径. eg: 'D:\wamp64\www\web'
echo Helper::trimPath('D:\wamp64\www/web');


// 创建新目录, 使用 yii\helpers\FileHelper::createDirectory() 方法:
echo FileHelper::createDirectory('uploads/image/201707');

// 规范化文件/目录路径, 使用 yii\helpers\FileHelper::normalizePath() 方法:
echo FileHelper::normalizePath('uploads/image/201707/1512001416.jpg');

// 遍历文件夹, 获取某个目录的所有文件, 使用 yii\helpers\FileHelper::findFiles() 方法:
$files = FileHelper::findFiles(Yii::getAlias('@webroot'));
```

调用上传类:
```php
$config = [
	'maxSize' => 1*1024*1024,  // 上传大小限制
	'allowFiles' => ['.png', '.jpg', '.jpeg'],  // 允许上传的文件类型
	'pathFormat' => '/uploads/image/{time}',  // 文件保存路径
	'thumbStatus' => false,  // 是否生成缩略图
	'thumbWidth' => 300,  // 缩略图的宽度
	'thumbHeight' => 200,  // 缩略图的高度
	'thumbMode' => 'outbound',  // 生成缩略图的模式, 可用值: 'inset'(补白), 'outbound'(裁剪)
];
$up = new Uploader('upfile', $config);
echo Json::encode([
    'url' => $up->fullName,
    'state' => $up->stateInfo
]);
```

说明: 为兼容 UEditor编辑器(http://ueditor.baidu.com), `$config['allowFiles'])`中的扩展名全都带有前缀'.', eg: ['.png', '.jpg', '.jpeg'].



开发进度:
-----
1. 上传 ----- 完成
2. 缩略图 ----- 完成
3. 分片上传 ----- 完成
4. 拉取远程图片 ----- 
5. 处理base64编码图片 ----- 完成
6. 保存上传信息到数据库 ----- 
7. 水印图片和文字 ----- 
8. Image 的其他应用(添加边框, 裁剪, 旋转) ----- 
