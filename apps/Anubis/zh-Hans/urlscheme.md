---
layout: raw
---

# URL Scheme

### 1. 基本格式 (x-callback-url)

所有 query string 字段值都应该单独进行 URL Encode 编码，这里为了可读性，展示时均未编码。

```js
anubis://x-callback-url/$module?input=$input&x-source=sourceApp&x-cancel=xx://other.app.url&x-success=xx://other.app.url/path?input=$output
```

**$module**: 功能路径，如正则小工具 `tools/regex`

**$input**: 传给 Anubis 处理的数据
```json
{"text": "some text", "pbFileName": "xx.txt", "pbName": ""}
```
- `text`: 通过 URL 传递的文本，这时可忽略下面两个字段
- `pbFileName`: 当文本过长或者不是文本时，可以通过系统剪贴板传递文件，此为传递的文件名
- `pbName`: 传递文件的剪贴板名称，默认填空字符串`""`，即为系统默认剪贴板。当透过剪贴板传递的是文本，而不是文件时，可省略 `pbFileName` 和 `text` 字段，只表达为 `{"pbName": ""}`

**\$output**: Anubis 处理后回传的结果数据，以 `input=$output` 的方式附加到 `x-success` 的 query string 中


### 2. 小工具调用

#### 小工具列表
```js
anubis://x-callback-url/tools/?input=$input
```

#### 正则调试
```js
anubis://x-callback-url/tools/regex?input={"text": "some text", "pbFileName": "xx.txt", "pbName": "", "reg": "cd", "case": true, "global": false, "replace": "00"}
```

**$input**: 除了基本格式中的字段外，对于正则配置还有以下参数 
- `reg`: 正则表达式语句
- `replace`: 替换值文本
- `case`: true 忽略大小写，默认为 false
- `global`: 全局搜索，默认为 true


#### SSL 证书查看
```js
anubis://x-callback-url/tools/ssl?input=$input
```

#### 日期格式化
```js
anubis://x-callback-url/tools/date?input=$input
```

#### UUID 生成
```js
anubis://x-callback-url/tools/uuid?input=$input
```

#### Base64
```js
anubis://x-callback-url/tools/base64?input={"text": "some text", "pbFileName": "xx.txt", "pbName": "", "decode": false}
```
- `decode`: true 解码，false 编码，默认 false，可不填

#### URL Encode
```js
anubis://x-callback-url/tools/urlencode?input={"text": "some text", "pbFileName": "xx.txt", "pbName": "", "decode": false, "component": false}
```
- `decode`: true 解码，false 编码，默认 false，可不填
- `component`: 只对解码无意义，true 为 `Encode URL Compoent`, 默认 false, 可不填


#### 文本字符编码转换: 如 gbk -> utf-8
```js
anubis://x-callback-url/tools/stringEncode?input=$input
```

#### Native to ASCII
```js
anubis://x-callback-url/tools/native2ascii?input=$input
```

#### 数据转 16 进制字符
```js
anubis://x-callback-url/tools/date2hex?input=$input
```

#### 字符串转义
```js
anubis://x-callback-url/tools/stringEscape?input=$input
```

#### HTML 转义
```js
anubis://x-callback-url/tools/htmlEscape?input=$input
```

#### IDN 域名编码
```js
anubis://x-callback-url/tools/punnycode?input=$input
```

#### Quoted-printable
```js
anubis://x-callback-url/tools/quotedPrintable?input=$input
```

#### 散列/哈希
```js
anubis://x-callback-url/tools/hash?input={"text": "some text", "pbFileName": "xx.txt", "pbName": "", "alg": "MD5"}
```

- `alg`: `MD5, MD4, MD3, NSString.hash, SHA1, SHA224, SHA256, SHA384, SHA512`

#### Hmac
```js
anubis://x-callback-url/tools/hashSalt?input={"text": "some text", "pbFileName": "xx.txt", "pbName": "", "alg": "HmacMD5", "salt": "xxx"}
```

- `alg`: `HmacMD5, HmacSHA1, HmacSHA224, NSString.hash, SHA1, SHA224, SHA256, SHA384, SHA512`
- `salt`: Hmac 的 key，选填


#### 加密
```js
anubis://x-callback-url/tools/crypto?input={"text": "some text", "pbFileName": "xx.txt", "pbName": "", "alg": "AES128", "key": "xxx", "iv": "123", "mode": "cbc", "decrypt": false}
```

- `alg`: `AES128, AES192, AES256, DES, 3DES, RC4, RC2, Blowfish, Cast-128`
- `key`: 密钥
- `iv`: 向量
- `mode`: `CBC, ECB, CTR, CFB, CFB8, NOFB`，其中 `ECB` 不支持 `iv`
- `decrypt`: true 解密，false 加密，默认 false，可不填

| 算法 / 长度 (byte) | key | iv | block |
|:-------|:----|:----|:----|
| AES128 | 16 | 16 | 16 |
| AES192 | 24 | 16 | 16 |
| AES256 | 32 | 16 | 16 |
| DES | 8 | 8 | 8 |
| 3DES | 24 | 8 | 8 |
| RC4 | 1~512 | - | - |
| RC2 | 1~128 | 8 | 8 |
| Blowfish | 8~56 | 8 | 8 |
| Cast-128 | 5~16 | 8 | 8 |


#### Crypto.js 兼容
```js
anubis://x-callback-url/tools/crypto.js?input={"text": "some text", "pbFileName": "xx.txt", "pbName": "", "alg": "AES128", "key": "xxx", "decrypt": false}
```

- `alg`: `AES256, DES, 3DES, RC4`
- `key`: 密钥
- `decrypt`: true 解密，false 加密，默认 false，可不填


#### bz, gzip, deflate
```js
anubis://x-callback-url/tools/streamCompress?input={"text": "some text", "pbFileName": "xx.txt", "pbName": "", "alg": "gz", "compress": false}
```

- `alg`: `gz, bz, zlib`
- `compress`: true 压缩，false 解压，默认 false，可不填


#### HTTP chunked 提取
```js
anubis://x-callback-url/tools/chunked?input=$input
```


#### JSMin
```js
anubis://x-callback-url/tools/jsmin?input=$input
```