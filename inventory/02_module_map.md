# 模块映射 (Module Map)

**创建时间**: 2026-04-08

---

## 1. Android 模块 → iOS 模块映射

### 1.1 顶层模块映射

| Android 模块 | 职责 | iOS 模块 | 迁移状态 |
|--------------|------|----------|----------|
| `:app` | 主应用，UI + 业务逻辑 | `App/` + `Features/` | 🔄 部分完成 |
| `:modules:book` | 书籍解析、本地文件支持 | `Core/Parser/` + `Core/Reader/` | 🔄 部分完成 |
| `:modules:rhino` | JS 执行引擎 | `Core/RuleEngine/JSBridge.swift` | ✅ 已实现 |
| `:modules:web` | 网络请求、HTML 解析 | `Core/Network/` + SwiftSoup | ✅ 已实现 |

### 1.2 app 模块内部映射

| Android 目录 | 职责 | iOS 目录 | 迁移状态 |
|--------------|------|----------|----------|
| `api/` | 外部 API 控制器 | `Core/API/` | ✅ 已实现 |
| `base/` | 基础类 | `Core/Base/` | ❌ 未迁移 |
| `constant/` | 常量定义 | `Core/Config/AppConstants.swift` | ✅ 已实现 |
| `data/dao/` | 数据库 DAO | `Core/Persistence/` | ✅ 已实现 |
| `data/entities/` | 实体类 | `Core/Persistence/*+CoreDataClass.swift` | ✅ 已实现 |
| `exception/` | 异常定义 | ❌ 未迁移 | ❌ |
| `help/` | 工具类 | 分散在各模块 | 🔄 部分完成 |
| `lib/` | 库封装 | `Core/` | 🔄 部分完成 |
| `model/` | 业务模型 | `Core/Model/` | 🔄 部分完成 |
| `receiver/` | 广播接收器 | ❌ iOS 不支持 | ⚠️ 需替代 |
| `service/` | 后台服务 | `Core/Cache/BackgroundCacheService.swift` | 🔄 部分完成 |
| `ui/` | 用户界面 | `Features/` | 🔄 部分完成 |
| `utils/` | 工具类 | 分散在各模块 | 🔄 部分完成 |
| `web/` | Web 服务 | `Core/WebServer/` | ✅ 已实现 |

---

## 2. UI 模块详细映射

### 2.1 主要页面映射

| Android UI 目录 | 页面功能 | iOS 对应 | 迁移状态 |
|-----------------|----------|----------|----------|
| `ui/about/` | 关于页面 | ❌ 未迁移 | ❌ |
| `ui/association/` | URL Scheme 导入 | `Core/Import/URLSchemeHandler.swift` | ✅ 已实现 |
| `ui/browser/` | 内置浏览器 | `Features/Source/BuiltInBrowserView.swift` | ✅ 已实现 |
| `ui/code/` | 代码编辑 | ❌ 未迁移 | ❌ |
| `ui/config/` | 配置页（12+） | `Features/Config/` | 🔄 部分完成 |
| `ui/dict/` | 字典规则 | `Features/Config/DictRuleView.swift` | ✅ 已实现 |
| `ui/file/` | 文件管理 | `Features/Config/FileManageView.swift` | ✅ 已实现 |
| `ui/font/` | 字体设置 | ❌ 未迁移 | ❌ |
| `ui/login/` | 登录功能 | ❌ 未迁移 | ❌ |
| `ui/main/` | 主页面 | `App/MainTabView.swift` | ✅ 已实现 |
| `ui/qrcode/` | 二维码 | `Features/Source/QRCodeScanView.swift` | ✅ 已实现 |
| `ui/replace/` | 替换规则 | `Features/Config/ReplaceRuleView.swift` | ✅ 已实现 |
| `ui/video/` | 视频播放 | ❌ 未迁移 | ❌ |
| `ui/welcome/` | 欢迎页 | ❌ 未迁移 | ❌ |
| `ui/widget/` | 桌面组件 | ❌ iOS 不支持 | ⚠️ 需替代 |

### 2.2 book 模块详细映射

