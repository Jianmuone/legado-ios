# 项目概述 (Project Overview)

**创建时间**: 2026-04-08  
**Android 源项目**: Luoyacheng/legado  
**iOS 目标项目**: legado-ios

---

## 1. Android 工程模块清单

### 1.1 根模块结构

```
legado/
├── app/                    # 主应用模块
│   └── src/main/java/io/legado/app/
│       ├── App.kt          # Application 入口
│       ├── api/            # 外部 API 控制器
│       ├── base/           # 基础类
│       ├── constant/       # 常量定义
│       ├── data/           # 数据层
│       │   ├── dao/        # 数据库 DAO
│       │   └── entities/   # 实体类
│       ├── exception/      # 异常定义
│       ├── help/           # 工具类
│       ├── lib/            # 库封装
│       ├── model/          # 业务模型
│       ├── receiver/       # 广播接收器
│       ├── service/        # 后台服务
│       ├── ui/             # 用户界面
│       ├── utils/          # 工具类
│       └── web/            # Web 服务
├── modules/
│   ├── book/               # 书籍解析模块
│   ├── rhino/              # JS 引擎模块
│   └── web/                # Web 工具模块
└── build.gradle
```

### 1.2 模块职责

| 模块 | 职责 | 依赖 |
|------|------|------|
| `app` | 主应用，包含所有 UI 和业务逻辑 | 所有子模块 |
| `modules/book` | 书籍解析、本地文件支持、EPUB/TXT 解析 | 无 |
| `modules/rhino` | JavaScript 执行引擎（Rhino） | 无 |
| `modules/web` | 网络请求、HTML 解析、Web 工具 | 无 |

### 1.3 UI 层目录结构

```
ui/
├── about/              # 关于页面
├── association/        # 关联功能
├── book/               # 书籍功能（核心）
│   ├── audio/          # 音频书籍
│   ├── bookmark/       # 书签管理
│   ├── cache/          # 缓存管理
│   ├── changecover/    # 封面更换
│   ├── changesource/   # 书源更换
│   ├── explore/        # 发现/探索
│   ├── group/          # 分组管理
│   ├── import/         # 书籍导入
│   ├── info/           # 书籍详情
│   ├── manage/         # 书籍管理
│   ├── manga/          # 漫画阅读
│   ├── read/           # 阅读器（最核心）
│   ├── search/         # 书籍搜索
│   ├── searchContent/  # 内容搜索
│   ├── source/         # 书源管理
│   └── toc/            # 目录
├── browser/            # 内置浏览器
├── code/               # 代码编辑
├── config/             # 配置页（12+ 个）
├── dict/               # 字典规则
├── file/               # 文件管理
├── font/               # 字体设置
├── login/              # 登录功能
├── main/               # 主页面
├── qrcode/             # 二维码
├── replace/            # 替换规则
├── rss/                # RSS 功能
│   ├── article/        # 文章列表
│   ├── favorites/      # 收藏
│   ├── read/           # 阅读
│   ├── source/         # 源管理
│   └── subscription/   # 订阅
├── video/              # 视频播放
├── welcome/            # 欢迎页
└── widget/             # 桌面组件
```

---

## 2. 迁移总策略

### 2.1 核心原则

1. **严格一比一移植**
   - 逐文件对照 Android 源码
   - 保持命名语义一致
   - 保持数据结构兼容

