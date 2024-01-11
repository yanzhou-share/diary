# aliyun oss sts 及其header签名 JS端
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
    const AccessKeyId = 'STS.NUwTosBZb36ooLsVVMbajRzb9';
    const AccessKeySecret = '6d48YZDxGW4BNXisy6DUFWarWP6KB5dxmCvizmeoF9TE';
    const SecurityToken = 'CAIS9AF1q6Ft5B2yfSjIr5bCH9XHr4VDhPSEbWrCslYYbu5Gvb/J2zz2IHhMeHFpCOwWtfs+lGBR7/0SlqJoRoReREvCccZr8szPQs51xNOT1fau5Jko1beHewHKeTOZsebWZ+LmNqC/Ht6md1HDkAJq3LL+bk/Mdle5MJqP+/UFB5ZtKWveVzddA8pMLQZPsdITMWCrVcygKRn3mGHdfiEK00he8TomsPvnmpHFtUCH0QGqkbEvyt6vcsT+Xa5FJ4xiVtq55utye5fa3TRYgxowr/8u0PQdqGuX5Y7MUwkIuk7WKYjO+9hoNxRla7MmCxKDV3cYAGgRGoABFRtxeQfq++0HIl1JDoCZ02n1M0BAoB3RRt0SuLv2Ivzj/sYUwZ7HRUj1U/gkrW0+VobtvGf57HoDqXdt/BpHjsIU/BBrpYz5snX8n/PpqZWipm/+pW19vYYjQyIfI4GgYZmFkj2cJ26tEyRwY4T5I0MPSZEvoMUTAFLvqtxvN0IgAA==';
    const Content_MD5 = '';
    const Content_Type = '';
    const bucketname = 't-oss-test';
    const key = 'testram/wystory.txt';

    const [auth, Signature, Date1, CanonicalizedResource] = signedHead(verb, body.Credentials.AccessKeyId, body.Credentials.AccessKeySecret, body.Credentials.SecurityToken, Content_MD5, Content_Type, bucketname, key);
```