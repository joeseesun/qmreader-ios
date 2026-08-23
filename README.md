# QMReader iOS

**中文** | [English](#english)

![QMReader iOS 阅读外观](docs/assets/reading-appearance.png)

> 专注中文长文、翻译与乔木改写的原生 SwiftUI 阅读器。
> A native SwiftUI reader for Chinese long-form reading, translation, and Qiaomu rewrites.

[![iOS Build](https://github.com/joeseesun/qmreader-ios/actions/workflows/build.yml/badge.svg)](https://github.com/joeseesun/qmreader-ios/actions/workflows/build.yml)
[![iOS 17+](https://img.shields.io/badge/iOS-17%2B-111111)](https://developer.apple.com/ios/)
[![SwiftUI](https://img.shields.io/badge/UI-SwiftUI-F05138)](https://developer.apple.com/xcode/swiftui/)
[![MIT License](https://img.shields.io/badge/code-MIT-green.svg)](LICENSE)

**已验证：** `ReaderLogicTests: PASS`；Xcode 26.2 无签名构建与 Apple Development 真机签名构建通过；0.5.0 已安装至 iPhone 15 Pro。

## 这是什么

QMReader iOS 是 [QMReader](https://rss.qiaomu.ai) 的轻量原生客户端。它把 RSS 文章、中文翻译和“乔木改写”放进一个安静、快速、可离线回看的阅读界面，重点解决三件事：

- 先看到可读的中文改写，而不是先闪出英文原文。
- 用原生导航、缓存、下拉刷新和频道历史缩短等待。
- 用真正会切换的中文字体、行距、页边距和纸面背景改善长文阅读。

## 核心能力

| 能力 | 你得到什么 |
| --- | --- |
| 改写优先列表 | 首页与频道只展示已经完成乔木改写的文章 |
| 原生频道历史 | 单独进入来源，继续加载历史消息 |
| 三种阅读内容 | 在原文、系统翻译和乔木改写之间切换 |
| 阅读外观 | 字号、三档行距、三档页边距、五种背景即时预览 |
| 五款开源中文字体 | 霞鹜文楷、霞鹜文楷 TC、朱雀仿宋、思源宋体、文津宋体随 App 分发 |
| 缓存与刷新 | 首屏优先读缓存；下拉刷新不清空当前列表 |
| 站内分享 | 分享 QMReader 的 canonical 改写页，原文链接仍可单独打开 |
| 链接加入 | 长按文章中的链接，可提交给 QMReader 抓取和改写 |

## 最快开始

```bash
git clone https://github.com/joeseesun/qmreader-ios.git
cd qmreader-ios
open QMReader.xcodeproj
```

然后在 Xcode 中：

1. 打开 `QMReader` Target → **Signing & Capabilities**。
2. 选择你自己的 Apple Development Team。
3. 如果 `ai.qiaomu.qmreader` 已被占用，把 Bundle Identifier 改为你自己的反向域名。
4. 选择 iOS 17+ 模拟器或已开启 Developer Mode 的 iPhone，点击 Run。

### 命令行验证

```bash
./run-reader-logic-tests.sh

xcodebuild \
  -project QMReader.xcodeproj \
  -scheme QMReader \
  -configuration Debug \
  -destination 'generic/platform=iOS Simulator' \
  CODE_SIGNING_ALLOWED=NO \
  build
```

## 阅读体验

- 背景：自动、暖纸、素白、护眼、深夜。
- 字体：系统苹方 + 五款 OFL 中文字体。
- 排版：15–24pt 字号、三档行距、三档页边距、多级标题节奏。
- 辅助功能：Dynamic Type、VoiceOver、Reduce Motion、44pt 触控区。

背景放在字号之后，打开面板即可看到；字体卡片直接用对应字体渲染“山高水长”，避免“设置显示已切换、正文仍然没变”。

顶部分享按钮生成 `https://rss.qiaomu.ai/articles/<slug>--<id>/rewrite` 站内链接；更多菜单中的“在 Safari 打开原文”才使用源站 URL。

## 数据与架构边界

| 层 | 职责 |
| --- | --- |
| SwiftUI App | 列表、频道、阅读器、缓存、收藏/已读状态、系统分享与刷新反馈 |
| `rss.qiaomu.ai` | RSS 数据、文章详情、翻译、乔木改写和链接抓取 |
| 本机存储 | URLCache、文章快照、已读/收藏和阅读外观设置 |

当前公开版本默认连接 `https://rss.qiaomu.ai`。若要连接自己的兼容后端，需要同时修改：

- `QMReader/APIClient.swift` 中的 `baseURL`
- `QMReader/ArticleShare.swift` 中的 `ArticleShareLink.baseURL`

长按“加入乔木阅读”会把目标 URL 发送到 QMReader 服务端进行抓取；请不要提交私密链接。

## 内置字体与许可证

App 内置五款 SIL OFL 1.1 字体。为控制真机开发安装体积，霞鹜文楷、霞鹜文楷 TC 与朱雀仿宋使用 GB2312/Big5 阅读子集；生僻扩展字由 iOS 自动回退系统字体。完整来源、版本和许可证见 [字体说明](QMReader/Fonts/Licenses/README.md)。

代码采用 [MIT License](LICENSE)，字体继续遵循各自的 SIL OFL 1.1 许可证。

## 已知限制

- 这是源码发布，不提供 App Store 或公开签名 IPA；真机运行需要你自己的 Apple Development Team。
- 当前版本以 Xcode 26.2、iOS 17 最低部署目标完成验证。
- 系统翻译桥接只在 iOS 18+ 可用；其他系统仍可阅读原文和服务端改写。
- 后端地址目前通过代码配置，还没有 App 内自定义服务器界面。
- 五款中文字体会增加约 45 MB 的未压缩 App 体积。

## 贡献与安全

欢迎聚焦阅读体验、可访问性、缓存、频道和兼容后端的贡献。提交前请阅读 [CONTRIBUTING.md](CONTRIBUTING.md) 和 [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md)。安全问题请按 [SECURITY.md](SECURITY.md) 私下报告。

## 关于向阳乔木

QMReader 来自向阳乔木的日常 AI 阅读与内容工作流实践：关注的不是信息堆积，而是怎样更快得到可信、可读、可复用的中文理解。

- 个人站：[qiaomu.ai](https://qiaomu.ai)
- 博客：[blog.qiaomu.ai](https://blog.qiaomu.ai)
- 乔木推荐：[tuijian.qiaomu.ai](https://tuijian.qiaomu.ai)
- X：[@vista8](https://x.com/vista8)
- GitHub：[@joeseesun](https://github.com/joeseesun)
- 微信公众号：向阳乔木推荐看

---

<a name="english"></a>

# English

QMReader iOS is a native SwiftUI client for [QMReader](https://rss.qiaomu.ai), built for long-form reading with Chinese translations and Qiaomu-style rewrites.

## What you get

- A rewrite-first feed that avoids flashing short English originals before Chinese content is ready.
- Native source history, pull-to-refresh, caching, read/favorite state, and system sharing.
- Original, system-translation, and Qiaomu-rewrite reading modes.
- Five paper themes, adjustable type size/line spacing/margins, and five bundled OFL Chinese fonts.
- Internal canonical share links while keeping the original-source URL available separately.

## Run it

```bash
git clone https://github.com/joeseesun/qmreader-ios.git
cd qmreader-ios
open QMReader.xcodeproj
```

Select your Apple Development Team and use your own Bundle Identifier when running on a physical device. The deployment target is iOS 17.

```bash
./run-reader-logic-tests.sh
xcodebuild -project QMReader.xcodeproj -scheme QMReader \
  -configuration Debug \
  -destination 'generic/platform=iOS Simulator' \
  CODE_SIGNING_ALLOWED=NO build
```

## Boundaries

The app fetches feed, article, translation, and rewrite data from `https://rss.qiaomu.ai`. Submitting a link sends that URL to the QMReader backend. Reading preferences, read/favorite state, and cached snapshots stay on the device.

This repository ships source code only—there is no public signed IPA or App Store build. System Translation requires iOS 18+. To use a compatible self-hosted backend, update the base URLs in `APIClient.swift` and `ArticleShare.swift`.

The app code is MIT licensed. Bundled fonts retain their upstream SIL OFL 1.1 licenses; see [font provenance](QMReader/Fonts/Licenses/README.md).

Maintained by [向阳乔木 / Joe](https://qiaomu.ai) · [@vista8](https://x.com/vista8) · [@joeseesun](https://github.com/joeseesun)
