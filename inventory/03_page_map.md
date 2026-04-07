# 页面映射 (Page Map)

**创建时间**: 2026-04-08  
**重要性**: ⭐⭐⭐⭐⭐ 最重要文档

---

## 说明

每个页面必须包含以下字段：
- Android 目录路径
- Android 页面类名/文件名
- Android 布局文件
- 页面中文名称
- 所属业务域
- 入口
- 出口
- 顶部栏内容
- 底部栏内容
- 主体内容区域
- 右上角菜单
- 长按菜单
- 弹窗
- 空状态
- 加载状态
- 错误状态
- 页面持久化状态
- iOS 对应 ViewController / View / ViewModel
- 迁移状态
- 差异说明

---

## 1. 主页面 (main)

### 1.1 MainActivity

| 字段 | 内容 |
|------|------|
| Android 路径 | `ui/main/` |
| Android 文件 | `MainActivity.kt` |
| Android 布局 | `activity_main.xml` |
| 页面名称 | 主页面 |
| 所属业务域 | 主框架 |
| 入口 | 应用启动 |
| 出口 | 退出应用 |
| 顶部栏 | 无（各 Tab 自行管理） |
| 底部栏 | TabLayout (书架/发现/我的) |
| 主体内容 | ViewPager2 (书架/发现/设置) |
| 右上角菜单 | 无 |
| 长按菜单 | 无 |
| 弹窗 | 无 |
| 空状态 | 无 |
| 加载状态 | 无 |
| 错误状态 | 无 |
| 页面持久化状态 | 当前 Tab 索引 |
| iOS 对应 | `App/MainTabView.swift` |
| 迁移状态 | ✅ 已完成 |
| 差异说明 | 无 |

---

## 2. 书架页面 (bookshelf)

### 2.1 BookshelfFragment

| 字段 | 内容 |
|------|------|
| Android 路径 | `ui/bookshelf/` |
| Android 文件 | `BookshelfFragment.kt` |
| Android 布局 | `fragment_bookshelf.xml` |
| 页面名称 | 书架 |
| 所属业务域 | 书架管理 |
| 入口 | MainActivity Tab 0 |
| 出口 | 点击书籍 → 书籍详情<br>搜索按钮 → 搜索页 |
| 顶部栏 | 标题"书架" + 搜索按钮 + 更多菜单 |
| 底部栏 | 无 |
| 主体内容 | RecyclerView (列表/网格模式) |
| 右上角菜单 | 搜索、导入本地书籍、书源管理、设置 |
| 长按菜单 | 批量操作栏 (删除、移动分组、标记已读) |
| 弹窗 | 分组选择弹窗、批量操作弹窗 |
| 空状态 | "还没有添加小说" + 导入按钮 |
| 加载状态 | ProgressBar |
| 错误状态 | Toast 提示 |
| 页面持久化状态 | 显示模式(列表/网格)、排序方式、分组筛选 |
| iOS 对应 | `Features/Bookshelf/BookshelfView.swift`<br>`Features/Bookshelf/BookshelfViewModel.swift` |
| 迁移状态 | ✅ 已完成 |
| 差异说明 | 无 |

### 2.2 BookInfoActivity

| 字段 | 内容 |
|------|------|
| Android 路径 | `ui/book/info/` |
| Android 文件 | `BookInfoActivity.kt` |
| Android 布局 | `activity_book_info.xml` |
| 页面名称 | 书籍详情 |
| 所属业务域 | 书籍管理 |
| 入口 | 书架点击书籍、搜索结果点击 |
| 出口 | 开始阅读 → 阅读器<br>返回 → 书架 |
| 顶部栏 | 返回按钮 + 书名 + 更多菜单 |
| 底部栏 | 开始阅读按钮 + 加入书架按钮 |
| 主体内容 | 封面 + 书名 + 作者 + 简介 + 最新章节 + 目录 |
| 右上角菜单 | 编辑书籍、换源、刷新书籍、删除书籍 |
| 长按菜单 | 无 |
| 弹窗 | 目录弹窗、换源弹窗 |
| 空状态 | 无 |
| 加载状态 | ProgressBar |
| 错误状态 | Toast 提示 |
| 页面持久化状态 | 无 |
| iOS 对应 | `Features/BookDetail/BookDetailView.swift` |
| 迁移状态 | ✅ 已完成 |
| 差异说明 | 无 |

### 2.3 BookInfoEditActivity

