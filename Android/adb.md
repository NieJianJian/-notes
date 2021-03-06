## adb常用命令

* 查看屏幕尺寸

  * 方法一：

    ```
    adb shell dumpsys window displays
    ```

  * 方法二：

    ```
    adb shell 
    wm size
    wm density
    ```

* 查看Activity相关信息

  ```
  adb shell dumpsys activity
  ```

  * 查看任务栈信息

    ```
    adb shell dumpsys activity recents
    ```

  * 查看任务栈中的Activity详细信息

    ```
    adb shell dumpsys activity activities
    ```

* 截图

  ```
  adb shell screencap -p /sdcard/001.png
  ```

* 录屏

  ```
  adb shell screenrecord /sdcard/demo.mp4
  ```

  加录制时间设置为10s的方式：

  ```
  adb shell screenrecord  --time-limit 10 /sdcard/demo.mp4
  ```

* 默认按键时间KeyCode，如返回键：

  ```
  adb shell input keyevent 4
  ```

* 模拟点击屏幕坐标位置

  ```
  adb shell input tap 100 100
  ```

* 模拟输入字符

  ```
  adb shell input text abc
  ```

* 模拟屏幕上划屏操作

  前四个数是坐标点，第五个数是滑动时间（单位毫秒）

  ```
  adb shell input swipe 50 250 250 250 500 
  ```

* 查看系统安装应用的包名列表

  ```java
  adb shell
  pm list packages
  ```

* 查看某应用的apk安装地址

  ```
  adb shell pm path [包名]
  ```

* 查看Activity的启动时间

  ```
  adb shell am start -S -W 包名/启动类的全限定名
  ```

  `-s`表示重启。结果如下：

  ```
  mbp:~ nj$ adb shell am start -S -W com.nj.testappli/com.nj.testappli.MainActivity
  Stopping: com.nj.testappli
  Starting: Intent { act=android.intent.action.MAIN cat=[android.intent.category.LAUNCHER] cmp=com.nj.testappli/.MainActivity }
  Status: ok
  Activity: com.nj.testappli/.MainActivity
  ThisTime: 556
  TotalTime: 556
  WaitTime: 615
  Complete
  ```

  `ThisTime`代表最后一个Activity的启动耗时；

  `TotalTime`代表一连串的Activity的启动耗时（有几个Activity就统计几个）；

  `ThisTime`和`TotalTime`一般情况下是相等的。只有在MainActivity的onCreate方法中，启动另外一个Activity，并且调用finish方法时，这两个值才会不相等。

  `WaitTime`是`TotalTime`加上应用进程创建过程的耗时。

* 查看当前运行的app

  ```
  adb shell dumpsys window windows | grep mFocusedApp
  ```

  





***

### 参考文献

1. [ ADB 用法大全](https://github.com/mzlogin/awesome-adb)