# 开源许可与第三方署名

本页列出「视频分割·充电岛」合并版 APP 使用或分发的第三方组件，包含来源链接、原作者署名、许可类型与用途；充电岛侧的参考机制与历史资源说明见第三节。

## 一、随 APP 分发的第三方组件

### FFmpeg
- 来源：https://ffmpeg.org/
- 原作者：FFmpeg Team
- 许可：上游 LGPL-2.1-or-later；经 ffmpeg-kit 以 --enable-version3 构建，随包以 LGPL-3.0 分发
- 用途：无损切割（-c copy 流复制）与转封装
- 版本：随 ffmpeg-kit-min 6.0.4 打包（FFmpeg 6.0 系列）

### ffmpeg-kit（dev.ffmpegkit-maintained:ffmpeg-kit-min:6.0.4）
- 来源：https://github.com/ffmpegkit-maintained/ffmpeg （上游 https://github.com/arthenica/ffmpeg-kit ，2025 年归档）
- 出处：Maven Central 上的社区维护接续构建，保持 com.arthenica.ffmpegkit API 不变；本版用于让原生库满足 16 KB 页对齐要求
- 原作者：上游 Tanersener（Arthenica）；维护分支维护者 Jokobee
- 许可：LGPL-3.0
- 用途：FFmpeg 的 Android / JNI 封装与命令执行

### libc++_shared.so
- 来源：https://github.com/llvm/llvm-project （随 Android NDK 分发）
- 原作者：LLVM Project / The Android Open Source Project
- 许可：Apache-2.0 WITH LLVM-exception
- 用途：C++ 标准运行库，ffmpeg-kit 原生库的运行依赖

### smart-exception（com.arthenica:smart-exception-java / -common:0.2.1）
- 来源：https://github.com/tanersener/smart-exception
- 原作者：Tanersener
- 许可：BSD-3-Clause
- 用途：ffmpeg-kit 的传递依赖（内部异常封装）

### AndroidX / Jetpack
- 组件：androidx.core:core-ktx:1.13.1 及其传递依赖（core、annotation、collection、concurrent、interpolator、lifecycle、arch.core、profileinstaller、startup、tracing、versionedparcelable 等）
- 来源：https://developer.android.com/jetpack/androidx
- 原作者：The Android Open Source Project / Google LLC
- 许可：Apache-2.0
- 用途：FileProvider（APK 安装授权）等基础组件

### Kotlin 标准库
- 组件：kotlin-stdlib、kotlin-stdlib-common 1.9.24，org.jetbrains:annotations 13.0
- 来源：https://kotlinlang.org/
- 原作者：JetBrains s.r.o.
- 许可：Apache-2.0
- 用途：Kotlin 运行时

### Guava listenablefuture（com.google.guava:listenablefuture:1.0）
- 来源：https://github.com/google/guava
- 原作者：Google LLC
- 许可：Apache-2.0
- 用途：AndroidX 的传递依赖

### Material Icons
- 来源：https://fonts.google.com/icons
- 原作者：Google LLC
- 许可：Apache-2.0
- 用途：7 个界面矢量图标的路径数据，文件与用途对应如下
  - ic_arrow_back.xml —— 返回箭头（实心）
  - ic_pause.xml —— 暂停（按同一造型等价重绘，非逐字复制）
  - ic_play_arrow.xml —— 播放三角
  - ic_skip_next.xml —— 下一段
  - ic_fullscreen.xml —— 进入全屏
  - ic_fullscreen_exit.xml —— 退出全屏
  - ic_video_placeholder.xml —— 缩略图缺失占位（播放三角）
- 说明：上述每个文件头均标注了来源、出处、原作者与许可；其余矢量图标（ic_back、ic_changelog、ic_clean、ic_history、ic_limit、ic_logs、ic_theme、ic_update、ic_rename、ic_storage、ic_launcher_background、ic_launcher_foreground、ic_launcher_monochrome）为项目自绘，使用圆弧/贝塞尔曲线与自有坐标，不含第三方路径

