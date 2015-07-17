
Valgrind.org

需要在 Linux 下编译，OS X 下可能编译不过

基本介绍

http://maintainablecode.logdown.com/posts/245425-valgrind-is-not-a-leak-checker
http://www.ibm.com/developerworks/cn/linux/l-cn-valgrind/


Android 版本的编译
http://valgrind.org/docs/manual/dist.readme-android.html

http://blog.frals.se/2014/07/02/building-and-running-valgrind-on-android/
https://gist.github.com/frals/7775c413a52763d80de3

http://stackoverflow.com/questions/13531496/cant-run-a-java-android-program-with-valgrind/19235439#19235439

编译好的版本下载地址
http://guoh.org/box/valgrind-3.10.1-android.tar.gz

运行会比较花时间




其他工具

https://code.google.com/p/address-sanitizer/wiki/Android
http://debuggingisfun.blogspot.hk/2014/12/android-address-sanitizer-for-native.html

目前在 Android 4.4 上试验出错

```Callstack
07-17 07:38:33.920   264   264 I DEBUG   : backtrace:
07-17 07:38:33.920   264   264 I DEBUG   :     #00  pc 00000000  <unknown>
07-17 07:38:33.920   264   264 I DEBUG   :     #01  pc 00088a20  /system/lib/libclang_rt.asan-arm-android.so (__sanitizer::MaybeInstallSigaction(int, void (*)(int, void*, void*))+108)
07-17 07:38:33.920   264   264 I DEBUG   :     #02  pc 00088998  /system/lib/libclang_rt.asan-arm-android.so (__sanitizer::InstallDeadlySignalHandlers(void (*)(int, void*, void*))+44)
07-17 07:38:33.920   264   264 I DEBUG   :     #03  pc 00073530  /system/lib/libclang_rt.asan-arm-android.so (__asan::AsanInitInternal()+1472)
07-17 07:38:33.920   264   264 I DEBUG   :     #04  pc 0000274d  /system/bin/linker

```Callstack
