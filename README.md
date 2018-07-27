# ReaderApp
cordova打包vue项目实践

> 打包过程很简单，不过在配android环境的时候跌了很多坑，所以最重要的就是配好环境了。需要的环境有：java jdk，android jdk，gradle。

### 创建cordova项目
``` cordova create 文件名 org.apache.cordova.包名 项目名 ```
### 添加android
``` cordova platform add android ```
### 修改vue项目
#### 安装vue-cordova
``` npm install vue-cordova --save ```

在main.js里面添加

```
import VueCorvova from 'vue-cordova'
Vue.use(VueCorvova)
```
#### 修改index.html
 在index.html引入cordova.js
 
``` <script type="text/javascript" src="cordova.js"></script> ```

在\<head\>中添加：

``` 
<meta http-equiv="Content-Security-Policy" content="default-src 'self' data: gap: https://ssl.gstatic.com 'unsafe-eval'; style-src 'self' 'unsafe-inline'; media-src *; img-src 'self' data: content:;">
<meta name="format-detection" content="telephone=no">
<meta name="msapplication-tap-highlight" content="no">
<meta name="viewport" content="user-scalable=no, initial-scale=1, maximum-scale=1, minimum-scale=1, width=device-width">
```
#### 将cordova项目中的/www/js/index.js复制到vue项目的main.js
### 打包vue项目
``` npm run build ```

如果没有修vue/config/index.js的打包路径，会在vue项目中生成一个dist文件夹，把dist中的内容copy替换cordova项目中的/www的全部内容。

可以打开/www/index.html查看是否显示正常。
#### PS

这里面有好几个坑，主要是vue打包出来的路径问题，会造成显示空白页的情况。

解决办法：
修改vue/config/index.js文件的build里面的 
``` assetsPublicPath: '/', ``` 
成 
``` assetsPublicPath: './', ```
### 生成apk
```cordova build android ```

在此之前可以查看android需要的环境是否都配好了：
```cordova requirements android ```


### 参考文档：
[通过cordova将vue项目打包为webapp](https://www.cnblogs.com/pengjunhao/p/6803606.html)

[vue-cli项目打包出现空白页和路径错误问题](https://blog.csdn.net/qq_32340877/article/details/79105032)
