# aliyun oss sts 及其header签名 JS端

* 注：aliyun 由于header中需要传递Date 和 CanonicalizedResource参数，与浏览器安全策略有冲突，所以只能用URL签名实现
## header签名
```javascript
    function signedHead(verb, AccessKeyId, AccessKeySecret, SecurityToken, Content_MD5, Content_Type, bucketname, key) {
        const Date1 = new Date().toUTCString();
        const CanonicalizedOSSHeaders = 'x-oss-security-token:' + SecurityToken;
        const CanonicalizedResource = `/${bucketname}/${key}`;
        const content = `${verb}\n${Content_MD5}\n${Content_Type}\n${Date1}\n${CanonicalizedOSSHeaders}\n${CanonicalizedResource}`;
        console.log('content:', content)
        const hmac = crypto.createHmac('sha1', AccessKeySecret);
        hmac.update(content);
        const Signature = hmac.digest('base64');
        const auth = `OSS ${AccessKeyId}:${Signature}`;
        return [auth, Signature, Date1, CanonicalizedResource];
    }

    const verb = 'GET';
    const AccessKeyId = '';
    const AccessKeySecret = '';
    const SecurityToken = 'CAIS9AF1q6Ft5B2yfSjIr5bCH9XHr4VDhPSEbWrCslYYbu5Gvb/J2zz2IHhMeHFpCOwWtfs+lGBR7/0SlqJoRoReREvCccZr8szPQs51xNOT1fau5Jko1beHewHKeTOZsebWZ+LmNqC/Ht6md1HDkAJq3LL+bk/Mdle5MJqP+/UFB5ZtKWveVzddA8pMLQZPsdITMWCrVcygKRn3mGHdfiEK00he8TomsPvnmpHFtUCH0QGqkbEvyt6vcsT+Xa5FJ4xiVtq55utye5fa3TRYgxowr/8u0PQdqGuX5Y7MUwkIuk7WKYjO+9hoNxRla7MmCxKDV3cYAGgRGoABFRtxeQfq++0HIl1JDoCZ02n1M0BAoB3RRt0SuLv2Ivzj/sYUwZ7HRUj1U/gkrW0+VobtvGf57HoDqXdt/BpHjsIU/BBrpYz5snX8n/PpqZWipm/+pW19vYYjQyIfI4GgYZmFkj2cJ26tEyRwY4T5I0MPSZEvoMUTAFLvqtxvN0IgAA==';
    const Content_MD5 = '';
    const Content_Type = '';
    const bucketname = 't-oss-test';
    const key = 'testram/wystory.txt';

    const [auth, Signature, Date1, CanonicalizedResource] = signedHead(verb, body.Credentials.AccessKeyId, body.Credentials.AccessKeySecret, body.Credentials.SecurityToken, Content_MD5, Content_Type, bucketname, key);
```

## url签名
```javascript
    const OSS = require('ali-oss');

    var body = {
        "AssumedRoleUser": {
        "Arn": "acs:ram::1117004172154836:role/ramosstest/sessiontest",
        "AssumedRoleId": "300401948379881138:sessiontest"
        },
        "Credentials": {
        "AccessKeyId": "STS.NUTggEQi9aB9g7jaooZWvBars",
        "AccessKeySecret": "6tJaZRTGRe5CtnGoAFaXxKCzKpsxqqfo1MmDPnpqrsq7",
        "Expiration": "2024-01-12T08:16:01Z",
        "SecurityToken": "CAIS9AF1q6Ft5B2yfSjIr5bhLN3xvLYY1oDSZRHbhW86VtharaTZkTz2IHhMeHFpCOwWtfs+lGBR7/0SlqJoRoReREvCccZr8szyFJMsxNOT1fau5Jko1beHewHKeTOZsebWZ+LmNqC/Ht6md1HDkAJq3LL+bk/Mdle5MJqP+/UFB5ZtKWveVzddA8pMLQZPsdITMWCrVcygKRn3mGHdfiEK00he8TomsPvnmpHFtUCH0QGqkbEvyt6vcsT+Xa5FJ4xiVtq55utye5fa3TRYgxowr/8u0PQdqGuX5Y7MUwkIuk7WKYjO+9hoNxRla7MmCxKDV3cYAGgRGoABRNJ+I7mgqccdK+KkpNSKc8RbKv+hG3Ijo2TRvDVRgUd3WiXzmVusjjZeXCD8zoxs74ycLyGdQYix5UWwQHOiCIQ0Kmnw4pDRK8d287/dGZGu0n3CwqtrPBGKoRBnW9Q2J1tEh+SKm1AsLtca4cPws7dFGuK97qH1Wc/Nx1HHYx0gAA=="
        },
        "RequestId": "889A5E52-4397-5A1A-BAF6-2A63E3DFA4C0"
    }

  const client = new OSS({
    region: 'oss-cn-hangzhou',
    accessKeyId: body.Credentials.AccessKeyId,
    accessKeySecret: body.Credentials.AccessKeySecret,
    stsToken: body.Credentials.SecurityToken,
    endpoint: 'oss-cn-hangzhou.aliyuncs.com',
    bucket: 't-oss-test'
  });
OpenSeadragon.extend(OpenSeadragon.DziTileSource.prototype, {
    getTileUrl: function( level, x, y ) {
        var bucketname = 't-oss-test'

        const signedUrl = client.signatureUrl(`tilized/m3g/02d37fd048e44917a35db766bbd87bfd/02d37fd048e44917a35db766bbd87bfd_files/${level}/${x}_${y}.jpg`, {
        expires: 3600
        })

        return String(signedUrl)
    }
})
```