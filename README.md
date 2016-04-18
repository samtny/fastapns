FastAPNS [![SensioLabsInsight](https://insight.sensiolabs.com/projects/6f8352c8-7cde-421b-b3d0-08ade1ed76bc/mini.png)](https://insight.sensiolabs.com/projects/6f8352c8-7cde-421b-b3d0-08ade1ed76bc) [![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/samtny/fastapns/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/samtny/fastapns/?branch=master)
==========

This library will send push notifications to Apple as fast as possible, and report any bad tokens.

Inspired by this StackOverflow post:

http://stackoverflow.com/a/18491136/1569360

...  and careful reading of 'Troubleshooting Push Notifications' here:

https://developer.apple.com/library/ios/technotes/tn2265/_index.html#//apple_ref/doc/uid/DTS40010376-CH1-TNTAG44

Example Usage:

```php
$payload = array(
    'aps' => array(
        'alert' => 'some alert',
    ),
);

$tokens = array(
    'ca360e9029938b9ed8ed435640f3760620526bd72037017d3c50cfa264b7914f',
    'ca360e9029938b9ed8ed435640f3760620526bd72037017d3c50cfa264b79150',
    'ca360e9029938b9ed8ed435640f3760620526bd72037017d3c50cfa264b79151',
    'ca360e9029938b9ed8ed435640f3760620526bd72037017d3c50cfa264b79152',
    'ca360e9029938b9ed8ed435640f3760620526bd72037017d3c50cfa264b79153',
);

$expiry = (new \DateTime('+24 hours'))->getTimestamp();

$client = FastAPNS\ClientBuilder::create()
    ->setLocalCert(__DIR__ . '/ssl/MyAppCertificate.includesprivatekey.pem')
    ->setPassphrase('p@ssword')
    ->build();

$client->send($payload, $tokens, $expiry);

var_dump($client->getBadTokens());
```

Ensure that your APNS certificate is encoded in PEM format and includes the private key.  This file should be set to mode 0400.

END
