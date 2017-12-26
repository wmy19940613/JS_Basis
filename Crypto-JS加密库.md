## Crypto-JS加密库
+ 什么是Crypto-JS加密库
   - 加密库一般用在用户登录的密码，注册密码，用于前端加密。
   - 在实际项目开发中可用md5进行加密
   ```
   var token = CryptoJS.MD5(time).toString(); //并将其转换成字符串形式
   ```
+ 作用：用前端框架加密后再进行传输，以提高密码传输过程中的安全性。
+ 使用方式：
   - 首先下载crypto-js.方式一：官网下载：http://cryptojs.altervista.org/但需要翻墙才行
   - 方法二：github上面下载
   - 正常下载解压后会有两个文件夹：rollups 和 components rollups下面是整合后的js,每一个可以单独通过js引用使用. componets下面刚包括所有的组件源码，以及各组件压缩后的js文件
  ```
  下面均以MD5为例：
     1).引用rollups下面的文件：
    [javascript] view plain copy 
    <script src="你的文件路径/rollups/md5.js"></script>  
    //js代码：  
    var md5 = CryptoJS.MD5("你想加密的内容");  
     2).引用components下面的文件：
    [javascript] view plain copy 
    <script src="你的文件路径/components/core-min.js"></script>  
    <script src="你的文件路径/components/md5-min.js"></script>  
    //js代码：  
    var md5 = CryptoJS.MD5("你想加密的内容");  
    console.log(md5)//这里打印的就是对你要加密的内容进行了加密，你会看到一堆数字加字母的串（base64的密文）。这就是加密后的效果。

  ```
   - 方法三：npm 下载
```
有一个crypto-js插件，可以用npm进行下载，然后可以编写一个加解密的工具类。代码如下:

import CryptoJS from 'crypto-js'
function getAesString(data,key,iv){//加密
    var key  = CryptoJS.enc.Utf8.parse(key);
    //alert(key）;
    var iv   = CryptoJS.enc.Utf8.parse(iv);
    var encrypted =CryptoJS.AES.encrypt(data,key,
        {
            iv:iv,
            mode:CryptoJS.mode.CBC,
            padding:CryptoJS.pad.Pkcs7
        });
    return encrypted.toString();    //返回的是base64格式的密文
}
function getDAesString(encrypted,key,iv){//解密
    var key  = CryptoJS.enc.Utf8.parse(key);
    var iv   = CryptoJS.enc.Utf8.parse(iv);
    var decrypted =CryptoJS.AES.decrypt(encrypted,key,
        {
            iv:iv,
            mode:CryptoJS.mode.CBC,
            padding:CryptoJS.pad.Pkcs7
        });
    return decrypted.toString(CryptoJS.enc.Utf8);      //
}
export function getAES(data){ //加密
    var key  = 'AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA';  //密钥
    var iv   = '1234567812345678';
    var encrypted =getAesString(data,key,iv); //密文
    var encrypted1 =CryptoJS.enc.Utf8.parse(encrypted);
    return encrypted;
}

export function getDAes(data){//解密
    var key  = 'AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA';  //密钥
    var iv   = '1234567812345678';
    var decryptedStr =getDAesString(data,key,iv);
    return decryptedStr;
}
```
+ 项目中使用过的例子：
```
1. 在package.json里面添加"crypto-js": "^3.1.8",（它是一个加密库）
2. npm install 下载crypto-js
3. 在api文件夹下的frame文件夹下面新建一个baseparams.js，，在这里面配置公共参数，里面引入crypto-js，
4. 在里面设置拦截器，获取盐参数，获取时间戳参数，最后设置当tokenid过期时，要跳转到login页
  let obj = {};
  let secretKey = "7PBE*O5M@tc3xy4PPfgoU@r04L4Gx7uR";
  obj = {
    accesskey:"@JZcc14L^PN6NjZ%PlSZsitH3xkDBoh8", //base编码
    appKey:"ycweb",//
    method:methodName ? methodName:"",//方法
    nonce:baseParam.nonce(),//生成的盐参数
    sign:"",//包括加密库
    timestamp:baseParam.timestamp(),//生成的时间戳参数
    tokenId:userHelper.getUserTokenId(),//tokenid
    version:"1.0"//版本号
  };
  let baseSignParam = obj.timestamp + obj.appKey + obj.accesskey + obj.method + obj.version + obj.nonce;//拼接字符串
  obj.sign = CryptoJS(encodeURIComponent(baseSignParam),encodeURIComponent(secretKey)).toString();
  //将baseSignParam里面的所有和secretKey进行加密，是加密函数，要tostring()转化成字符串
  return obj
```
+ 解释：encodeURIComponent() 
    - encodeURIComponent()是一个js函数，该函数可把字符串作为 URI 组件进行编码。
    - encodeURIComponent(URIstring)必传，是一个字符串，含有 URI 组件或其他要编码的文本
    - 该方法不会对 ASCII 字母和数字进行编码，也不会对这些 ASCII 标点符号进行编码： - _ . ! ~ * ' ( ) 。其他字符（比如 ：;/?:@&=+$,# 这些用于分隔 URI 组件的标点符号），都是由一个或多个十六进制的转义序列替换的