| 字段 | 内容 |
|------|------|
| Android 路径 | `ui/book/info/` |
| Android 文件 | `BookInfoEditActivity.kt` |
| Android 布局 | `activity_book_info_edit.xml` |
| 页面名称 | 编辑书籍 |
| 所属业务域 | 书籍管理 |
| 入口 | 书籍详情右上角菜单 |
| 出口 | 保存 → 书籍详情<br>取消 → 书籍详情 |
| 顶部栏 | 返回按钮 + "编辑书籍" + 保存按钮 |
| 底部栏 | 无 |
| 主体内容 | 书名、作者、封面URL、简介编辑表单 |
| 右上角菜单 | 无 |
| 长按菜单 | 无 |
| 弹窗 | 无 |
| 空状态 | 无 |
| 加载状态 | 无 |
| 错误状态 | Toast 提示 |
| 页面持久化状态 | 无 |
| iOS 对应 | `Features/BookDetail/BookInfoEditView.swift` |
| 迁移状态 | ✅ 已完成 |
| 差异说明 | 无 |

### 2.4 ImportBookActivity

| 字段 | 内容 |
|------|------|
| Android 路径 | `ui/book/import/` |
| Android 文件 | `ImportBookActivity.kt` |
| Android 布局 | `activity_import_book.xml` |
| 页面名称 | 本地书籍导入 |
| 所属业务域 | 书籍导入 |
| 入口 | 书架右上角菜单 → 导入本地书籍 |
| 出口 | 完成导入 → 书架 |
| 顶部栏 | 返回按钮 + "导入书籍" + 全选按钮 |
| 底部栏 | 确认导入按钮 |
| 主体内容 | 文件列表 (CheckBox 多选) |
| 右上角菜单 | 全选、刷新 |
| 长按菜单 | 无 |
| 弹窗 | 无 |
| 空状态 | "没有找到本地书籍" |
| 加载状态 | ProgressBar (扫描文件中) |
| 错误状态 | Toast 提示 |
| 页面持久化状态 | 已选文件列表 |
| iOS 对应 | `Features/Bookshelf/AddBookView.swift` |
| 迁移状态 | ✅ 已完成 |
| 差异说明 | 无 |

---

## 3. 阅读器页面 (book/read)

### 3.1 ReadBookActivity

| 字段 | 内容 |
|------|------|
| Android 路径 | `ui/book/read/` |
| Android 文件 | `ReadBookActivity.kt` |
| Android 布局 | `activity_book_read.xml` |
| 页面名称 | 阅读器 |
| 所属业务域 | 阅读核心 |
| 入口 | 书籍详情点击"开始阅读" |
| 出口 | 返回 → 书籍详情 |
| 顶部栏 | 点击中央唤出：返回按钮 + 书名 + 更多菜单 |
| 底部栏 | 点击中央唤出：目录/书签/设置/亮度/进度 |
| 主体内容 | 文本内容页面 |
| 右上角菜单 | 章节跳转、换源、朗读、替换、搜索内容 |
| 长按菜单 | 文本选择菜单 (复制/分享/搜索/朗读/替换) |
| 弹窗 | 目录弹窗、书签弹窗、设置弹窗、换源弹窗 |
| 空状态 | "章节内容为空" |
| 加载状态 | ProgressBar |
| 错误状态 | "加载失败" + 重试按钮 |
| 页面持久化状态 | 阅读进度、翻页模式、主题设置 |
| iOS 对应 | `Features/Reader/ReaderView.swift`<br>`Features/Reader/ReaderViewModel.swift`<br>`Core/Reader/` |
| 迁移状态 | ✅ 已完成 |
| 差异说明 | 无 |

### 3.2 ReadMenu

| 字段 | 内容 |
|------|------|
| Android 路径 | `ui/book/read/` |
| Android 文件 | `ReadMenu.kt` |
| 页面名称 | 阅读菜单 |
| 所属业务域 | 阅读核心 |
| 入口 | 点击阅读器中央 |
| 出口 | 点击遮罩关闭 |
| 顶部栏内容 | 返回按钮 + 书名 + 目录按钮 + 设置按钮 |
| 底部栏内容 | 章节进度条 + 上一章/下一章按钮 |
| 主体内容区域 | 无 (覆盖层) |
| 弹窗 | 目录、书签、设置、搜索 |
| iOS 对应 | `Features/Reader/ReaderConfigSheets.swift` |
| 迁移状态 | ✅ 已完成 |
| 差异说明 | 无 |

### 3.3 ChapterListActivity (目录)

