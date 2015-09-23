#取出安裝於Android的APK
####1.列出裝置所有的APP Package Name
```adb shell pm list packages```
####2.確認該app的路徑
```adb shell pm path com.example.someapp```
####3.取出APK
```adb pull /data/app/com.example.someapp.apk```