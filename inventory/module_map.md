# Legado iOS Migration - Module Map

> 本文档记录 Android Legado 模块到 iOS 的映射关系。

**生成日期**: 2026-04-08

---

## 1. 模块映射总览

| Android 模块 | iOS 模块 | 说明 |
|--------------|----------|------|
| `:app` | `Legado` | 主应用 Target |
| `:modules:book` | `ReaderCore` | 阅读核心框架 |
| `:modules:rhino` | `JSRuleRuntime` | JS 规则运行时 |
| `:modules:web` | - | Web 界面（iOS 暂不需要） |

---

## 2. :app 模块映射

### 2.1 api 层

| Android 目录 | iOS 目录 | 输入 | 输出 | 状态 |
|--------------|----------|------|------|------|
| `api/ApiController.kt` | `Core/API/Controllers/` | HTTP Request | JSON Response | 待迁移 |
| `api/ReturnData.kt` | `Core/API/Models/ReturnData.swift` | - | - | 待迁移 |
| `api/SourceDebug.kt` | `Core/API/Debugging/` | WebSocket Message | Debug Output | 待迁移 |

### 2.2 base 层

| Android 目录 | iOS 目录 | 职责 | 状态 |
|--------------|----------|------|------|
| `base/BaseActivity.kt` | `Core/Base/BaseViewController.swift` | Activity 基类 | 待迁移 |
| `base/BaseFragment.kt` | `Core/Base/BaseFragment.swift` | Fragment 基类 | 待迁移 |
| `base/BaseViewModel.kt` | `Core/Base/BaseViewModel.swift` | ViewModel 基类 | 待迁移 |

### 2.3 data 层

| Android 目录 | iOS 目录 | 职责 | 状态 |
|--------------|----------|------|------|
| `data/entities/` | `Core/Persistence/Entities/` | 数据实体 | ✅ 部分完成 |
| `data/dao/` | `Core/Persistence/DAO/` | 数据访问对象 | 待迁移 |
| `data/AppDatabase.kt` | `Core/Persistence/CoreDataStack.swift` | 数据库管理 | ✅ 已完成 |

### 2.4 help 层

| Android 目录 | iOS 目录 | 职责 | 状态 |
|--------------|----------|------|------|
| `help/book/BookHelp.kt` | `Core/Reader/Provider/BookHelp.swift` | 书籍缓存管理 | ✅ 已完成 |
| `help/book/ContentProcessor.kt` | `Core/Reader/Provider/ContentProcessor.swift` | 内容处理 | ✅ 已完成 |
| `help/http/` | `Core/Network/` | HTTP 帮助类 | 待迁移 |
| `help/storage/` | `Core/Storage/` | 存储帮助类 | 待迁移 |

### 2.5 model 层

| Android 目录 | iOS 目录 | 职责 | 状态 |
|--------------|----------|------|------|
| `model/AnalyzeRule.kt` | `Core/Rules/AnalyzeRule.swift` | 规则解析核心 | 🔄 进行中 |
| `model/AnalyzeUrl.kt` | `Core/Rules/AnalyzeUrl.swift` | URL 分析 | 待迁移 |
| `model/LocalBook.kt` | `Core/Reader/LocalBook.swift` | 本地书籍解析 | 待迁移 |
| `model/ReadBook.kt` | `Core/Reader/ReadBook.swift` | 阅读管理 | ✅ 已完成 |

### 2.6 ui 层

| Android 目录 | iOS 目录 | 职责 | 状态 |
|--------------|----------|------|------|
| `ui/main/` | `Features/Main/` | 主界面 | 待迁移 |
| `ui/book/read/` | `Features/Reader/` | 阅读页 | ✅ 部分完成 |
| `ui/book/search/` | `Features/Search/` | 搜索页 | 待迁移 |
| `ui/book/source/` | `Features/Source/` | 书源管理 | 待迁移 |
| `ui/book/toc/` | `Features/Toc/` | 目录页 | 待迁移 |
| `ui/rss/` | `Features/RSS/` | RSS 订阅 | 待迁移 |
| `ui/config/` | `Features/Config/` | 配置页 | 待迁移 |

### 2.7 web 层