| Android 目录 | 页面功能 | iOS 对应 | 迁移状态 |
|--------------|----------|----------|----------|
| `book/audio/` | 音频书籍 | `Features/AudioPlayer/` | ✅ 已实现 |
| `book/bookmark/` | 书签管理 | `Features/Reader/BookmarkSheet.swift` | ✅ 已实现 |
| `book/cache/` | 缓存管理 | `Core/Cache/` | ✅ 已实现 |
| `book/changecover/` | 封面更换 | ❌ 未迁移 | ❌ |
| `book/changesource/` | 书源更换 | `Features/Reader/ChangeSourceSheet.swift` | ✅ 已实现 |
| `book/explore/` | 发现页 | `Features/Discovery/DiscoveryView.swift` | ✅ 已实现 |
| `book/group/` | 分组管理 | `Features/Source/GroupManageView.swift` | ✅ 已实现 |
| `book/import/` | 书籍导入 | `Features/Bookshelf/AddBookView.swift` | ✅ 已实现 |
| `book/info/` | 书籍详情 | `Features/BookDetail/BookDetailView.swift` | ✅ 已实现 |
| `book/manage/` | 书籍管理 | `Features/Bookshelf/` | ✅ 已实现 |
| `book/manga/` | 漫画阅读 | `Features/MangaReader/` | ✅ 已实现 |
| `book/read/` | 阅读器 | `Features/Reader/` + `Core/Reader/` | ✅ 已实现 |
| `book/search/` | 书籍搜索 | `Features/Search/` | ✅ 已实现 |
| `book/searchContent/` | 内容搜索 | `Features/Reader/SearchContentView.swift` | ✅ 已实现 |
| `book/source/` | 书源管理 | `Features/Source/` | ✅ 已实现 |
| `book/toc/` | 目录页 | 集成在 ReaderView | ✅ 已实现 |

### 2.3 RSS 模块详细映射

| Android 目录 | 页面功能 | iOS 对应 | 迁移状态 |
|--------------|----------|----------|----------|
| `rss/article/` | RSS 文章列表 | `Features/RSS/RSSSubscriptionView.swift` | ✅ 已实现 |
| `rss/favorites/` | RSS 收藏 | `Features/RSS/RssFavoritesView.swift` | ✅ 已实现 |
| `rss/read/` | RSS 阅读 | 集成在 SubscriptionView | ✅ 已实现 |
| `rss/source/` | RSS 源管理 | `Features/RSS/RssSourceEditView.swift` | ✅ 已实现 |
| `rss/subscription/` | RSS 订阅 | `Features/RSS/RSSSubscriptionView.swift` | ✅ 已实现 |

---

## 3. 配置页面映射

| Android 文件 | 配置功能 | iOS 对应 | 迁移状态 |
|--------------|----------|----------|----------|
| `ConfigActivity.kt` | 配置入口 | `Features/Config/SettingsView.swift` | ✅ 已实现 |
| `WelcomeConfigFragment.kt` | 欢迎配置 | ❌ 未迁移 | ❌ |
| `ThemeConfigFragment.kt` | 主题配置 | `Core/Theme/ThemeManager.swift` | ✅ 已实现 |
| `ThemeListDialog.kt` | 主题列表 | 集成在 ThemeManager | ✅ 已实现 |
| `CoverConfigFragment.kt` | 封面配置 | ❌ 未迁移 | ❌ |
| `CoverRuleConfigDialog.kt` | 封面规则配置 | ❌ 未迁移 | ❌ |
| `BackupConfigFragment.kt` | 备份配置 | `Features/Config/BackupRestoreView.swift` | ✅ 已实现 |
| `OtherConfigFragment.kt` | 其他配置 | `Features/Config/SettingsView.swift` | 🔄 部分完成 |
| `CheckSourceConfig.kt` | 书源检查配置 | `Core/Source/SourceChecker.swift` | ✅ 已实现 |
| `DirectLinkUploadConfig.kt` | 直链上传配置 | ❌ 未迁移 | ❌ |

---

## 4. 阅读器模块映射

### 4.1 阅读器核心文件

| Android 文件 | 功能 | iOS 对应 | 迁移状态 |
|--------------|------|----------|----------|
| `ReadBookActivity.kt` | 阅读主页面 | `Features/Reader/ReaderView.swift` | ✅ 已实现 |
| `BaseReadBookActivity.kt` | 阅读基类 | `Features/Reader/ReaderViewModel.swift` | ✅ 已实现 |
| `ReadBookViewModel.kt` | 阅读视图模型 | `Features/Reader/ReaderViewModel.swift` | ✅ 已实现 |
| `ReadMenu.kt` | 阅读菜单 | `Features/Reader/ReaderConfigSheets.swift` | ✅ 已实现 |
| `MangaMenu.kt` | 漫画菜单 | `Features/MangaReader/` | ✅ 已实现 |
| `SearchMenu.kt` | 搜索菜单 | `Features/Reader/SearchContentView.swift` | ✅ 已实现 |
| `TextActionMenu.kt` | 文本操作菜单 | `Features/Reader/TextActionMenu.swift` | ✅ 已实现 |
| `ContentEditDialog.kt` | 内容编辑 | `Features/Reader/ContentEditSheet.swift` | ✅ 已实现 |
| `EffectiveReplacesDialog.kt` | 有效替换 | `Features/Reader/EffectiveReplacesSheet.swift` | ✅ 已实现 |

