# LightAndroidUpgrade
安卓更新的一个简单组件

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

