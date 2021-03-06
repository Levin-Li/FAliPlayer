# FAliplayer

Flutter版的阿里云列表播放器，支持边播边缓存

[![pub package](https://img.shields.io/pub/v/faliplayer.svg)](https://pub.dev/packages/faliplayer) 
[![GitHub stars](https://img.shields.io/github/stars/Dovvvis/FAliPlayer)](https://github.com/Dovvvis/FAliPlayer/stargazers) 
![GitHub issues](https://img.shields.io/github/issues/Dovvvis/FAliPlayer) 
<!-- [![GitHub license](https://img.shields.io/github/license/Dovvvis/FAliPlayer)](https://github.com/Dovvvis/FAliPlayer/blob/master/LICENSE)  -->

# 示例效果
![gif图加载慢请耐心等待](https://github.com/Dovvvis/FAliPlayer/blob/master/gif/s.gif)

[点击此处看视频效果](http://video.iqingbai.com/RPReplay_Final1584613529.MP4)

### 引入
```
import 'package:faliplayer/faliplayer.dart';
```
### 示例
```
class MyApp extends StatefulWidget {
  @override
  _MyAppState createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> {
  FAliListPlayerController controller;
  List<String> urls = [
        ...
  ];

  @override
  void initState() {
    super.initState();
    ///初始化
    controller = FAliListPlayerController(isAutoPlay: true, loop: true);
    ///添加视频源
    controller.addUrls(urls);
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: const Text('Plugin example app'),
        ),
        body: FAliPlayerView.builder(
          controller: controller,
          ///视频列表每页的UI
          pageBuilder: (c, i) {
            return ...;
          },
          ///每个视频的缩略图
          thumbImageBuilder: (c, i, h, w) {
            return ...;
          },
        ),
      ),
    );
  }
}

```
### 控制播放
```
//开始
controller.start();
//暂停
controller.pause();
//移动到某个视频并播放
controller.moveTo(0);
//下一个
controller.moveToNext();
//上一个
controller.moveToPre();
//跳转
controller.seekTo(positon);
```
### 监听

```
//播放位置更新监听
controller.setPositionUpdateListener((position) {

});

//缓存位置更新监听
controller.setBufferedPositionUpdateListener((position) {

});

//视频大小变化监听
controller.setOnVideoSizeChanged((){

});

//视频播放事件变化监听
controller.setOnPlayEventListener((type){
      
});
```
### 设置缓存配置
请在初始化的视频设置，正常在initState处设置

```
controller.setCacheConfig(
          AVPCacheConfig(path: d.path, maxDuration: 100, maxSizeMB: 1024));
```
### 获取缓存文件的路径

```
///获取缓存文件的路径
///[url]文件的url
Future<void> getCachePath(String url)
```
### 设置视频显示模式
```
Future<void> setScalingMode(AVPScalingMode mode)
```

属性 | 说明
------- | -------
SCALETOFILL            |      拉伸（会变形）
SCALEASPECTFIT         |      按照原比例显示
SCALEASPECTFILL        |      按照原比例显示并充满屏幕



