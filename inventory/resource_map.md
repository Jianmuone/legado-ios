# Legado iOS Migration - Resource Map

> 本文档记录 Android Legado 资源文件到 iOS 的映射关系。
> 
> **生成日期**: 2026-04-08

---

## 1. 资源总览

| 资源类型 | Android 数量 | iOS 映射 |
|----------|--------------|----------|
| layout | 101 | Storyboard/XIB/SwiftUI |
| menu | 90 | UIMenu/UIAction |
| values | 10 | Localizable.strings |
| values-night | 2 | Asset Catalog |
| values-zh | 2 | Localizable.strings (zh-Hans) |
| values-zh-rHK | 2 | Localizable.strings (zh-Hant-HK) |
| values-zh-rTW | 2 | Localizable.strings (zh-Hant) |
| drawable | 100+ | Asset Catalog |
| anim | 5 | UIView.animate |
| raw | 1 | Bundle Resources |

---

## 2. Layout 映射

### 2.1 Activity 映射

| Android Layout | iOS 实现 | 说明 |
|----------------|----------|------|
| `activity_main.xml` | `MainTabBarController.swift` | 主界面 TabBar |
| `activity_read_book.xml` | `ReaderViewController.swift` | 阅读页 |
| `activity_book_info.xml` | `BookInfoViewController.swift` | 书籍详情 |
| `activity_book_source.xml` | `BookSourceViewController.swift` | 书源管理 |
| `activity_book_search.xml` | `SearchViewController.swift` | 搜索页 |
| `activity_config.xml` | `ConfigViewController.swift` | 配置页 |

### 2.2 Fragment 映射

| Android Layout | iOS 实现 | 说明 |
|----------------|----------|------|
| `fragment_bookshelf1.xml` | `BookshelfListViewController.swift` | 书架列表 |
| `fragment_bookshelf2.xml` | `BookshelfGridViewController.swift` | 书架网格 |
| `fragment_explore.xml` | `ExploreViewController.swift` | 发现页 |
| `fragment_rss.xml` | `RssViewController.swift` | RSS 订阅 |
| `fragment_my_config.xml` | `MyViewController.swift` | 我的 |
| `fragment_chapter_list.xml` | `ChapterListViewController.swift` | 章节列表 |

### 2.3 Dialog 映射

| Android Layout | iOS 实现 | 说明 |
|----------------|----------|------|
| `dialog_read_book_style.xml` | `ReadStyleViewController.swift` | 阅读样式 |
| `dialog_read_aloud.xml` | `ReadAloudViewController.swift` | 朗读设置 |
| `dialog_change_cover.xml` | `ChangeCoverViewController.swift` | 换封面 |
| `dialog_book_change_source.xml` | `ChangeSourceViewController.swift` | 换源 |

---

## 3. Menu 映射

### 3.1 选项菜单

| Android Menu | iOS 实现 | 说明 |
|--------------|----------|------|
| `menu/main_bnv.xml` | `UITabBarController` | 底部导航 |
| `menu/book_read.xml` | `UIMenu` | 阅读页菜单 |
| `menu/book_source.xml` | `UIMenu` | 书源菜单 |
| `menu/bookshelf_manage.xml` | `UIMenu` | 书架管理 |

### 3.2 上下文菜单

| Android Menu | iOS 实现 | 说明 |
|--------------|----------|------|
| `menu/bookshelf_manage_sel.xml` | `UIContextMenuConfiguration` | 书架长按菜单 |
| `menu/book_source_item.xml` | `UIContextMenuConfiguration` | 书源长按菜单 |

---

## 4. 多语言支持

### 4.1 支持的语言

| 语言 | Android values | iOS lproj |
|------|----------------|-----------|
| 默认（英文） | `values/` | `en.lproj/` |
| 简体中文 | `values-zh/` | `zh-Hans.lproj/` |
| 繁体中文（台湾） | `values-zh-rTW/` | `zh-Hant.lproj/` |
| 繁体中文（香港） | `values-zh-rHK/` | `zh-Hant-HK.lproj/` |

### 4.2 字符串映射

**Android:**
```xml
<!-- values-zh/strings.xml -->
<string name="bookshelf">书架</string>
<string name="explore">发现</string>
<string name="rss">订阅</string>
```

