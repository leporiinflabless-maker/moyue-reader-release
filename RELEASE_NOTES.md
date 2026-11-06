# 墨阅 v1.0.0

微信读书风格本地 EPUB/TXT 阅读器首个公开版本。

## 下载

- `moyue-reader-v1.0.apk`（75,986,198 B）
- SHA-256：`75855EAA1C2245748D2EEF02ED11142B35D55479D2C3C862ADB0E96A9B0C5994`

要求 Android 8.0+（minSdk 26）。

## 本版内容

- 本地 EPUB 2/3、TXT 阅读，无 DRM。
- libLineBreak-v2 UAX #14 断行 + 完整 DS typeset 节点模型 + 4-fitness 最优断行。
- 中文 ICU 词内禁则、行首/行尾标点禁则、英文 Liang/TeX 断词。
- 内置思源宋体 Medium、Noto Sans CJK SC、霞鹜文楷等宽 Medium；支持用户导入字体。
- 字宽/行高/基线/行盒 drawOffset 按微信 `CharElement`/`Paragraph` 整数公式校准。
- 选词、选择柄、划线/笔记、全书搜索、词典、字符书签、目录、阅读统计。
- 平移/覆盖/无动画/仿真卷曲、上下滑动、自动阅读、横屏双页。
- EdgeTts 听书、逐词高亮、睡眠定时、后台播放。

## 说明

- 不包含账号、书城、推荐、会员、DRM 或云端同步。
- 商业字体（方正、汉仪、仓耳等）不随 APK 分发；请使用自己已授权的文件导入。
- 本仓库只发布 APK 与说明，不包含微信读书 APK、商业字体或书籍内容。
