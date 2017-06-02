# zmxy-php-sdk
基于composer的php-sdk

调试中项目

https://b.zmxy.com.cn/technology/openDoc.htm?relInfo=CERTIFICATION_QUICK_START

use \zmxy\ZmopClient;
use \zmxy\api\ZhimaCustomerCertificationInitializeRequest;
use \zmxy\api\ZhimaCustomerCertificationCertifyRequest;

--------- function start ----------<br/>
$client = new \zmxy\ZmopClient(self::$gatewayUrl, self::$appId, self::$charset, self::$privateKeyFilePath, self::$zhiMaPublicKeyFilePath);<br/>
$request = new \zmxy\api\ZhimaCustomerCertificationInitializeRequest();<br/>
$request->setPlatform('zmop');<br/>
$request->setTransactionId(self::generateTransactionId());<br/>  
$request->setProductCode('w1010100000000002978');<br/>  
$request->setBizCode('FACE');<br/>
$request->setIdentityParam("{\"identity_type\":\"CERT_INFO\",\"cert_type\":\"IDENTITY_CARD\",\"cert_name\":\"收委\",\"cert_no\":\"260104197909275964\"}");<br/>
$request->setExtBizParam("{}");<br/>
$init = (array)$client->execute($request);<br/>
if(!$init || !$init['biz_no']){<br/>
    return false;<br/>
}<br/>
$request2 = new \zmxy\api\ZhimaCustomerCertificationCertifyRequest();<br/>
$request2->setBizNo($init['biz_no']);<br/>
$request2->setReturnUrl($callbackUrl);<br/>
//生成认证url<br/>
$url = $client->generatePageRedirectInvokeUrl($request2);<br/>
--------- function end ----------
