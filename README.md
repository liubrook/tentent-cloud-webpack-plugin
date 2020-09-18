## tentent-cloud-webpack-plugin
webpack打包上传腾讯云

## 安装
```
npm i tencent-cloud-webpack-plugin
```

## 使用方法

支持的配置项:

+ `secretId` COS SecretId
+ `secretKey` COS SecretKey
+ `bucket` COS 存储对象名称，格式为对象名称加应用 ID，如：`bucket-1250000000`
+ `region` COS 存储地域，参见[官方文档](https://cloud.tencent.com/document/product/436/6224)
+ `path` 存储路径， 默认为 `[hash]`，也可以指定 hash 长度，如: `[hash:8]`
+ `exclude` 可选，排除特定文件，正则表达式，如: `/index\.html$/`
+ `include` 可选，指定要上传的文件，正则表达式，如: `/app\.js$/`
+ `batch` 可选，批量上传文件并发数，默认 20

***注: Webpack 的 `output.publicPath` 要指向 COS（或自定义的）域名地址***
```js
// 引入
const CosPlugin = require('cos-webpack')

// 这里用项目名加上时间戳用来在腾讯云中区分标识
const fileName = 'projectName/' + new Date().getTime()

// 配置 Plugin
const cosPlugin = new CosPlugin({
    secretId: defaultSettings.tencent.secretId,
    secretKey: defaultSettings.tencent.secretKey,
    bucket: defaultSettings.tencent.bucket,
    region: defaultSettings.tencent.region,
    path: fileName
});

// Webpack 的配置
module.exports = {
 output: {
    publicPath: IS_PROD ? defaultSettings.tencent.publicPath + fileName + '/dist' : '/',
    outputDir: 'dist',
    assetsDir: 'static',
 },
 plugins: [
   cosPlugin
   // ...
 ]
 // ...
}
```

## 示例
[示例项目](https://github.com/liubrook/tencent-cloud-webpack)