## 二、LGPL-3.0 合规说明

- 本项目未修改 FFmpeg、ffmpeg-kit、smart-exception 的任何源码或二进制，仅通过公开 API 调用
- FFmpeg 以动态库（.so）形式打包，Java/Kotlin 层通过 ffmpeg-kit 的公开 JNI 接口调用；用户可自行替换为重新构建的库，本项目不设置阻止替换的技术措施
- 源码获取：ffmpeg-kit 上游 https://github.com/arthenica/ffmpeg-kit ；本版维护分支 https://github.com/ffmpegkit-maintained/ffmpeg ；FFmpeg https://ffmpeg.org/download.html ；libc++ https://github.com/llvm/llvm-project
- AAR 坐标：dev.ffmpegkit-maintained:ffmpeg-kit-min:6.0.4（Maven Central）；v6.5 及更早为 com.arthenica:ffmpeg-kit-min:6.0-2
- 许可全文：LGPL-3.0 https://www.gnu.org/licenses/lgpl-3.0.html ；LGPL-2.1 https://www.gnu.org/licenses/old-licenses/lgpl-2.1.html ；Apache-2.0 https://www.apache.org/licenses/LICENSE-2.0
- 使用的是 min 变体（不含 -gpl），未启用 --enable-gpl，不包含 GPL 授权的 FFmpeg 组件
- 16 KB 对齐：v6.6 起全部 arm64 原生库的 ELF LOAD 段按 16 KB 对齐（p_align=0x4000），APK 内未压缩 .so 的 ZIP 偏移也对齐到 16 KB 边界，满足 Android 15+ 的 16 KB 页大小要求

## 三、原创内容

- 业务代码（app/src/main/java/com/tools/videosplit/ 下 21 个 Kotlin 文件）、自绘资源（启动图标、渐变与玻璃质感背景、进度条、12 个自绘矢量图标）均为本项目原创，不含第三方素材
- 充电岛（ChargeIsland）业务代码（app/src/main/java/com/chargeisland/app/ 下 9 个 Java 文件与 ChargeActivity.kt）为本项目原创；**第三方代码/库：无**——JSON 解析（org.json）与网络请求（HttpURLConnection）均为 Android 系统自带组件
- 充电岛自绘资源：62 个电池温度图标（ic_temp_0–61 与 ic_temp_unknown）、pill_badge、bg_dialog、ic_stat_transparent、ic_charge 等，均为项目原创
- 充电岛参考机制署名（仅参考机制/API 用法，未复制其代码）：
  - 小米超级岛开发指南 — https://dev.mi.com/xiaomihyperos/documentation/detail?pId=2131 （充电岛 v1.3 前的超级岛参数接入；v1.3 起已移除厂商私有参数）
  - Android 实时动态（Live Updates）通知 — https://developer.android.com/develop/ui/views/notifications/live-update
  - VideoSplitter（作者同账号项目）应用内更新机制、通知形态、更新日志页结构的机制参考（充电岛 v1.4–v1.6；两项目现已合并为本 APP）
  - androidx NotificationCompat.EXTRA_REQUEST_PROMOTED_ONGOING — 提升请求 extras key 字面值 `android.requestPromotedOngoing` 的协议来源（充电岛 v1.4 起）
- 历史资源说明：充电岛 v1.0–v2.1 的通知/启动图标曾使用 Material Design `flash_on` 闪电路径（Apache-2.0 设计资源）；v2.2 起已全部替换为项目自绘图标，当前代码无该路径残留
- 图标设计稿由项目自带的 design_icons.py 生成预览，该脚本仅用于开发期出图，不随 APK 分发
- 未内置第三方字体文件，界面文字使用系统字体
- 名称与图标未使用任何第三方商标

## 四、项目自身许可

- 业务代码与资源在 AI 辅助下生成，经维护者审阅
- 当前仓库未附带 LICENSE 文件，README 声明为「纯免费，仅供个人使用，不做任何商用」；该表述是使用声明，不是标准开源许可证
- 如需复用、修改或再分发本项目代码，请先与维护者确认许可方式