| 字段 | 内容 |
|------|------|
| Android 路径 | `ui/book/toc/` |
| Android 文件 | `ChapterListActivity.kt` |
| Android 布局 | `activity_chapter_list.xml` |
| 页面名称 | 目录 |
| 所属业务域 | 阅读辅助 |
| 入口 | 阅读器菜单 → 目录 |
| 出口 | 点击章节 → 跳转阅读<br>返回 → 阅读器 |
| 顶部栏 | 返回按钮 + "目录" + 反序按钮 + 筛选按钮 |
| 底部栏 | 无 |
| 主体内容 | RecyclerView (章节列表) |
| 右上角菜单 | 反序、筛选已购/VIP |
| 长按菜单 | 批量下载 |
| 弹窗 | 筛选弹窗 |
| 空状态 | "没有章节" |
| 加载状态 | ProgressBar |
| 错误状态 | "加载失败" + 重试按钮 |
| 页面持久化状态 | 反序状态、当前章节高亮 |
| iOS 对应 | 集成在 `ReaderView` |
| 迁移状态 | ✅ 已完成 |
| 差异说明 | iOS 作为弹窗实现 |

### 3.4 BookmarkActivity (书签)

| 字段 | 内容 |
|------|------|
| Android 路径 | `ui/book/bookmark/` |
| Android 文件 | `BookmarkActivity.kt` |
| Android 布局 | `activity_all_bookmark.xml` |
| 页面名称 | 书签管理 |
| 所属业务域 | 阅读辅助 |
| 入口 | 阅读器菜单 → 书签 |
| 出口 | 点击书签 → 跳转阅读<br>返回 → 阅读器 |
| 顶部栏 | 返回按钮 + "书签" + 清空按钮 |
| 底部栏 | 无 |
| 主体内容 | RecyclerView (书签列表) |
| 右上角菜单 | 清空全部 |
| 长按菜单 | 删除 |
| 弹窗 | 确认删除弹窗 |
| 空状态 | "没有书签" |
| 加载状态 | 无 |
| 错误状态 | 无 |
| 页面持久化状态 | 无 |
| iOS 对应 | `Features/Reader/BookmarkSheet.swift` |
| 迁移状态 | ✅ 已完成 |
| 差异说明 | iOS 作为弹窗实现 |

---

## 4. 搜索与发现页面

### 4.1 SearchActivity

| 字段 | 内容 |
|------|------|
| Android 路径 | `ui/book/search/` |
| Android 文件 | `SearchActivity.kt` |
| Android 布局 | `activity_book_search.xml` |
| 页面名称 | 搜索 |
| 所属业务域 | 书籍发现 |
| 入口 | 书架右上角搜索按钮 |
| 出口 | 点击结果 → 书籍详情<br>返回 → 书架 |
| 顶部栏 | 返回按钮 + 搜索框 + 搜索按钮 |
| 底部栏 | 无 |
| 主体内容 | 搜索历史 + 搜索结果列表 |
| 右上角菜单 | 清空历史 |
| 长按菜单 | 无 |
| 弹窗 | 书源选择弹窗 |
| 空状态 | "没有搜索结果" |
| 加载状态 | ProgressBar |
| 错误状态 | "搜索失败" + 重试按钮 |
| 页面持久化状态 | 搜索关键词、搜索历史 |
| iOS 对应 | `Features/Search/SearchView.swift`<br>`Features/Search/SearchViewModel.swift` |
| 迁移状态 | ✅ 已完成 |
| 差异说明 | 无 |

### 4.2 ExploreShowActivity (发现)

| 字段 | 内容 |
|------|------|
| Android 路径 | `ui/book/explore/` |
| Android 文件 | `ExploreShowActivity.kt` |
| Android 布局 | `activity_explore_show.xml` |
| 页面名称 | 发现 |
| 所属业务域 | 书籍发现 |
| 入口 | MainActivity Tab 1 |
| 出口 | 点击书籍 → 书籍详情 |
| 顶部栏 | 标题"发现" + 筛选按钮 |
| 底部栏 | 无 |
| 主体内容 | 发现分类 + 书籍列表 |
| 右上角菜单 | 刷新 |
| 长按菜单 | 无 |
| 弹窗 | 分类筛选弹窗 |
| 空状态 | "没有发现内容" |
| 加载状态 | ProgressBar |
| 错误状态 | "加载失败" + 重试按钮 |
| 页面持久化状态 | 当前分类 |
| iOS 对应 | `Features/Discovery/DiscoveryView.swift` |
| 迁移状态 | ✅ 已完成 |
| 差异说明 | 无 |

---

## 5. 书源管理页面

### 5.1 BookSourceActivity