### 4.2 阅读器页面组件

| Android 目录 | 功能 | iOS 对应 | 迁移状态 |
|--------------|------|----------|----------|
| `page/ContentTextView.kt` | 文本视图 | `Features/Reader/HTMLContentView.swift` | ✅ 已实现 |
| `page/PageView.kt` | 页面视图 | `Core/Reader/Views/` | ✅ 已实现 |
| `page/ReadView.kt` | 阅读视图 | `Features/Reader/ReaderView.swift` | ✅ 已实现 |
| `page/AutoPager.kt` | 自动翻页 | `Features/Reader/AutoPageTurnManager.swift` | ✅ 已实现 |
| `page/api/` | 页面 API | `Core/Reader/` | ✅ 已实现 |
| `page/delegate/` | 翻页代理 | `Core/Reader/PageDelegate/` | ✅ 已实现 |
| `page/entities/` | 页面实体 | `Core/Reader/Models/` | ✅ 已实现 |
| `page/provider/` | 内容提供者 | `Core/Reader/Provider/` | ✅ 已实现 |

### 4.3 阅读器配置组件

| Android 文件 | 功能 | iOS 对应 | 迁移状态 |
|--------------|------|----------|----------|
| `AutoReadDialog.kt` | 自动朗读 | `Features/Reader/TTSControlsView.swift` | ✅ 已实现 |
| `BgAdapter.kt` | 背景适配 | 集成在 ThemeManager | ✅ 已实现 |
| `BgTextConfigDialog.kt` | 背景文本配置 | `Features/Reader/ReaderSettingsFullView.swift` | ✅ 已实现 |
| `ChineseConverter.kt` | 简繁转换 | ❌ 未迁移 | ❌ |
| `ClickActionConfigDialog.kt` | 点击动作配置 | ❌ 未迁移 | ❌ |
| `HttpTtsEditDialog.kt` | HTTP TTS 编辑 | `Features/Config/HttpTTSConfigView.swift` | ✅ 已实现 |
| `MoreConfigDialog.kt` | 更多配置 | `Features/Reader/ReaderSettingsFullView.swift` | ✅ 已实现 |
| `PaddingConfigDialog.kt` | 边距配置 | 集成在 ReaderSettingsFullView | ✅ 已实现 |
| `PageKeyDialog.kt` | 页面按键 | ❌ 未迁移 | ❌ |
| `ReadAloudConfigDialog.kt` | 朗读配置 | `Core/TTS/` | ✅ 已实现 |
| `ReadAloudDialog.kt` | 朗读对话框 | `Features/Reader/TTSControlsView.swift` | ✅ 已实现 |
| `ReadStyleDialog.kt` | 阅读样式 | `Features/Reader/ReaderSettingsFullView.swift` | ✅ 已实现 |
| `SpeakEngineDialog.kt` | 朗读引擎 | 集成在 TTSManager | ✅ 已实现 |
| `TextFontWeightConverter.kt` | 字重转换 | ❌ 未迁移 | ❌ |
| `TipConfigDialog.kt` | 提示配置 | ❌ 未迁移 | ❌ |

---

## 5. 书源管理模块映射

| Android 目录 | 功能 | iOS 对应 | 迁移状态 |
|--------------|------|----------|----------|
| `source/debug/` | 书源调试 | `Features/Source/SourceDebugView.swift` | ✅ 已实现 |
| `source/edit/` | 书源编辑 | `Features/Source/SourceEditView.swift` | ✅ 已实现 |
| `source/manage/` | 书源管理 | `Features/Source/SourceManageView.swift` | ✅ 已实现 |

---

## 6. 数据模型映射

