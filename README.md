# zmxy-php-sdk
基于composer的php-sdk

调试中项目

https://b.zmxy.com.cn/technology/openDoc.htm?relInfo=CERTIFICATION_QUICK_START

use \zmxy\ZmopClient;
use \zmxy\api\ZhimaCustomerCertificationInitializeRequest;
use \zmxy\api\ZhimaCustomerCertificationCertifyRequest;

--------- function start ----------
$client = new \zmxy\ZmopClient(self::$gatewayUrl, self::$appId, self::$charset, self::$privateKeyFilePath, self::$zhiMaPublicKeyFilePath);
$request = new \zmxy\api\ZhimaCustomerCertificationInitializeRequest();
$request->setPlatform('zmop');
$request->setTransactionId(self::generateTransactionId());
$request->setProductCode('w1010100000000002978');
$request->setBizCode('FACE');
$request->setIdentityParam("{\"identity_type\":\"CERT_INFO\",\"cert_type\":\"IDENTITY_CARD\",\"cert_name\":\"收委\",\"cert_no\":\"260104197909275964\"}");
$request->setExtBizParam("{}");
$init = (array)$client->execute($request);
if(!$init || !$init['biz_no']){
    return false;
}
$request2 = new \zmxy\api\ZhimaCustomerCertificationCertifyRequest();
$request2->setBizNo($init['biz_no']);
$request2->setReturnUrl($callbackUrl);
//生成认证url
$url = $client->generatePageRedirectInvokeUrl($request2);
--------- function end ----------