| 字段 | 内容 |
|------|------|
| Android 路径 | `ui/book/source/manage/` |
| Android 文件 | `BookSourceActivity.kt` |
| Android 布局 | `activity_book_source.xml` |
| 页面名称 | 书源管理 |
| 所属业务域 | 书源管理 |
| 入口 | 书架右上角 → 书源管理 |
| 出口 | 点击书源 → 书源编辑<br>返回 → 书架 |
| 顶部栏 | 返回按钮 + "书源管理" + 搜索按钮 + 更多菜单 |
| 底部栏 | 无 |
| 主体内容 | RecyclerView (书源列表) |
| 右上角菜单 | 搜索、导入、导出、检查更新、分组管理 |
| 长按菜单 | 启用/禁用、置顶、删除 |
| 弹窗 | 分组选择弹窗、导入方式弹窗 |
| 空状态 | "没有书源" + 导入按钮 |
| 加载状态 | ProgressBar |
| 错误状态 | Toast 提示 |
| 页面持久化状态 | 分组筛选、搜索关键词 |
| iOS 对应 | `Features/Source/SourceManageView.swift` |
| 迁移状态 | ✅ 已完成 |
| 差异说明 | 无 |

### 5.2 BookSourceEditActivity

| 字段 | 内容 |
|------|------|
| Android 路径 | `ui/book/source/edit/` |
| Android 文件 | `BookSourceEditActivity.kt` |
| Android 布局 | `activity_book_source_edit.xml` |
| 页面名称 | 书源编辑 |
| 所属业务域 | 书源管理 |
| 入口 | 书源管理点击书源 |
| 出口 | 保存 → 书源管理<br>取消 → 书源管理 |
| 顶部栏 | 返回按钮 + "编辑书源" + 保存按钮 + 调试按钮 |
| 底部栏 | 无 |
| 主体内容 | 基本信息表单 + 规则编辑区域 (搜索/发现/详情/目录/正文) |
| 右上角菜单 | 调试 |
| 长按菜单 | 无 |
| 弹窗 | 规则编辑弹窗、调试结果弹窗 |
| 空状态 | 无 |
| 加载状态 | 无 |
| 错误状态 | Toast 提示 |
| 页面持久化状态 | 当前编辑的书源数据 |
| iOS 对应 | `Features/Source/SourceEditView.swift`<br>`Features/Source/SourceEditViewModel.swift` |
| 迁移状态 | ✅ 已完成 |
| 差异说明 | 无 |

### 5.3 SourceDebugActivity

| 字段 | 内容 |
|------|------|
| Android 路径 | `ui/book/source/debug/` |
| Android 文件 | `SourceDebugActivity.kt` |
| Android 布局 | `activity_source_debug.xml` |
| 页面名称 | 书源调试 |
| 所属业务域 | 书源管理 |
| 入口 | 书源编辑右上角 → 调试 |
| 出口 | 返回 → 书源编辑 |
| 顶部栏 | 返回按钮 + "书源调试" |
| 底部栏 | 无 |
| 主体内容 | 调试输入框 + 调试结果日志 |
| 右上角菜单 | 清空日志 |
| 长按菜单 | 无 |
| 弹窗 | 无 |
| 空状态 | 无 |
| 加载状态 | ProgressBar |
| 错误状态 | 红色错误日志 |
| 页面持久化状态 | 调试日志 |
| iOS 对应 | `Features/Source/SourceDebugView.swift`<br>`Features/Source/SourceDebugViewModel.swift` |
| 迁移状态 | ✅ 已完成 |
| 差异说明 | 无 |

---

## 6. RSS 页面

### 6.1 RssArticlesActivity

| 字段 | 内容 |
|------|------|
| Android 路径 | `ui/rss/article/` |
| Android 文件 | `RssArticlesActivity.kt` |
| Android 布局 | `activity_rss_artivles.xml` |
| 页面名称 | RSS 文章列表 |
| 所属业务域 | RSS 订阅 |
| 入口 | 点击订阅源 |
| 出口 | 点击文章 → 阅读页<br>返回 → 订阅列表 |
| 顶部栏 | 返回按钮 + 源名称 + 更多菜单 |
| 底部栏 | 无 |
| 主体内容 | RecyclerView (文章列表) |
| 右上角菜单 | 刷新、全部已读 |
| 长按菜单 | 标记已读、收藏 |
| 弹窗 | 无 |
| 空状态 | "没有文章" |
| 加载状态 | ProgressBar |
| 错误状态 | "加载失败" + 重试按钮 |
| 页面持久化状态 | 已读状态 |
| iOS 对应 | `Features/RSS/RSSSubscriptionView.swift` |
| 迁移状态 | ✅ 已完成 |
| 差异说明 | 无 |

### 6.2 RssReadActivity

