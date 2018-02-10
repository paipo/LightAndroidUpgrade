# LightAndroidUpgrade
安卓版本更新的一个简单组件

## 使用方法
android studio 引用 lightupgrade library 到项目 , 在 gradle 添加代码 , 例如
```java
compile project(path:':lightupgrade')
```
## 主要代码
```java
new UpgradeHelper.Builder(ActivitySet.this)
                        .setUpgradeUrl("http://xxxxxx?version=1")
                        .setDelay(1000)
                        .setIsAboutChecking(true)
                        .build().run(new UpgradeCheckCallback() {
                            @Override
                            public void Check(int c) {
                                if(UpgradeCheckCallback.C_EQUAL == c){
                                    //是同样版本
                                }
                            }
                });

```
UpgradeCheckCallback 为回调，不需要回调的时候
```java
new UpgradeHelper.Builder(ActivitySet.this)
                        .setUpgradeUrl("http://xxxxxx?version=1")
                        .setDelay(1000)
                        .setIsAboutChecking(true)
                        .build().run();

```
## 更新服务端的 json 格式
```javascript
{ 
	"status": "1", 
	"message": "", 
	"upgradeinfo": { 
		"appName": "", 
		"versionCode": "2",
		"versionName":"2.0", 
		"packageName": "com.xxxx",
		"apkUrl":"http://xxxxx/xxx.apk", 
		"upgradeNotes":"更新到 2.0", 
		"upgradeTitle":"", 
		"isForce":"0", 
		"fileSize":"2000", 
		"md5":"xxxxxxxxx" 
		} 
}
```
* status 1 时开始处理
* versionCode 版本，用来对比当前版本
* packageName 包名称
* apkUrl 下载地址
* upgradeNotes 显示在更新提示框的内容
* upgradeTitle 显示在更新提示框的标题，如没有使用默认标题
* isForce 0 ：可稍后更新，马上更新
* ![image](https://raw.githubusercontent.com/paipo/screenshots/master/lightup0.jpg)
* isForce 1 ：只有马上更新（不更新不能使用的情况）
* ![image](https://raw.githubusercontent.com/paipo/screenshots/master/lightup1.jpg)
* isForce 2 ：提示更新，不能做任何事情（特殊情况，如不兼容）
* ![image](https://raw.githubusercontent.com/paipo/screenshots/master/lightup2.jpg)
* md5 ：安装包的md5值，不一致时会提示 升级包错误，可在LightDialogActivity代码中查找 apkMD5= 查看的md5值，生成一个升级包计算一次再写入更新服务端
