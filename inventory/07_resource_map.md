# 资源映射 (Resource Map)

**创建时间**: 2026-04-08  
**状态**: 🔄 进行中

---

## 1. 布局文件映射

### 1.1 主要布局文件

| Android 布局 | 功能 | iOS 对应 | 状态 |
|--------------|------|----------|------|
| `activity_main.xml` | 主页面 | `MainTabView.swift` | ✅ |
| `activity_book_read.xml` | 阅读器 | `ReaderView.swift` | ✅ |
| `activity_book_info.xml` | 书籍详情 | `BookDetailView.swift` | ✅ |
| `activity_book_source.xml` | 书源管理 | `SourceManageView.swift` | ✅ |
| `activity_book_search.xml` | 搜索页 | `SearchView.swift` | ✅ |
| `activity_rss_artivles.xml` | RSS 列表 | `RSSSubscriptionView.swift` | ✅ |
| `activity_config.xml` | 设置页 | `SettingsView.swift` | ✅ |
| `activity_replace_rule.xml` | 替换规则 | `ReplaceRuleView.swift` | ✅ |

### 1.2 弹窗布局

| Android 布局 | 功能 | iOS 对应 | 状态 |
|--------------|------|----------|------|
| `dialog_bookmark.xml` | 书签弹窗 | `BookmarkSheet.swift` | ✅ |
| `dialog_book_change_source.xml` | 换源弹窗 | `ChangeSourceSheet.swift` | ✅ |
| `dialog_book_group_picker.xml` | 分组选择 | 集成在 GroupManageView | ✅ |
| `dialog_auto_read.xml` | 自动朗读 | `TTSControlsView.swift` | ✅ |
| `dialog_bookshelf_config.xml` | 书架配置 | 集成在 BookshelfView | ✅ |

---

## 2. 多语言资源映射

### 2.1 支持的语言

| Android values | 语言 | iOS 对应 | 状态 |
|----------------|------|----------|------|
| `values/` | 英文 | `en.lproj/Localizable.strings` | ✅ |
| `values-zh/` | 简体中文 | `zh-Hans.lproj/Localizable.strings` | ✅ |
| `values-zh-rTW/` | 繁体中文 | `zh-Hant.lproj/Localizable.strings` | ✅ |
| `values-zh-rHK/` | 粤语 | ❌ | ❌ |
| `values-es-rES/` | 西班牙语 | ❌ | ❌ |
| `values-ja-rJP/` | 日语 | ❌ | ❌ |
| `values-pt-rBR/` | 葡萄牙语 | ❌ | ❌ |
| `values-vi/` | 越南语 | ❌ | ❌ |

### 2.2 字符串提取原则

- 从 Android `values-zh/strings.xml` 提取所有中文文案
- 保持文案语义一致
- 禁止擅自修改文案

---

## 3. 主题与样式资源

### 3.1 夜间模式

| Android | iOS | 状态 |
|---------|-----|------|
| `values-night/` | ThemeManager.darkMode | ✅ |
| 颜色资源自动切换 | Color Assets | ✅ |

### 3.2 主题配置

| 主题类型 | Android 实现 | iOS 实现 | 状态 |
|----------|--------------|----------|------|
| 亮色主题 | 默认 | ThemeManager.light | ✅ |
| 暗色主题 | values-night | ThemeManager.dark | ✅ |
| 羊皮纸 | 自定义 | ThemeManager.sepia | ✅ |
| 护眼 | 自定义 | ThemeManager.eyeProtection | ✅ |
| 自定义 | 用户选择 | 需要实现 | ❌ |

---

## 4. 横屏布局映射

### 4.1 横屏布局文件

| Android 布局 | 功能 | iOS 对应 | 状态 |
|--------------|------|----------|------|
| `layout-land/activity_book_read.xml` | 阅读器横屏 | 需要单独适配 | 🔄 |
| `layout-land/activity_book_info.xml` | 书籍详情横屏 | 需要单独适配 | 🔄 |

### 4.2 iOS 横屏适配

- 使用 Size Classes 自动适配
- 部分页面需要单独横屏布局
- 必须验证横屏效果与 Android 一致

---

## 5. 图片资源映射

### 5.1 图标资源

| Android | iOS | 状态 |
|---------|-----|------|
| `mipmap-*/ic_launcher.png` | `Assets.xcassets/AppIcon.appiconset/` | ✅ |
| `drawable-*/ic_*.xml` | SF Symbols 或自定义图标 | 🔄 |

### 5.2 书籍封面

- 默认封面占位图
- 封面缓存机制
- 封面加载失败处理

---

## 6. 动画资源映射

### 6.1 翻页动画

| Android | iOS | 状态 |
|---------|-----|------|
| 仿真翻页 | CurlPageView | ✅ |
| 覆盖翻页 | CoverPageView | ✅ |
| 滑动翻页 | SlidePageView | ✅ |
| 滚动 | PagedReaderView (scroll mode) | ✅ |
| 无动画 | 无动画模式 | ✅ |

### 6.2 页面转场动画

- 使用 SwiftUI 默认转场
- 与 Android 转场效果对比验证

---

## 7. 资源文件清单

### 7.1 Android 资源目录

```
app/src/main/res/
├── anim/              # 补间动画
├── animator/          # 属性动画
├── drawable/          # 图片/矢量图
├── layout/            # 布局文件
├── layout-land/       # 横屏布局
├── menu/              # 菜单文件
├── mipmap-*/          # 应用图标
├── raw/               # 原始文件
├── values/            # 默认值
├── values-night/      # 夜间模式
├── values-zh/         # 简体中文
├── values-zh-rTW/     # 繁体中文
├── values-zh-rHK/     # 粤语
├── values-es-rES/     # 西班牙语
├── values-ja-rJP/     # 日语
├── values-pt-rBR/     # 葡萄牙语
├── values-vi/         # 越南语
└── xml/               # XML 配置
```

### 7.2 iOS 资源目录

```
Resources/
├── Assets.xcassets/           # 图片资源
├── en.lproj/                  # 英文
├── zh-Hans.lproj/             # 简体中文
├── zh-Hant.lproj/             # 繁体中文
└── WebStatic/                 # Web 静态资源
```

---

## 8. 待迁移资源

### 高优先级
- [ ] 横屏布局验证
- [ ] 更多语言支持
- [ ] 自定义主题资源

### 中优先级
- [ ] 动画效果验证
- [ ] 图标资源完善

### 低优先级
- [ ] raw 资源文件