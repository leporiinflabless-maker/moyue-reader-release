# 墨阅 v1.0.1

修复听书逐词高亮的三个实际问题，并重新校准高亮/选择框的行末坐标。

## 下载

- `moyue-reader-v1.0.1.apk`（66,842,064 B）
- SHA-256：`F7F0697ECD51E7FCEE8FB048A286B68CB928EEE37F08DFF483F91F3F1636CCB7`

要求 Android 8.0+（minSdk 26），versionCode 2，versionName 1.0.1。

## 修复内容

- **行末词高亮坐标**：`getPrimaryHorizontal(line.end)` 会返回下一行行首，导致行末词高亮横跨到左边距；现在行末使用当前行 `getLineRight()`，同时修复选择框和选择柄的同类坐标。
- **软连字符/零宽字符映射**：Edge `WordBoundary.Text` 不含 `U+00AD` 等朗读不可见字符；直接查找失败时先去掉这些字符并保留原文映射，避免高亮卡在整句或后续词错位。
- **跨页长句**：长句朗读到下一页时只向前翻页，不重新调用 `playCurrent()`，避免句子从头重读。
- **block 边界定位**：页首正好落在两个 block 分隔位时，`findIndexAt` 返回后一个 block 的首句，不再从上一句重新开始。

## 未修复/限制

- Edge 的 `WordBoundary.startMs` 未补偿系统音频输出延迟，高亮可能比实际发声略早几十毫秒。
- Edge 把数字/缩写读成另一种文本时，找不到原文会回退整句高亮，不影响播放。
- 逐词高亮依赖 Edge 返回 `WordBoundary`；无元数据时仍为整句高亮。