## 五、其他说明

- Android SDK、Gradle、Kotlin 编译器、Android Gradle Plugin 等仅用于构建，不随 APK 分发
  - Gradle：https://gradle.org/ ，Gradle Inc.，Apache-2.0
  - Kotlin 编译器 / kotlin-gradle-plugin：https://kotlinlang.org/ ，JetBrains s.r.o.，Apache-2.0
  - Android Gradle Plugin / Android SDK Build-Tools：https://developer.android.com/studio ，The Android Open Source Project / Google LLC，Apache-2.0（SDK 使用另受 Android SDK 条款约束）
  - Pillow（仅 design_icons.py 图标预览使用）：https://python-pillow.org/ ，Jeffrey A. Clark 等，MIT-CMU（HPND）
- Apache-2.0 组件的版权与许可声明以本页及 README 的署名区块为准
- 本页内容与仓库 THIRD_PARTY_NOTICES.md 保持一致

## 六、代码原创性核查记录

### 2026-11-22 全量核查

- 核查范围：`app/src/main/java` 全部 18 个 Kotlin 文件、`app/src/main/res` 下 17 个矢量图标与 8 个形状/渐变资源、`AndroidManifest.xml`、`app/build.gradle.kts`、`design_icons.py`
- 核查方法：
  1. 逐文件检索版权头、许可证标识、外部链接、`TODO/StackOverflow` 等复制痕迹
  2. 逐个比对矢量图标 `pathData` 与 Material Icons 路径：7 个命中并已署名，10 个为自绘（圆弧/贝塞尔 + 自有坐标系）
  3. 对照 `releaseRuntimeClasspath` 依赖树核对随包组件，确认与第一节清单一致，无未声明的第三方库
  4. 通读共享工具与自定义控件（Ui、Theme、Dialogs、PlayerActivity 手势与适配、MediaFiles、StatusBarProgress），确认无整段复制或改写自外部项目
- 结论：未发现复制或改编的第三方业务代码；非原创内容仅为**未修改的二进制依赖**与**7 个图标路径数据**，均已在本页与仓库 THIRD_PARTY_NOTICES.md 署名
- 无第三方字体、图片、音频素材随包分发

### 2026-11-25 增量复核（v7.7–v8.1 改动）

- 复核范围：新增 Nav.kt、ClipRename.kt、SplitRecords.kt（Kotlin 文件 18 → 21，约 8100 行）与自绘图标 ic_rename、ic_storage（矢量图标 17 → 19），以及主页改版、统一返回导航等 15 个文件的重构
- 复核方法：检索版权头、许可标识、外部链接与复制痕迹；核对依赖声明无新增（仍为 ffmpeg-kit-min 6.0.4 + core-ktx）；检查新增图标文件头的原创声明
- 结论：未发现复制或改编的第三方业务代码；新增图标均为项目自绘；ChangelogActivity 新增的在线更新日志拉取地址仅为网络请求目标，不分发第三方代码，无需署名

### 2026-11-27 合并版全版本核查（v1.0–v1.3）

- 核查范围：以 VideoSplitter 8.6（versionCode 78）源码为底座的合并工程——Kotlin 21 个 + 充电岛 Java 9 个、矢量图标 20 个、充电岛资源 65 个（62 个温度图标等）、内置日志（changelog.md / charge_changelog.md）与本署名文件；覆盖「视频分割」v1.0–v8.6 与「充电岛」v1.0–v4.1 的全部版本历史
- 核查方法：
  1. 逐文件检索版权头、许可证标识、外部链接与复制痕迹
  2. 对照依赖树确认合并后随包组件与第一节一致，无新增第三方库（充电岛侧零第三方依赖）
  3. 逐项核对充电岛参考机制（超级岛指南、Live Updates、更新与通知机制参考、promoted extras 协议字面值）与历史资源（flash_on）均已署名
  4. 核对内置双日志与本页版本记录一致
- 结论：未发现未署名的第三方代码/库/素材/参考机制；合并未引入新的第三方分发组件
