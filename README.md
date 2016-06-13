## 阿里大鱼API接口（短信接口）Thinkphp专版范例

> 提供方官网：http://www.alidayu.com/
>
> PHP版本：PHP>=5.3

### 配置说明

文件`/Application/Common/Conf/config.php`定义`AlidayuAppKey`和`AlidayuAppSecret`即可。获取，请参考官网！

### 使用说明

```php
<?php
/**
 * 阿里大鱼API接口（短信接口）Thinkphp专版范例
 *
 * @author Flc <2016-02-18 23:18:10>
 * @link http://flc.ren 
 * @link https://code.csdn.net/flc1125/alidayu
 */
namespace Home\Controller;

use Think\Controller;
use Alidayu\AlidayuClient as Client;
use Alidayu\Request\SmsNumSend;

class IndexController extends Controller
{
    /**
     * 阿里大鱼demo
     * @return [type] [description]
     */
    public function index()
    {
        $client  = new Client;
        $request = new SmsNumSend;

        // 短信内容参数
        $smsParams = [
            'code'    => $this->randString(),
            'product' => '测试的'
        ];

        // 设置请求参数
        $req = $request->setSmsTemplateCode('SMS_5053601')
            ->setRecNum('13312341234')
            ->setSmsParam(json_encode($smsParams))
            ->setSmsFreeSignName('活动验证')
            ->setSmsType('normal')
            ->setExtend('demo');

        print_r($client->execute($req));
    }

    /**
     * 获取随机位数数字
     * @param  integer $len 长度
     * @return string       
     */
    protected static function randString($len = 6)
    {
        $chars = str_repeat('0123456789', $len);
        $chars = str_shuffle($chars);
        $str   = substr($chars, 0, $len);
        return $str;
    }
}
?>
```

### 其他说明

- 目前仅开发短信相关功能，如需拓展，请在`/ThinkPHP/Library/Alidayu/Request/`目录下新增类，以开发更多功能接口！

- 开发文档参考网址：http://open.taobao.com/doc2/apiDetail.htm?spm=0.0.0.0.pjxLXY&apiId=25450