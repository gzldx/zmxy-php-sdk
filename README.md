# zmxy-php-sdk
基于composer的php-sdk

## 调试中项目

### 文档路径
https://b.zmxy.com.cn/technology/openDoc.htm?relInfo=CERTIFICATION_QUICK_START

#### composer.json
```
"repositories": [
    {
        "type": "composer",
        "url": "https://packagist.phpcomposer.com"
    },
    {
        "packagist": false
    },
    {
        "type": "vcs",
        "url": "https://github.com/gzldx/zmxy-php-sdk"
    }
],
"require": {
    "zmxy/php-sdk": "dev-master"
},
```

#### 调用

```  
use \zmxy\ZmopClient;  
use \zmxy\api\ZhimaCustomerCertificationInitializeRequest;  
use \zmxy\api\ZhimaCustomerCertificationCertifyRequest;  

//function start
$client = new \zmxy\ZmopClient(self::$gatewayUrl, self::$appId, self::$charset, self::$privateKeyFilePath, self::$zhiMaPublicKeyFilePath);  
$ci_request = new \zmxy\api\ZhimaCustomerCertificationInitializeRequest();  
$ci_request->setPlatform('zmop');  
$ci_request->setTransactionId(self::generateTransactionId());  
$ci_request->setProductCode('w1010100000000002978');  
$ci_request->setBizCode('FACE');  
$ci_request->setIdentityParam("{"identity_type":"CERT_INFO","cert_type":"IDENTITY_CARD","cert_name":"收委","cert_no":"260104197909275964"}");  
$ci_request->setExtBizParam("{}");
//获取本次请求标示biz_no
$result = (array)$client->execute($ci_request);
if(!$result || !$result['biz_no']){
    return false;
}
$cc_request = new \zmxy\api\ZhimaCustomerCertificationCertifyRequest();
$cc_request->setBizNo($result['biz_no']);
$cc_request->setReturnUrl($callbackUrl);
//生成认证url
$url = $client->generatePageRedirectInvokeUrl($cc_request);
```