2. **优先级**
   - P0: 阅读器核心（book/read）
   - P1: 书源引擎（book/source + 规则执行）
   - P2: 书架管理（book/manage + group + cache）
   - P3: 搜索发现（book/search + explore）
   - P4: RSS 订阅（rss/*）
   - P5: 配置与辅助功能（config/*, replace/*, dict/* 等）

3. **技术选型约束**
   - 语言: Swift
   - UI: UIKit + Auto Layout（禁用 SwiftUI 先搭壳）
   - 数据: SQLite（CoreData 封装）
   - 网络: URLSession
   - JS: JavaScriptCore
   - 阅读器: TextKit 2

### 2.2 禁止事项

- ❌ 删减功能
- ❌ 合并页面
- ❌ 简化菜单层级
- ❌ 改变默认值
- ❌ 改变交互路径
- ❌ MVP 思维
- ❌ "以后再补"占位

---

## 3. iOS 技术选型

### 3.1 语言与框架

| 领域 | 技术选择 | 理由 |
|------|----------|------|
| 语言 | Swift 5.10 | iOS 原生，与 Xcode 15.4 兼容 |
| UI | UIKit + Auto Layout | 严格对照 Android 布局，禁用 SwiftUI |
| 导航 | UINavigationController + UITabBarController | 对应 Android Activity 结构 |
| 数据 | CoreData (SQLite) | 已有实现，保持兼容 |
| 网络 | URLSession | 原生，支持 Cookie/重试/缓存 |
| JS 引擎 | JavaScriptCore | 对应 Android Rhino |
| HTML 解析 | SwiftSoup | 对应 Android Jsoup |
| XPath | Kanna | 对应 Android XPath |
| 阅读器 | TextKit 2 + CoreText | 分页、仿真翻页、性能 |
| 音视频 | AVFoundation | 后台播放、进度同步 |

### 3.2 架构设计

```
Legado-iOS/
├── App/                    # 应用入口
│   ├── AppDelegate.swift
│   ├── SceneDelegate.swift
│   └── LegadoApp.swift
├── Core/                   # 核心能力
│   ├── Persistence/        # 数据持久化 (CoreData)
│   ├── Network/            # 网络层
│   ├── RuleEngine/         # 规则引擎
│   ├── WebServer/          # 本地 HTTP 服务
│   ├── Sync/               # WebDAV 同步
│   ├── TTS/                # 语音朗读
│   └── Import/             # 导入处理
├── Features/               # 功能模块
│   ├── Bookshelf/          # 书架
│   ├── Reader/             # 阅读器
│   ├── Search/             # 搜索
│   ├── Source/             # 书源管理
│   ├── RSS/                # RSS 订阅
│   └── Config/             # 配置
└── UIComponents/           # 通用组件
```

---

## 4. 风险点

### 4.1 高风险

| 风险 | 影响 | 缓解措施 |
|------|------|----------|
| JavaScript 兼容性 | 书源规则可能执行失败 | 使用相同测试用例回归 |
| 阅读器翻页效果 | 仿真翻页实现复杂 | 参考 Android PageView 实现 |
| Content Provider | iOS 无法原样实现 | 用 URL Scheme + 本地 HTTP 替代 |
| 后台服务 | iOS 后台限制严格 | 使用 BGTaskScheduler + 通知 |

### 4.2 中风险

| 风险 | 影响 | 缓解措施 |
|------|------|----------|
| 横屏布局 | 需要单独适配 | 严格对照 layout-land |
| 夜间模式 | 需要全局主题切换 | 已有 ThemeManager |
| 多语言 | 需要翻译所有文案 | 从 Android values/ 提取 |

---

## 5. 验收方式

### 5.1 对照验收

- 同一页面、同状态、同数据，截图对比
- 同一操作路径，行为回放对比
- 同一书源，搜索/目录/正文结果对比

### 5.2 兼容验收

- 导入 Android 导出的 JSON 书源
- 导入 Android 导出的备份文件
- WebDAV 同步数据互通

### 5.3 功能验收

- 参考 [09_acceptance_matrix.md](./09_acceptance_matrix.md)
- 每个页面必须有对应验收项
- 差异必须进入白名单

---

## 6. 开发波次

| Wave | 内容 | 预计时间 |
|------|------|----------|
| 0 | 基线采集（本文档） | 1 天 |
| 1 | 工程骨架与基础设施 | 3-5 天 |
| 2 | App 骨架页 | 2-3 天 |
| 3 | 书架与书籍管理 | 5-7 天 |
| 4 | 搜索/发现/书源 | 5-7 天 |
| 5 | 阅读器核心 | 7-10 天 |
| 6 | RSS/订阅域 | 3-5 天 |
| 7 | 替换净化/字典/字体/二维码/浏览器/视频/登录/插件 | 5-7 天 |
| 8 | 接口兼容与外部唤起 | 3-5 天 |
| 9 | 回归、比对、收尾 | 5-7 天 |

**总计**: 40-57 天