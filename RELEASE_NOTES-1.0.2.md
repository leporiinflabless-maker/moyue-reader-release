# 墨阅 v1.0.2

优化大型 EPUB 的打开解析速度，50 MB / 695 章的《明朝那些事儿（增补版）》解析时间从约 8.4 秒降到约 1.3–1.5 秒。

## 下载

- `moyue-reader-v1.0.2.apk`（66,564,558 B）
- SHA-256：`7112B716B236CB06B62DB6B517C6D168005D69BF25778C43DE27CE08D57DB0FD`

要求 Android 8.0+（minSdk 26），versionCode 3，versionName 1.0.2。

## 优化内容

- **章节并行解析**：按 spine 顺序把 XHTML 章节提交到最多 6 个 worker，结果按原顺序合并；每个 worker 使用独立 `ZipFile`，避免 Android 的 ZipFile 读锁把解压串行化。8 核实测 6 worker 最快，8 worker 反而略慢。
- **图片延迟解码**：打开书籍时不再解压全部图片、写入 `cache/images`；只用 `inJustDecodeBounds` 从 zip 流读取宽高，正文块记录 `imageArchive/imageEntry`，第一次绘制时由 `ImageStore` 读取并缓存 Bitmap，退出阅读器时关闭 zip。
- **实体替换单次化**：XHTML 的 30 个命名实体由 30 次全串 `replace` 改为一次 `Regex.replace`。
- **资源关闭**：解析完成后统一关闭解析用的 ZipFile，避免反复打开大书累积文件描述符。

## 实测（Redmi M2012K10C，Android 12，52,068,294 B EPUB，695 章 / 644 图 / 5043 页）

| 阶段 | header | 解析 total |
|---|---:|---:|
| 优化前 | 155 ms | 8423 ms |
| 图片懒解码 | 154 ms | 7345 ms |
| 并行解析 + 实体优化 | 125–179 ms | **1319–1471 ms** |

- 全书分页仍在首屏出现后后台完成：5043 页约 8.5 秒；首章 7 页 109 ms 即可阅读。
- 页面缓存命中约 140–150 ms，页数与优化前完全一致。
- 回归：第 17 页插图正常显示；重启后恢复到同一本书；36 章普通 EPUB 解析 266 ms、278 页正常。

## 未改变

- 账号、书城、推荐、会员、DRM、云同步仍不包含。
- 商业字体仍不随 APK 分发，只支持用户自行导入已授权字体。