**iOS:**
```
// zh-Hans.lproj/Localizable.strings
"bookshelf" = "书架";
"explore" = "发现";
"rss" = "订阅";
```

---

## 5. 夜间模式

### 5.1 颜色映射

**Android:**
```xml
<!-- values-night/colors.xml -->
<color name="primary">#FF000000</color>
<color name="background">#FF1E1E1E</color>
```

**iOS:**
```swift
// Asset Catalog → Color Set
// Name: primary
// Dark: #000000
// Name: background
// Dark: #1E1E1E
```

### 5.2 样式映射

**Android:**
```xml
<!-- values-night/styles.xml -->
<style name="AppTheme" parent="Theme.MaterialComponents.DayNight">
    <item name="colorPrimary">@color/primary</item>
</style>
```

**iOS:**
```swift
// 自动适配夜间模式
UIColor(named: "primary")
```

---

## 6. 图标映射

### 6.1 底部导航图标

| Android Drawable | iOS Asset | 说明 |
|------------------|-----------|------|
| `ic_bottom_books.xml` | `tab_bookshelf` | 书架 |
| `ic_bottom_explore.xml` | `tab_explore` | 发现 |
| `ic_bottom_rss_feed.xml` | `tab_rss` | RSS |
| `ic_bottom_person.xml` | `tab_my` | 我的 |

### 6.2 常用图标

| Android Drawable | iOS Asset | SF Symbol | 说明 |
|------------------|-----------|-----------|------|
| `ic_search.xml` | `icon_search` | `magnifyingglass` | 搜索 |
| `ic_add.xml` | `icon_add` | `plus` | 添加 |
| `ic_edit.xml` | `icon_edit` | `pencil` | 编辑 |
| `ic_delete.xml` | `icon_delete` | `trash` | 删除 |
| `ic_settings.xml` | `icon_settings` | `gearshape` | 设置 |
| `ic_bookmark.xml` | `icon_bookmark` | `bookmark` | 书签 |
| `ic_chapter_list.xml` | `icon_chapter` | `list.bullet` | 目录 |

---

## 7. 动画映射

### 7.1 阅读页动画

| Android Animation | iOS 实现 | 说明 |
|-------------------|----------|------|
| `anim_readbook_top_in.xml` | `UIView.animate` | 顶部菜单进入 |
| `anim_readbook_top_out.xml` | `UIView.animate` | 顶部菜单退出 |
| `anim_readbook_bottom_in.xml` | `UIView.animate` | 底部菜单进入 |
| `anim_readbook_bottom_out.xml` | `UIView.animate` | 底部菜单退出 |

### 7.2 翻页动画

| 翻页模式 | Android 实现 | iOS 实现 | 状态 |
|----------|--------------|----------|------|
| 覆盖 | `CoverPageView` | `CoverPageViewController` | ✅ 已完成 |
| 仿真 | `SimulationPageView` | `SimulationPageViewController` | ✅ 已完成 |
| 滑动 | `ScrollPageView` | `ScrollPageViewController` | ✅ 已完成 |
| 滚动 | `TextView.scroll` | `UITextView` | ✅ 已完成 |

---

## 8. 字体资源

### 8.1 内置字体

| 字体 | Android 路径 | iOS 路径 |
|------|--------------|----------|
| 系统字体 | 系统提供 | 系统提供 |
| 自定义字体 | `assets/fonts/` | `Resources/Fonts/` |

### 8.2 字体加载

```swift
// iOS 字体注册
guard let fontURL = Bundle.main.url(forResource: "CustomFont", withExtension: "ttf") else { return }
CTFontManagerRegisterFontsForURL(fontURL as CFURL, .process, nil)
```

---

## 9. 原始资源

### 9.1 音频文件

| Android raw | iOS Resources | 用途 |
|-------------|---------------|------|
| `silent_sound.mp3` | `silent_sound.mp3` | 静音音频 |

---

## 10. 资源迁移状态

| 资源类型 | 迁移进度 |
|----------|----------|
| layout | 🔄 30% |
| menu | ⏳ 0% |
| values (strings) | 🔄 50% |
| values-night | ⏳ 0% |
| drawable (icons) | 🔄 40% |
| anim | 🔄 60% |
| fonts | ⏳ 0% |

---

*本文档由 Wave 0 基线采集自动生成*