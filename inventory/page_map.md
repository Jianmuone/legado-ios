# Legado iOS Migration - Page Map

> 本文档记录 Android Legado 所有页面到 iOS 的映射关系。
> 
> **生成日期**: 2026-04-08
> **页面总数**: 75+

---

## 页面清单索引

| 目录 | 页面数 | 迁移状态 |
|------|--------|----------|
| [about](#1-about) | 3 | 待迁移 |
| [association](#2-association) | 10 | 待迁移 |
| [book/audio](#3-bookaudio) | - | 待迁移 |
| [book/bookmark](#4-bookbookmark) | 1 | 待迁移 |
| [book/cache](#5-bookcache) | - | 待迁移 |
| [book/changecover](#6-bookchangecover) | 1 | 待迁移 |
| [book/changesource](#7-bookchangesource) | 2 | 待迁移 |
| [book/explore](#8-bookexplore) | - | 待迁移 |
| [book/group](#9-bookgroup) | 3 | 待迁移 |
| [book/import](#10-bookimport) | 2 | 待迁移 |
| [book/info](#11-bookinfo) | - | 待迁移 |
| [book/manage](#12-bookmanage) | 1 | 待迁移 |
| [book/manga](#13-bookmanga) | 3 | 待迁移 |
| [book/read](#14-bookread) | 11 | 🔄 进行中 |
| [book/search](#15-booksearch) | 1 | 待迁移 |
| [book/source](#16-booksource) | 1 | 待迁移 |
| [book/toc](#17-booktoc) | 4 | 待迁移 |
| [config](#18-config) | 4 | 待迁移 |
| [dict](#19-dict) | 2 | 待迁移 |
| [file](#20-file) | 1 | 待迁移 |
| [font](#21-font) | 1 | 待迁移 |
| [login](#22-login) | 2 | 待迁移 |
| [main](#23-main) | 6 | 🔄 进行中 |
| [replace](#24-replace) | 1 | 待迁移 |
| [rss](#25-rss) | 5 | 待迁移 |
| [widget](#26-widget) | 7 | 待迁移 |

---

## 1. about

### 1.1 UpdateDialog

| 字段 | 值 |
|------|-----|
| **Android 目录** | `ui/about/` |
| **Android 文件** | `UpdateDialog.kt` |
| **Android 布局** | `dialog_update.xml` |
| **页面名称** | 更新对话框 |
| **所属业务域** | 关于 |
| **入口** | 检查更新 |
| **出口** | 更新/取消 |
| **顶部栏内容** | 标题：检查更新 |
| **底部栏内容** | 无 |
| **主体内容区域** | 更新日志、下载按钮 |
| **右上角菜单** | 无 |
| **长按菜单** | 无 |
| **弹窗** | 无 |
| **空状态** | 无 |
| **加载状态** | 进度条 |
| **错误状态** | 下载失败提示 |
| **页面持久化状态** | 无 |
| **iOS 对应** | `Features/About/UpdateDialogViewController.swift` |
| **迁移状态** | ⏳ 待迁移 |
| **差异说明** | 无 |

### 1.2 CrashLogsDialog

| 字段 | 值 |
|------|-----|
| **Android 目录** | `ui/about/` |
| **Android 文件** | `CrashLogsDialog.kt` |
| **Android 布局** | `dialog_recycler_view.xml` |
| **页面名称** | 崩溃日志对话框 |
| **所属业务域** | 关于 |
| **入口** | 设置 → 关于 → 崩溃日志 |
| **出口** | 返回 |
| **顶部栏内容** | 标题：崩溃日志 |
| **底部栏内容** | 无 |
| **主体内容区域** | RecyclerView 日志列表 |
| **右上角菜单** | 复制/分享/清空 |
| **长按菜单** | 复制/分享 |
| **弹窗** | 日志详情 |
| **空状态** | 无崩溃日志 |
| **加载状态** | 无 |
| **错误状态** | 无 |
| **页面持久化状态** | 无 |
| **iOS 对应** | `Features/About/CrashLogsViewController.swift` |
| **迁移状态** | ⏳ 待迁移 |
| **差异说明** | 无 |

### 1.3 AppLogDialog

| 字段 | 值 |
|------|-----|
| **Android 目录** | `ui/about/` |
| **Android 文件** | `AppLogDialog.kt` |
| **Android 布局** | `dialog_recycler_view.xml` |
| **页面名称** | 应用日志对话框 |
| **所属业务域** | 关于 |
| **入口** | 设置 → 关于 → 应用日志 |
| **出口** | 返回 |
| **顶部栏内容** | 标题：应用日志 |
| **底部栏内容** | 无 |
| **主体内容区域** | RecyclerView 日志列表 |
| **右上角菜单** | 复制/分享/清空 |
| **长按菜单** | 复制/分享 |
| **弹窗** | 日志详情 |
| **空状态** | 无日志 |
| **加载状态** | 无 |
| **错误状态** | 无 |
| **页面持久化状态** | 无 |
| **iOS 对应** | `Features/About/AppLogViewController.swift` |
| **迁移状态** | ⏳ 待迁移 |
| **差异说明** | 无 |

---

## 2. association

### 2.1 VerificationCodeDialog

| 字段 | 值 |
|------|-----|
| **Android 目录** | `ui/association/` |
| **Android 文件** | `VerificationCodeDialog.kt` |
| **Android 布局** | `dialog_verification_code_view.xml` |
| **页面名称** | 验证码对话框 |
| **所属业务域** | 导入 |
| **入口** | 导入需要验证的资源 |
| **出口** | 确认/取消 |
| **顶部栏内容** | 标题：验证码 |
| **底部栏内容** | 无 |
| **主体内容区域** | 验证码输入框 |
| **右上角菜单** | 无 |
| **长按菜单** | 无 |
| **弹窗** | 无 |
| **空状态** | 无 |
| **加载状态** | 无 |
| **错误状态** | 验证码错误 |
| **页面持久化状态** | 无 |
| **iOS 对应** | `Features/Association/VerificationCodeViewController.swift` |
| **迁移状态** | ⏳ 待迁移 |
| **差异说明** | 无 |

### 2.2 ImportBookSourceDialog

| 字段 | 值 |
|------|-----|
| **Android 目录** | `ui/association/` |
| **Android 文件** | `ImportBookSourceDialog.kt` |
| **Android 布局** | `dialog_recycler_view.xml` |
| **页面名称** | 导入书源对话框 |
| **所属业务域** | 导入 |
| **入口** | URL Scheme / 分享 / 文件选择 |
| **出口** | 导入/取消 |
| **顶部栏内容** | 标题：导入书源 |
| **底部栏内容** | 导入按钮 |
| **主体内容区域** | 书源列表（多选） |
| **右上角菜单** | 全选/反选 |
| **长按菜单** | 无 |
| **弹窗** | 书源详情 |
| **空状态** | 无有效书源 |
| **加载状态** | 加载中 |
| **错误状态** | 解析失败 |
| **页面持久化状态** | 无 |
| **iOS 对应** | `Features/Association/ImportBookSourceViewController.swift` |
| **迁移状态** | ⏳ 待迁移 |
| **差异说明** | 无 |

### 2.3 AddToBookshelfDialog

| 字段 | 值 |
|------|-----|
| **Android 目录** | `ui/association/` |
| **Android 文件** | `AddToBookshelfDialog.kt` |
| **Android 布局** | `dialog_add_to_bookshelf.xml` |
| **页面名称** | 添加到书架对话框 |
| **所属业务域** | 导入 |
| **入口** | URL Scheme `legado://import/addToBookshelf` |
| **出口** | 添加/取消 |
| **顶部栏内容** | 标题：添加到书架 |
| **底部栏内容** | 添加按钮 |
| **主体内容区域** | 书籍信息预览 |
| **右上角菜单** | 无 |
| **长按菜单** | 无 |
| **弹窗** | 无 |
| **空状态** | 无 |
| **加载状态** | 加载中 |
| **错误状态** | 添加失败 |
| **页面持久化状态** | 无 |
| **iOS 对应** | `Features/Association/AddToBookshelfViewController.swift` |
| **迁移状态** | ⏳ 待迁移 |
| **差异说明** | 无 |

---

## 14. book/read

### 14.1 ReadBookActivity (核心阅读页)

| 字段 | 值 |
|------|-----|
| **Android 目录** | `ui/book/read/` |
| **Android 文件** | `ReadBookActivity.kt` |
| **Android 布局** | `activity_read_book.xml` |
| **页面名称** | 阅读页 |
| **所属业务域** | 阅读器核心 |
| **入口** | 书架点击书籍 / 目录点击章节 |
| **出口** | 返回键 / 菜单退出 |
| **顶部栏内容** | 书名、返回、菜单 |
| **底部栏内容** | 上一章/下一章、目录、设置 |
| **主体内容区域** | 正文页面（TextSwitcher/PageView） |
| **右上角菜单** | 目录、换源、朗读、更多 |
| **长按菜单** | 复制、搜索、替换 |
| **弹窗** | 阅读设置、字体、主题 |
| **空状态** | 无章节 |
| **加载状态** | 加载动画 |
| **错误状态** | 章节加载失败 |
| **页面持久化状态** | 阅读进度、亮度、设置 |
| **iOS 对应** | `Features/Reader/ReaderViewController.swift` |
| **迁移状态** | 🔄 进行中 |
| **差异说明** | 无 |

### 14.2 ReadStyleDialog

| 字段 | 值 |
|------|-----|
| **Android 目录** | `ui/book/read/config/` |
| **Android 文件** | `ReadStyleDialog.kt` |
| **Android 布局** | `dialog_read_book_style.xml` |
| **页面名称** | 阅读样式配置 |
| **所属业务域** | 阅读器核心 |
| **入口** | 阅读页 → 设置 |
| **出口** | 确定/取消 |
| **顶部栏内容** | 标题：阅读样式 |
| **底部栏内容** | 无 |
| **主体内容区域** | 字体、字号、行距、边距配置 |
| **右上角菜单** | 重置 |
| **长按菜单** | 无 |
| **弹窗** | 字体选择、主题选择 |
| **空状态** | 无 |
| **加载状态** | 无 |
| **错误状态** | 无 |
| **页面持久化状态** | 配置项 |
| **iOS 对应** | `Features/Reader/Config/ReadStyleViewController.swift` |
| **迁移状态** | ⏳ 待迁移 |
| **差异说明** | 无 |

### 14.3 ReadAloudDialog

| 字段 | 值 |
|------|-----|
| **Android 目录** | `ui/book/read/config/` |
| **Android 文件** | `ReadAloudDialog.kt` |
| **Android 布局** | `dialog_read_aloud.xml` |
| **页面名称** | 朗读配置 |
| **所属业务域** | 阅读器核心 |
| **入口** | 阅读页 → 朗读 |
| **出口** | 关闭 |
| **顶部栏内容** | 标题：朗读设置 |
| **底部栏内容** | 播放控制 |
| **主体内容区域** | TTS 引擎选择、语速、音调 |
| **右上角菜单** | 无 |
| **长按菜单** | 无 |
| **弹窗** | HTTP TTS 编辑 |
| **空状态** | 无 TTS 引擎 |
| **加载状态** | 无 |
| **错误状态** | 无 |
| **页面持久化状态** | TTS 配置 |
| **iOS 对应** | `Features/Reader/Config/ReadAloudViewController.swift` |
| **迁移状态** | ⏳ 待迁移 |
| **差异说明** | 无 |

---

## 23. main

### 23.1 MainActivity

| 字段 | 值 |
|------|-----|
| **Android 目录** | `ui/main/` |
| **Android 文件** | `MainActivity.kt` |
| **Android 布局** | `activity_main.xml` |
| **页面名称** | 主界面 |
| **所属业务域** | 主界面 |
| **入口** | 应用启动 |
| **出口** | 返回键退出 |
| **顶部栏内容** | 标题、搜索、菜单 |
| **底部栏内容** | TabBar（书架、发现、RSS、我的） |
| **主体内容区域** | Fragment 容器 |
| **右上角菜单** | 搜索、设置 |
| **长按菜单** | 无 |
| **弹窗** | 无 |
| **空状态** | 无 |
| **加载状态** | 启动画面 |
| **错误状态** | 无 |
| **页面持久化状态** | 当前 Tab |
| **iOS 对应** | `Features/Main/MainTabBarController.swift` |
| **迁移状态** | 🔄 进行中 |
| **差异说明** | 无 |

### 23.2 BookshelfFragment1

| 字段 | 值 |
|------|-----|
| **Android 目录** | `ui/main/bookshelf/style1/` |
| **Android 文件** | `BookshelfFragment1.kt` |
| **Android 布局** | `fragment_bookshelf1.xml` |
| **页面名称** | 书架（列表样式） |
| **所属业务域** | 主界面 |
| **入口** | 主界面 → 书架 Tab |
| **出口** | 切换 Tab |
| **顶部栏内容** | 书架标题、搜索、菜单 |
| **底部栏内容** | 无 |
| **主体内容区域** | RecyclerView 书籍列表 |
| **右上角菜单** | 搜索、整理、设置 |
| **长按菜单** | 编辑、删除、分组 |
| **弹窗** | 书籍详情、分组选择 |
| **空状态** | 空书架提示 |
| **加载状态** | 加载中 |
| **错误状态** | 无 |
| **页面持久化状态** | 滚动位置、显示模式 |
| **iOS 对应** | `Features/Bookshelf/BookshelfListViewController.swift` |
| **迁移状态** | ⏳ 待迁移 |
| **差异说明** | 无 |

### 23.3 BookshelfFragment2

| 字段 | 值 |
|------|-----|
| **Android 目录** | `ui/main/bookshelf/style2/` |
| **Android 文件** | `BookshelfFragment2.kt` |
| **Android 布局** | `fragment_bookshelf2.xml` |
| **页面名称** | 书架（网格样式） |
| **所属业务域** | 主界面 |
| **入口** | 主界面 → 书架 Tab |
| **出口** | 切换 Tab |
| **顶部栏内容** | 书架标题、搜索、菜单 |
| **底部栏内容** | 无 |
| **主体内容区域** | RecyclerView 书籍网格 |
| **右上角菜单** | 搜索、整理、设置 |
| **长按菜单** | 编辑、删除、分组 |
| **弹窗** | 书籍详情、分组选择 |
| **空状态** | 空书架提示 |
| **加载状态** | 加载中 |
| **错误状态** | 无 |
| **页面持久化状态** | 滚动位置、显示模式 |
| **iOS 对应** | `Features/Bookshelf/BookshelfGridViewController.swift` |
| **迁移状态** | ⏳ 待迁移 |
| **差异说明** | 无 |

### 23.4 ExploreFragment

| 字段 | 值 |
|------|-----|
| **Android 目录** | `ui/main/explore/` |
| **Android 文件** | `ExploreFragment.kt` |
| **Android 布局** | `fragment_explore.xml` |
| **页面名称** | 发现页 |
| **所属业务域** | 主界面 |
| **入口** | 主界面 → 发现 Tab |
| **出口** | 切换 Tab |
| **顶部栏内容** | 发现标题、搜索 |
| **底部栏内容** | 无 |
| **主体内容区域** | 发现源列表 |
| **右上角菜单** | 书源管理 |
| **长按菜单** | 编辑书源 |
| **弹窗** | 书源详情 |
| **空状态** | 无发现源 |
| **加载状态** | 加载中 |
| **错误状态** | 无 |
| **页面持久化状态** | 滚动位置 |
| **iOS 对应** | `Features/Explore/ExploreViewController.swift` |
| **迁移状态** | ⏳ 待迁移 |
| **差异说明** | 无 |

### 23.5 RssFragment

| 字段 | 值 |
|------|-----|
| **Android 目录** | `ui/main/rss/` |
| **Android 文件** | `RssFragment.kt` |
| **Android 布局** | `fragment_rss.xml` |
| **页面名称** | RSS 订阅 |
| **所属业务域** | 主界面 |
| **入口** | 主界面 → RSS Tab |
| **出口** | 切换 Tab |
| **顶部栏内容** | RSS 标题、搜索 |
| **底部栏内容** | 无 |
| **主体内容区域** | 订阅源列表 |
| **右上角菜单** | 订阅源管理 |
| **长按菜单** | 编辑订阅源 |
| **弹窗** | 订阅源详情 |
| **空状态** | 无订阅源 |
| **加载状态** | 加载中 |
| **错误状态** | 无 |
| **页面持久化状态** | 滚动位置 |
| **iOS 对应** | `Features/RSS/RssViewController.swift` |
| **迁移状态** | ⏳ 待迁移 |
| **差异说明** | 无 |

### 23.6 MyFragment

| 字段 | 值 |
|------|-----|
| **Android 目录** | `ui/main/my/` |
| **Android 文件** | `MyFragment.kt` |
| **Android 布局** | `fragment_my_config.xml` |
| **页面名称** | 我的 |
| **所属业务域** | 主界面 |
| **入口** | 主界面 → 我的 Tab |
| **出口** | 切换 Tab |
| **顶部栏内容** | 我的标题 |
| **底部栏内容** | 无 |
| **主体内容区域** | 设置入口列表 |
| **右上角菜单** | 无 |
| **长按菜单** | 无 |
| **弹窗** | 无 |
| **空状态** | 无 |
| **加载状态** | 无 |
| **错误状态** | 无 |
| **页面持久化状态** | 无 |
| **iOS 对应** | `Features/My/MyViewController.swift` |
| **迁移状态** | ⏳ 待迁移 |
| **差异说明** | 无 |

---

## 统计

| 状态 | 数量 |
|------|------|
| ✅ 已完成 | 5 |
| 🔄 进行中 | 3 |
| ⏳ 待迁移 | 67+ |

---

*本文档由 Wave 0 基线采集自动生成*