| Android 目录 | iOS 目录 | 职责 | 状态 |
|--------------|----------|------|------|
| `web/WebServer.kt` | `Core/WebServer/` | HTTP 服务 | 待迁移 |
| `web/WebSocket.kt` | `Core/WebSocket/` | WebSocket 服务 | 待迁移 |

---

## 3. :modules:book 模块映射

| Android 类 | iOS 类 | 职责 | 状态 |
|------------|--------|------|------|
| `LocalBook.kt` | `LocalBook.swift` | 本地书籍入口 | 待迁移 |
| `EpubFile.kt` | `EpubFile.swift` | EPUB 解析 | 待迁移 |
| `TxtFile.kt` | `TxtFile.swift` | TXT 解析 | 待迁移 |
| `PdfFile.kt` | `PdfFile.swift` | PDF 解析 | 待迁移 |
| `MobiFile.kt` | `MobiFile.swift` | MOBI 解析 | 待迁移 |
| `BookHelp.kt` | `BookHelp.swift` | 缓存管理 | ✅ 已完成 |
| `ImageProvider.kt` | `ImageProvider.swift` | 图片缓存 | ✅ 已完成 |

---

## 4. :modules:rhino 模块映射

| Android 实现 | iOS 实现 | 说明 |
|--------------|----------|------|
| `RhinoScriptEngine` | `JSContext` | JS 执行引擎 |
| `ScriptRuntime` | `ScriptRuntime.swift` | JS 运行时环境 |
| `JS 库注入` | `JS 库注入` | 自定义 JS 库 |

---

## 5. 依赖关系

```
iOS 架构依赖图:

┌─────────────────────────────────────────────────────────────┐
│                      Legado (App Target)                     │
├─────────────────────────────────────────────────────────────┤
│  Features/                                                  │
│  ├── Main/          → Core/Base, Core/UI                    │
│  ├── Reader/        → ReaderCore, Core/Rules                │
│  ├── Search/        → Core/Rules, Core/Network              │
│  ├── Source/        → Core/Rules, Core/Network              │
│  ├── RSS/           → Core/Rules, Core/Network              │
│  └── Config/        → Core/Settings                         │
├─────────────────────────────────────────────────────────────┤
│  Core/                                                      │
│  ├── Base/          → UIKit                                 │
│  ├── Persistence/   → CoreData, SQLite                      │
│  ├── Network/       → URLSession                            │
│  ├── Rules/         → JSRuleRuntime, SwiftSoup              │
│  ├── Reader/        → ReaderCore                            │
│  └── Settings/      → UserDefaults                          │
├─────────────────────────────────────────────────────────────┤
│  ReaderCore (Framework)                                     │
│  ├── LocalBook/     → ZIPFoundation                         │
│  ├── Layout/        → TextKit, CoreText                     │
│  └── Cache/         → FileManager                           │
├─────────────────────────────────────────────────────────────┤
│  JSRuleRuntime (Framework)                                  │
│  ├── JSEngine/      → JavaScriptCore                        │
│  ├── Runtime/       → Foundation                            │
│  └── Libraries/     → 自定义 JS 库                          │
└─────────────────────────────────────────────────────────────┘
```

---

## 6. 边界定义

### 6.1 Core 层边界

| 模块 | 职责 | 不负责 |
|------|------|--------|
| `Core/Persistence` | 数据持久化 | 业务逻辑 |
| `Core/Network` | 网络请求 | 规则解析 |
| `Core/Rules` | 规则解析 | UI 展示 |
| `Core/Reader` | 阅读引擎 | 书源管理 |

### 6.2 Features 层边界

| 模块 | 职责 | 不负责 |
|------|------|--------|
| `Features/Reader` | 阅读页 UI | 规则执行 |
| `Features/Source` | 书源管理 UI | 网络请求 |
| `Features/Search` | 搜索 UI | 数据存储 |

---

## 7. 状态管理

| 模块 | Android 方式 | iOS 方式 |
|------|--------------|----------|
| `ViewModel` | `androidx.lifecycle.ViewModel` | `ObservableObject` |
| `LiveData` | `androidx.lifecycle.LiveData` | `@Published` |
| `State` | `StateFlow` | `@State` / `@Binding` |
| `Database` | `Room` | `CoreData` |
| `Preferences` | `SharedPreferences` | `UserDefaults` |

---

*本文档由 Wave 0 基线采集自动生成*