| Android 实体 | iOS 对应 | 迁移状态 |
|--------------|----------|----------|
| `Book.kt` | `Book+CoreDataClass.swift` | ✅ 已实现 |
| `BookChapter.kt` | `BookChapter+CoreDataClass.swift` | ✅ 已实现 |
| `BookGroup.kt` | `BookGroup+CoreDataClass.swift` | ✅ 已实现 |
| `Bookmark.kt` | `Bookmark+CoreDataClass.swift` | ✅ 已实现 |
| `BookSource.kt` | `BookSource+CoreDataClass.swift` | ✅ 已实现 |
| `BookProgress.kt` | `BookProgress+CoreDataClass.swift` | ✅ 已实现 |
| `Cookie.kt` | `Cookie+CoreDataClass.swift` | ✅ 已实现 |
| `ReplaceRule.kt` | `ReplaceRule+CoreDataClass.swift` | ✅ 已实现 |
| `RssSource.kt` | `RssSource+CoreDataClass.swift` | ✅ 已实现 |
| `RssArticle.kt` | `RssArticle+CoreDataClass.swift` | ✅ 已实现 |
| `RssReadRecord.kt` | `RssReadRecord+CoreDataClass.swift` | ✅ 已实现 |
| `RssStar.kt` | `RssStar+CoreDataClass.swift` | ✅ 已实现 |
| `SearchBook.kt` | `SearchBook+CoreDataClass.swift` | ✅ 已实现 |
| `SearchKeyword.kt` | `SearchKeyword+CoreDataClass.swift` | ✅ 已实现 |
| `HttpTTS.kt` | `HttpTTS+CoreDataClass.swift` | ✅ 已实现 |
| `DictRule.kt` | `DictRule+CoreDataClass.swift` | ✅ 已实现 |
| `RuleSub.kt` | `RuleSub+CoreDataClass.swift` | ✅ 已实现 |
| `TxtTocRule.kt` | `TxtTocRule+CoreDataClass.swift` | ✅ 已实现 |
| `Cache.kt` | `CacheEntry+CoreDataClass.swift` | ✅ 已实现 |
| `ReadRecord.kt` | `ReadRecord+CoreDataClass.swift` | ✅ 已实现 |
| `Server.kt` | ❌ 未迁移 | ❌ |
| `KeyboardAssist.kt` | ❌ 未迁移 | ❌ |
| `BookChapterReview.kt` | ❌ 未迁移 | ❌ |
| `BookSourcePart.kt` | ❌ 未迁移 | ❌ |

---

## 7. 服务与后台任务映射

| Android 服务 | 功能 | iOS 对应 | 迁移状态 |
|--------------|------|----------|----------|
| `BackgroundService` | 后台下载/缓存 | `BackgroundCacheService.swift` | ✅ 已实现 |
| `ReadAloudService` | 后台朗读 | `AVFoundation` | ✅ 已实现 |
| `ContentProvider` | 外部数据访问 | `URLSchemeHandler` + `APIServer` | ✅ 已实现 |
| `BroadcastReceiver` | 事件监听 | `NotificationCenter` | ⚠️ 需适配 |

---

## 8. 模块边界与依赖

### 8.1 iOS 模块依赖关系

```
App/
├── 依赖 → Features/
├── 依赖 → Core/
└── 依赖 → Resources/

Features/
├── Bookshelf/ → Core/Persistence, Core/Network
├── Reader/ → Core/Reader, Core/Persistence, Core/TTS
├── Search/ → Core/RuleEngine, Core/Network
├── Source/ → Core/RuleEngine, Core/Persistence
├── RSS/ → Core/RuleEngine, Core/Persistence
└── Config/ → Core/Sync, Core/Persistence

Core/
├── Persistence/ → 无外部依赖
├── Network/ → 无外部依赖
├── RuleEngine/ → JavaScriptCore, SwiftSoup, Kanna
├── WebServer/ → Network.framework
├── Reader/ → TextKit, CoreData
└── TTS/ → AVFoundation
```

### 8.2 关键依赖说明

| iOS 模块 | 外部依赖 | 用途 |
|----------|----------|------|
| `Core/RuleEngine` | JavaScriptCore | JS 规则执行 |
| `Core/RuleEngine` | SwiftSoup | HTML 解析 |
| `Core/RuleEngine` | Kanna | XPath 解析 |
| `Core/Reader` | TextKit 2 | 文本渲染与分页 |
| `Core/TTS` | AVFoundation | 语音朗读 |
| `Core/Sync` | WebDAV 协议 | 云同步 |