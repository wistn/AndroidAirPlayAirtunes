# AndroidAirPlayAirtunes
在Android设备上实现Airplay的Airtunes音乐播放功能


## 2017-6-30
- 实现了第一部分功能，**让iOS设备通过AirTunes发现Android设备**
- 相关功能分析: [链接](http://www.jianshu.com/p/e0f786c32952)

## 2017-7-3
实现了第二部分功能, **iOS设备通过AirTunes连接上Android设备**
相关功能分析: [链接](http://www.jianshu.com/p/63b99afb13fc)

## 2017-7-4
实现了所有功能,**在Android设备上实现Airplay的Airtunes音乐播放功能**
相关功能分析: [链接](http://www.jianshu.com/p/55b19f32085f)

![效果图1](https://github.com/RDduwan/markdownpic/blob/master/playmusic1.jpeg?raw=true)
![效果图2](https://github.com/RDduwan/markdownpic/blob/master/playmusic2.jpeg?raw=true)

———— 以上是原作者的项目说明 ————
fork使用者（我）2021年打包笔记：
感谢原作者 RDduwan！原项目效果(在Android设备上实现Airplay的Airtunes音乐播放功能)：屏幕镜像方式找不到安卓设备，要在控制栏扬声器与电视里连接，发射端和接收端各自有音量栏调节（是叠加效果），实现安卓设备成为airplay音箱等。推送本地文件音频、网络音频正常，推送tts音频有声音但不同步；发射端推送视频时会推送音频不会推送画面（发射端视频如果是本地文件视频、浏览器如safari网页视频、app在线视频如爱奇艺、腾讯视频有同步声音，如果是app在线视频AcFun等有声音但不同步，如果是app在线视频哔哩哔哩接收端没有声音。如果播放后半小时没声音，就亮一下安卓设备屏幕。

mac版android studio 4.2.1 构建调试版 Build-make project->Build-build APK->Run-run
build阶段 1 如果报错 Could not determine java version from xxx (The project uses Gradle version which is incompatible with Studio running on Java 10 or newer)，调用的java要改低版本比如oracle jdk8，android studio界面右上角放大镜按钮搜索choose runtime（设置里提前安装该插件）选择jdk8(并且 project structure 里面 Sdk location-jdk location 设置), 如果是命令行 ./gradlew 调用就临时export JAVA_HOME=jdk8对应路径

2 如果报错 SDK location not found ， AndroidAirPlayAirtunes/app/build.gradle 找到 targetSdkVersion ，在 ANDROID_HOME 里确保有该版本, android studio 可在 Preferences-Appearance & Behavior-System Settings-Android SDK 添加（命令行方法还要设置环境变量 ANDROID_HOME ）

3 如果报错 Could not find com.android.support.constraint:constraint-layout:1.0.0-alpha7 , 涉及Android Studio 约束布局功能，如果android studio3.5以上的版本，AndroidAirPlayAirtunes/app/build.gradle 的 compile 'com.android.support.constraint:constraint-layout:数字' 数字改为1.1.3，然后Android Studio 同步

4 如果android studio提示加上 maven Google ，就点击按钮，自动在AndroidAirPlayAirtunes/build.gradle 2处
    repositories { 加上
        maven {
            url 'https://maven.google.com/'
            name 'Google'
        }
    }

重新命令行打包调试版apk ./gradlew assembleDebug #已包含 打包工程 ./gradlew build -x test
安装到真机 adb install -r ./app/build/outputs/apk/app-debug.apk

根据fork的人（我）需求，在不同安卓设备要显示不同的Airplay/Airtunes接收端名字，所以修改 AndroidAirPlayAirtunes/app/src/main/java/ss/serven/rduwan/airtunesandroid/AirTunesRunnable.java