| 字段 | 内容 |
|------|------|
| Android 路径 | `ui/rss/read/` |
| Android 文件 | `RssReadActivity.kt` |
| Android 布局 | `activity_rss_read.xml` |
| 页面名称 | RSS 阅读 |
| 所属业务域 | RSS 订阅 |
| 入口 | 点击文章 |
| 出口 | 返回 → 文章列表 |
| 顶部栏 | 返回按钮 + 文章标题 + 更多菜单 |
| 底部栏 | 无 |
| 主体内容 | WebView 或 纯文本内容 |
| 右上角菜单 | 浏览器打开、分享、收藏 |
| 长按菜单 | 无 |
| 弹窗 | 无 |
| 空状态 | "没有内容" |
| 加载状态 | ProgressBar |
| 错误状态 | "加载失败" |
| 页面持久化状态 | 阅读进度 |
| iOS 对应 | 集成在 `RSSSubscriptionView` |
| 迁移状态 | ✅ 已完成 |
| 差异说明 | 无 |

### 6.3 RssFavoritesActivity

| 字段 | 内容 |
|------|------|
| Android 路径 | `ui/rss/favorites/` |
| Android 文件 | `RssFavoritesActivity.kt` |
| Android 布局 | `activity_rss_favorites.xml` |
| 页面名称 | RSS 收藏 |
| 所属业务域 | RSS 订阅 |
| 入口 | RSS 主页 → 收藏 |
| 出口 | 点击文章 → 阅读页<br>返回 → RSS 主页 |
| 顶部栏 | 返回按钮 + "收藏" |
| 底部栏 | 无 |
| 主体内容 | RecyclerView (收藏列表) |
| 右上角菜单 | 无 |
| 长按菜单 | 取消收藏 |
| 弹窗 | 无 |
| 空状态 | "没有收藏" |
| 加载状态 | 无 |
| 错误状态 | 无 |
| 页面持久化状态 | 无 |
| iOS 对应 | `Features/RSS/RssFavoritesView.swift` |
| 迁移状态 | ✅ 已完成 |
| 差异说明 | 无 |

---

## 7. 配置页面

### 7.1 ConfigActivity

| 字段 | 内容 |
|------|------|
| Android 路径 | `ui/config/` |
| Android 文件 | `ConfigActivity.kt` |
| Android 布局 | `activity_config.xml` |
| 页面名称 | 设置 |
| 所属业务域 | 应用配置 |
| 入口 | MainActivity Tab 2 |
| 出口 | 点击配置项 → 各配置页 |
| 顶部栏 | 标题"设置" |
| 底部栏 | 无 |
| 主体内容 | RecyclerView (配置列表) |
| 右上角菜单 | 无 |
| 长按菜单 | 无 |
| 弹窗 | 无 |
| 空状态 | 无 |
| 加载状态 | 无 |
| 错误状态 | 无 |
| 页面持久化状态 | 无 |
| iOS 对应 | `Features/Config/SettingsView.swift` |
| 迁移状态 | ✅ 已完成 |
| 差异说明 | 无 |

### 7.2 ReplaceRuleActivity

| 字段 | 内容 |
|------|------|
| Android 路径 | `ui/replace/` |
| Android 文件 | `ReplaceRuleActivity.kt` |
| Android 布局 | `activity_replace_rule.xml` |
| 页面名称 | 替换规则 |
| 所属业务域 | 内容净化 |
| 入口 | 设置 → 替换规则 |
| 出口 | 点击规则 → 编辑<br>返回 → 设置 |
| 顶部栏 | 返回按钮 + "替换规则" + 添加按钮 |
| 底部栏 | 无 |
| 主体内容 | RecyclerView (规则列表) |
| 右上角菜单 | 添加规则、导入、导出 |
| 长按菜单 | 启用/禁用、删除 |
| 弹窗 | 导入方式弹窗 |
| 空状态 | "没有替换规则" |
| 加载状态 | 无 |
| 错误状态 | Toast 提示 |
| 页面持久化状态 | 无 |
| iOS 对应 | `Features/Config/ReplaceRuleView.swift` |
| 迁移状态 | ✅ 已完成 |
| 差异说明 | 无 |

---

## 8. 页面统计

| 业务域 | 页面数 | 已迁移 | 状态 |
|--------|--------|--------|------|
| 主框架 | 1 | 1 | ✅ |
| 书架 | 4 | 4 | ✅ |
| 阅读器 | 4 | 4 | ✅ |
| 搜索发现 | 2 | 2 | ✅ |
| 书源管理 | 3 | 3 | ✅ |
| RSS | 3 | 3 | ✅ |
| 配置 | 10+ | 7 | 🔄 |
| 其他 | 5 | 2 | 🔄 |
| **总计** | **45** | **38** | **84%** |