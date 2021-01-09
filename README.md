# thinkphp5.x 前后端分离图像验证码
thinkphp5.x 图像验证码拓展，可在前后端分离项目使用

本拓展只是将官方验证码类拓展，在不影响原代码情况下，新增一个可在前后端分离项目中使用的接口

接口返回类型如下：

```
{
	// 图像验证码ID
    "uniqid": "9a721d42b98946876bf6737f6bf89976",
	// 验证码图片base64 
    "content": "data:image/jpg/png;base64,为了好看，省略n字符"
}
```



## 使用 Composer 安装
```shell
$ composer require 18y/think-jwt-captcha
```
## 使用方式

在控制器中使用下面的代码进行验证码生成


```php
<?php
namespace app\index\controller;

use JwtCaptcha\JwtCaptcha;

class Index
{
	// 验证码配置，详细文档看官方 https://www.kancloud.cn/manual/thinkphp5_1/354122
	private $config = [
	    // 验证码密钥
	    'seKey'    => 'xiadmin.com',
	    // 验证码图片高度
	    'imageH'   => 34,
	    // 验证码图片宽度
	    'imageW'   => 130,
	    // 验证码字体大小(px)
	    'fontSize' => 18,
	    // 验证码位数
	    'length'   => 3,
	    // 是否画混淆曲线  
	    'useCurve'   => false,
	    // 是否添加杂点
	    'useNoise'   => false,
	];

	// 生成验证码
    public function verify()
    {
		$captcha = new JwtCaptcha($this->config);
		return $captcha->getEntry();
    }

    // 验证输入验证码是否正确
    public function verify_check()
    {
    	// 验证码ID
    	$uniqid = '9a721d42b98946876bf6737f6bf89976';
    	// 用户输入验证码
    	$code = 'abb';
		$captcha = new JwtCaptcha($this->config);
	    $result = $captcha->checkCaptcha($uniqid, $code);
	    if(!$result)
	    {
	    	// 验证码错误
	    }
    }
}


```