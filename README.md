# VideoCombo — 视频分割·充电岛

一个 APP，两套核心能力：**视频无损分割**（VideoSplitter 8.6 全量功能）+ **充电进度岛**（ChargeIsland 全量功能），统一玻璃拟态 UI、独立功能入口。

## 下载

- 前往 [Releases](../../releases) 下载最新 `VideoCombo-x.y.apk` 直接安装
- 包名 `com.tools.combo`，与「视频分割」「充电岛」单功能版并存安装，互不覆盖

## 功能

- **视频分割**：关键帧对齐无损切割、每段上限自适应重切、删除原视频、分割历史与连续播放、存储分析、命名模板、状态栏进度
- **充电岛**：实时电量/功率/温度/电压、充满与耗尽预估、电量曲线、前台监控通知（Live Update 提升）、插电与开机自启、未充电常驻
- **在线更新**：启动静默检查 + 关于页手动检查，下载、校验、一键安装，更新的是合并包、双功能不丢失

## 更新源

应用内检查更新读取本仓库 Release 上的 `version.json`：

```
https://github.com/Leoxijing/VideoCombo/releases/latest/download/version.json（GitHub 直连失败时自动回退 jsdelivr CDN：https://cdn.jsdelivr.net/gh/Leoxijing/VideoCombo@main/version.json）
```

字段：`versionCode`（整数，递增）、`versionName`、`url`（APK 下载地址）、`notes`（更新说明）。

## 版本规则

- 版本号 `vX.Y (versionCode N)`：小数位递增，达到 9.9 后进位为 1.0.0，依此类推
- versionCode 每次发版 +1
- 更新日志见 [CHANGELOG.md](CHANGELOG.md)，APP 内「更新日志」随包内置、离线可查

## 署名

第三方组件、参考机制与全版本核查记录见 [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md)；引入任何第三方代码/库时必须同步更新署名区。

## 声明

纯免费，仅供个人使用，不做任何商用。
