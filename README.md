# KimiCode（Android）

> 桌面上的代码，装进口袋。

KimiCode 是一个 Android 随身客户端，连接 **Kimi Code Desktop 的官方远程控制服务**。电脑上开启远程控制后，手机扫码配对一次，之后点桌面图标就能直接进入自己的 Kimi Code 工作区——查看会话、继续对话、审批工具调用，不用再开浏览器。

安装包约 5.8 MB，最低支持 Android 8.0（API 26）。

## 下载

从 [Releases](../../releases) 页面下载最新 `app-release.apk`，侧载安装（需允许「安装未知应用」）。

## 三分钟上手

1. 电脑打开 **Kimi Code Desktop 1.1.0+**：设置 → 远程控制 → 开启，保持电脑运行并联网
2. 手机打开 App，**扫码** / **相册识别二维码** / **粘贴配对链接**，确认域名后保存
3. 在应用内弹窗登录同一 Kimi 账号，完成

之后打开 App 即进入工作区。

## 它是怎么工作的

App 本身只是一个安全的配对壳：配对链接加密保存在本机，远程页面用全屏 WebView 加载官方远程控制服务。所有代码执行、文件读写都发生在你的电脑上，手机只是窗口。仅允许 HTTPS，不申请存储、通讯录、定位等多余权限。

## 常见问题

- **电脑必须开着吗？** 是。电脑休眠、断网或 Desktop 退出后远程控制不可用。
- **想换一台电脑配对？** 当前版本没有应用内换配对入口，清除应用数据或重装后重新扫码。
- **桌面端重建了远程链接？** 旧配对会失效，同样清除数据后重新配对。
- **是官方应用吗？** 不是。这是第三方客户端，远程控制能力由 Kimi Code Desktop 官方服务提供。

## 自己构建

环境：JDK 17 + Android SDK 35 + Gradle 8.13。

```bash
gradle testDebugUnitTest assembleRelease
```

- `local.properties` 需配置 `sdk.dir` 指向本机 Android SDK
- 没有 `signing/keystore.properties` 时 release 自动回退 debug 签名，可直接侧载
- Windows 下项目路径不能含中文（AGP 限制），可用 `subst` 映射纯 ASCII 盘符解决
- 仓库带 GitHub Actions 工作流，push / PR / 打 `v*` tag 自动构建并上传 APK artifact

## 来源与许可

本仓库 fork 自 [hf-zhangyang/kimi-code-mobile](https://github.com/hf-zhangyang/kimi-code-mobile)，新增 GitHub Actions 构建工作流（已向上游提交 PR）。

项目代码以 [MIT License](LICENSE) 开源。第三方组件：JourneyApps ZXing（Apache 2.0）、AndroidX Security Crypto / Tink，完整许可见 [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md)。
