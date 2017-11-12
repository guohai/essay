Android 8.0 当中允许 Activiy 以画中画模式展现。这是一种多窗口模式的改进加强，在视频类应用中用处非常大，有了这种模式，就可以在视频通话或者观看直播的过程当中打开另外的应用而不用退出当前视频。更详细的就再累述了，大家去阅读 [官方文档](https://developer.android.com/guide/topics/ui/picture-in-picture.html) 就行

这里以 Agora RTC SDK 为例来给大家展示下该特性，实际上不用 Agora RTC SDK 做任何修改。

### 准备环境

+ Android 8.0 或以上版本手机

+ [Agora RTC SDK 1.14.0](http://download.agora.io/sdk/release/Agora_Native_SDK_for_Android_v1_14_0_FULL.zip) 或 [以上](https://www.agora.io/cn/download/) 版本

+ Android Studio 3.0 或以上版本(非必需)

### 如何实现画中画模式
默认应用是不支持画中画模式的，需要给视频所在的 Activity 做些配置，如下在 `AndroidManifest.xml` 加上属性 resizeableActivity/supportsPictureInPicture 并均设置为 true
<pre>
android:resizeableActivity="true"
android:supportsPictureInPicture="true"
android:configChanges=
    "screenSize|smallestScreenSize|screenLayout|orientation"
</pre>

为了进入画中画模式，Activty 必需要用 `enterPictureInPictureMode(PictureInPictureParams params)` 方法，非常的简单，但是为了告诉系统进入画中画模式之后，Activity 界面在整个屏幕当中的布局，我们需要设置一些参数。我们这里简单设置下，具体在使用的时候需要根据屏幕的分辨率动态取设置，更多信息参考 [官方文档](https://developer.android.com/reference/android/app/PictureInPictureParams.Builder.html)。
<pre>
PictureInPictureParams params = new PictureInPictureParams.Builder()
        .setAspectRatio(new Rational(10, 16))
        .build();
</pre>

当然需要在程序当中控制 Acticity 界面当中的内容，比如我们可以隐藏自己本地的预览画面，隐藏不需要的按钮信息等等，这个实现也非常简单。
<pre>
@Override
public void onPictureInPictureModeChanged(boolean isInPictureInPictureMode, Configuration newConfig) {
    super.onPictureInPictureModeChanged(isInPictureInPictureMode, newConfig);
    FrameLayout container = findViewById(R.id.local_video_view_container);
    SurfaceView surfaceView = (SurfaceView) container.getChildAt(0);
    surfaceView.setZOrderMediaOverlay(!isInPictureInPictureMode);
    surfaceView.setVisibility(isInPictureInPictureMode ? View.GONE : View.VISIBLE);
    container.setVisibility(isInPictureInPictureMode ? View.GONE : View.VISIBLE);
}
</pre>

另外值得一说的是，进入画中画模式，系统会触发生命周期的方法 `onPause/onResume` 方法，我们需要根据需要适当的做些操作，比如是画中画模式的话，就不做任何操作，音视频流继续，否则的话，就关闭视频流，反正在后台也看不见视频。

### 运行截图
![PiP with Agora RTC SDK](https://github.com/AgoraIO/Agora-Picture-in-Picture-Android/blob/master/screenshots/pip-sample-agora.gif)

### 开始行动吧
还等什么，了解了这些之后，快给自己的应用加上这个功能吧。我们也提供了 [示例代码](https://github.com/AgoraIO/Agora-Picture-in-Picture-Android) 供参考。
