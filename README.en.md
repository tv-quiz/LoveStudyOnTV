# LoveStudyOnTV (娃爱答题)

**Learn first, then watch TV.** An Android TV app that asks your kids a quiz question before they can keep watching.

🌐 **Website: [http://106.54.222.166:8686/](http://106.54.222.166:8686/)**

[中文说明](README.md) · [Download APK](http://106.54.222.166:8686/download/tvquiz.apk) · [Releases](https://github.com/tv-quiz/LoveStudyOnTV/releases) · [Issues](https://github.com/tv-quiz/LoveStudyOnTV/issues)

> The app interface and question banks are in Chinese. The banks follow the Chinese primary school curriculum.

## What it does

- After the TV plays for a set time (for example 15 minutes), a full-screen question appears.
- The child answers with the remote control. A correct answer lets them keep watching. A wrong answer gives a new question, plus optional extra questions.
- Questions match the child's grade and term: mental arithmetic, math word problems, classical poems, Chinese characters, English words.
- Parents manage everything from a phone browser. No phone app: scan the QR code on the TV with the phone camera.
- Several children can watch together: each answers their own question, take turns, or use the youngest child's level.
- A 6-digit parent PIN protects pairing, turning the quiz off, and temporary passes.

## Quick start

1. Install the APK on the TV (USB stick, TV browser, or `adb`). Allow "Display over other apps". See [docs/install.md](docs/install.md) (Chinese).
2. Open the app on the TV. Scan the QR code with your phone (same Wi-Fi as the TV).
3. Enter the 6-digit pairing code shown on the TV. Set a 6-digit parent PIN. Add your children.

Install with adb:

```
adb connect <tv-ip>:5555
adb install -r tvquiz.apk
adb shell appops set com.gebilaozhongyi.tvquiz SYSTEM_ALERT_WINDOW allow
adb shell am start -n com.gebilaozhongyi.tvquiz/.MainActivity
```

Have an AI agent that can run commands? Give it [docs/ai-install.md](docs/ai-install.md).

## Free and advanced editions

| | Free | Advanced |
|---|:---:|:---:|
| Built-in arithmetic | ✓ | ✓ |
| Children | 1 | Several, can watch together |
| Math word problems | | ✓ |
| Question banks (poems, characters, English, …) | | ✓ |
| Records | Today | Full history |

To unlock the advanced edition, open **我的 → 激活码** (Me → Activation code) in the phone page and enter **`666888`**. This code is free for a limited time.

## Requirements

Android 9 or newer smart TV or TV box. LG webOS and Samsung Tizen TVs are not supported.

## License

Free for personal and family use. Binaries only; the source code is not included. See [LICENSE](LICENSE).

Keywords: Android TV, kids quiz, screen time, parental control, learn before watching TV, educational TV app, TV box.
