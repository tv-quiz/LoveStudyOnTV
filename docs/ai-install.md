# AI 安装指南

[← 返回首页](../README.md)

如果你的电脑上有能执行命令的 AI 助手（例如 Claude Code、Cursor 等），把下面整段复制给它，再说一句「照这个装到我的电视上」。你只要在电视上按一次「允许」。

```text
【娃爱答题安装任务 · 交给 AI 的说明】

任务：把「娃爱答题」安装到用户的安卓电视或电视盒子上，授权，启动，确认装好。
工具和方法由你决定。下面是你需要知道的事实、要求和常见问题。

== 这是什么 ==

「娃爱答题」是安卓电视应用。电视播放一段时间后弹出题目，孩子答对才能接着看。
装好后，电视首页显示一个二维码和 6 位配对码。家长用手机相机扫码，在手机浏览器里配对和管理。
扫码配对由用户自己做。你只需要在最后提醒用户。

== 你需要的事实 ==

- 安装包（最新版）：http://106.54.222.166:8686/download/tvquiz.apk
- 版本信息：http://106.54.222.166:8686/download/tvquiz.json
  字段：versionCode、versionName、url、size、sha256、notes
- 包名：com.gebilaozhongyi.tvquiz
- 主界面：com.gebilaozhongyi.tvquiz/.MainActivity
- 系统要求：Android 9（API 28）及以上。
- 只用上面的地址下载。不要用第三方 APK 网站。

== 建议步骤 ==

1. 下载 tvquiz.json 和 tvquiz.apk。用 sha256 校验安装包，不一致就停下并告诉用户。
2. 请用户在电视的开发者选项里打开「网络调试」（ADB over network），并告诉你电视的 IP 地址。
   如果你能扫描局域网，也可以自己找 5555 端口开着的设备，但要请用户确认是哪台电视。
3. 连接电视：
   adb connect <电视IP>:5555
4. 安装：
   adb -s <电视IP>:5555 install -r tvquiz.apk
5. 授予悬浮窗权限（应用靠它在其他应用上层弹出题目）：
   adb -s <电视IP>:5555 shell appops set com.gebilaozhongyi.tvquiz SYSTEM_ALERT_WINDOW allow
6. 启动应用：
   adb -s <电视IP>:5555 shell am start -n com.gebilaozhongyi.tvquiz/.MainActivity
7. 验证（见「成功标准」）。

== 常见问题 ==

1. 第一次 adb 连接时，电视弹出「允许 USB 调试吗？」。你不能代替用户操作。
   到这一步就停下，请用户用遥控器勾选「一律允许」并点「允许」，然后重新连接。
   adb devices 显示 unauthorized：请用户看电视上的弹框。没有弹框，就请用户关掉再打开网络调试，
   你执行 adb kill-server 后重新 adb connect。显示 offline 或连接被拒绝：网络调试没开、IP 不对，或不在同一网络。
   安卓 11 及以上的电视也可以用「无线调试」：请用户在电视上选「使用配对码配对设备」，告诉你 IP、配对端口和 6 位码，
   你执行 adb pair <IP>:<配对端口>，再 adb connect <IP>:<连接端口>（连接端口在「无线调试」页面上，和配对端口不同）。
   用户找不到开发者选项时，请他看 http://106.54.222.166:8686/help.html#brands 里的品牌表。
2. 小米 / Redmi 电视：开发者选项里还要打开「USB 安装」，否则 install 会失败。
3. 有的品牌不让通过 U 盘或浏览器安装外来应用，adb 是这类电视的主要方法。
   如果 adb 安装也被系统拒绝，把命令和报错原文告诉用户，不要反复尝试。
4. 如果电视上有签名不同的旧版本，install -r 会失败（INSTALL_FAILED_UPDATE_INCOMPATIBLE）。
   这时要先卸载旧版本，卸载会清除设置。先征得用户同意再卸载。
5. LG（webOS）、三星（Tizen）等不是安卓系统，不能安装。直接告诉用户。

== 成功标准 ==

- adb shell dumpsys package com.gebilaozhongyi.tvquiz 里的 versionName 和 tvquiz.json 里的一致。
- adb shell appops get com.gebilaozhongyi.tvquiz SYSTEM_ALERT_WINDOW 显示 allow。
- 应用已启动：电视屏幕显示娃爱答题首页、二维码和配对码。可以截图给用户看：
  adb -s <电视IP>:5555 exec-out screencap -p > tv.png

== 边界 ==

- 不刷机，不 root，不改动电视上的其他应用和系统设置。
- 装不上时，把命令和报错原文如实告诉用户。不要反复换方法硬试。
- 完成后告诉用户：
  1) 手机连上和电视相同的 Wi-Fi，用相机扫电视首页的二维码；
  2) 输入电视上的 6 位配对码，设置 6 位家长密码；
  3) 要用内测版，先到家长群领取免费的内测激活码（打开 http://106.54.222.166:8686/#group ，点右下角「加群反馈」），再在管理页面「我的 → 激活码」输入；
  4) 更多帮助：http://106.54.222.166:8686/help.html
  5) 建议在电视开发者选项里关掉「网络调试」，以后升级时再打开。
```
