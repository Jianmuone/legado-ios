# Legado iOS Migration - Data Map

> 本文档记录 Android Legado 数据实体到 iOS 的映射关系。
> 
> **生成日期**: 2026-04-08
> **实体总数**: 17

---

## 1. Book (书籍)

### 1.1 Android 字段

| 字段 | 类型 | 主键 | 索引 | 默认值 | 可空 | 语义 |
|------|------|------|------|--------|------|------|
| `bookUrl` | String | ✅ | ❌ | "" | ❌ | 书籍唯一标识 URL |
| `tocUrl` | String | ❌ | ❌ | "" | ❌ | 目录页 URL |
| `origin` | String | ❌ | ❌ | BookType.localTag | ❌ | 书源 URL |
| `originName` | String | ❌ | ❌ | "" | ❌ | 书源名称 |
| `name` | String | ❌ | ✅ | "" | ❌ | 书名 |
| `author` | String | ❌ | ✅ | "" | ❌ | 作者 |
| `kind` | String? | ❌ | ❌ | null | ✅ | 分类 |
| `customTag` | String? | ❌ | ❌ | null | ✅ | 自定义标签 |
| `coverUrl` | String? | ❌ | ❌ | null | ✅ | 封面 URL |
| `customCoverUrl` | String? | ❌ | ❌ | null | ✅ | 自定义封面 URL |
| `intro` | String? | ❌ | ❌ | null | ✅ | 简介 |
| `customIntro` | String? | ❌ | ❌ | null | ✅ | 自定义简介 |
| `charset` | String? | ❌ | ❌ | null | ✅ | 字符编码 |
| `type` | Int | ❌ | ❌ | 0 | ❌ | 书籍类型 |
| `group` | Long | ❌ | ❌ | 0 | ❌ | 分组 ID |
| `latestChapterTitle` | String? | ❌ | ❌ | null | ✅ | 最新章节标题 |
| `latestChapterTime` | Long | ❌ | ❌ | 0 | ❌ | 最新章节时间 |
| `lastCheckTime` | Long | ❌ | ❌ | 0 | ❌ | 最后检查时间 |
| `lastCheckCount` | Int | ❌ | ❌ | 0 | ❌ | 最后检查章节数 |
| `totalChapterNum` | Int | ❌ | ❌ | 0 | ❌ | 总章节数 |
| `durChapterTitle` | String? | ❌ | ❌ | null | ✅ | 当前章节标题 |
| `durChapterIndex` | Int | ❌ | ❌ | 0 | ❌ | 当前章节索引 |
| `durChapterPos` | Int | ❌ | ❌ | 0 | ❌ | 当前章节位置 |
| `durChapterTime` | Long | ❌ | ❌ | 0 | ❌ | 当前章节时间 |
| `wordCount` | String? | ❌ | ❌ | null | ✅ | 字数 |
| `canUpdate` | Boolean | ❌ | ❌ | true | ❌ | 是否可更新 |
| `order` | Int | ❌ | ❌ | 0 | ❌ | 排序 |
| `originOrder` | Int | ❌ | ❌ | 0 | ❌ | 原排序 |
| `variable` | String? | ❌ | ❌ | null | ✅ | 变量 JSON |
| `readConfig` | ReadConfig? | ❌ | ❌ | null | ✅ | 阅读配置 |
| `syncTime` | Long | ❌ | ❌ | 0 | ❌ | 同步时间 |

### 1.2 iOS 对应结构

```swift
// Core/Persistence/Entities/Book+CoreDataClass.swift
@objc(Book)
public class Book: NSManagedObject {
    @NSManaged public var bookUrl: String
    @NSManaged public var tocUrl: String
    @NSManaged public var origin: String
    @NSManaged public var originName: String
    @NSManaged public var name: String
    @NSManaged public var author: String
    @NSManaged public var kind: String?
    @NSManaged public var customTag: String?
    @NSManaged public var coverUrl: String?
    @NSManaged public var customCoverUrl: String?
    @NSManaged public var intro: String?
    @NSManaged public var customIntro: String?
    @NSManaged public var charset: String?
    @NSManaged public var type: Int32
    @NSManaged public var group: Int64
    @NSManaged public var latestChapterTitle: String?
    @NSManaged public var latestChapterTime: Int64
    @NSManaged public var lastCheckTime: Int64
    @NSManaged public var lastCheckCount: Int32
    @NSManaged public var totalChapterNum: Int32
    @NSManaged public var durChapterTitle: String?
    @NSManaged public var durChapterIndex: Int32
    @NSManaged public var durChapterPos: Int32
    @NSManaged public var durChapterTime: Int64
    @NSManaged public var wordCount: String?
    @NSManaged public var canUpdate: Bool
    @NSManaged public var order: Int32
    @NSManaged public var originOrder: Int32
    @NSManaged public var variable: String?
    @NSManaged public var readConfigData: Data? // 序列化的 ReadConfig
    @NSManaged public var syncTime: Int64
}
```

### 1.3 迁移策略

- 字段命名保持一致，确保 JSON 导入导出兼容
- `ReadConfig` 作为嵌套对象存储，iOS 使用 `Codable` 序列化
- 索引字段 `name`、`author` 在 CoreData 中配置索引

---

## 2. BookChapter (章节)

### 2.1 Android 字段

| 字段 | 类型 | 主键 | 索引 | 默认值 | 可空 | 语义 |
|------|------|------|------|--------|------|------|
| `url` | String | ✅ | ❌ | "" | ❌ | 章节 URL |
| `title` | String | ❌ | ❌ | "" | ❌ | 章节标题 |
| `isVolume` | Boolean | ❌ | ❌ | false | ❌ | 是否卷名 |
| `baseUrl` | String | ❌ | ❌ | "" | ❌ | 基础 URL |
| `bookUrl` | String | ✅ | ✅ | "" | ❌ | 所属书籍 URL |
| `index` | Int | ❌ | ✅ | 0 | ❌ | 章节索引 |
| `isVip` | Boolean | ❌ | ❌ | false | ❌ | 是否 VIP |
| `isPay` | Boolean | ❌ | ❌ | false | ❌ | 是否付费 |
| `resourceUrl` | String? | ❌ | ❌ | null | ✅ | 资源 URL |
| `tag` | String? | ❌ | ❌ | null | ✅ | 标签 |
| `wordCount` | String? | ❌ | ❌ | null | ✅ | 字数 |
| `start` | Long? | ❌ | ❌ | null | ✅ | 起始位置 |
| `end` | Long? | ❌ | ❌ | null | ✅ | 结束位置 |
| `startFragmentId` | String? | ❌ | ❌ | null | ✅ | 起始片段 ID |
| `endFragmentId` | String? | ❌ | ❌ | null | ✅ | 结束片段 ID |
| `variable` | String? | ❌ | ❌ | null | ✅ | 变量 |

### 2.2 iOS 对应结构

```swift
@objc(BookChapter)
public class BookChapter: NSManagedObject {
    @NSManaged public var url: String
    @NSManaged public var title: String
    @NSManaged public var isVolume: Bool
    @NSManaged public var baseUrl: String
    @NSManaged public var bookUrl: String
    @NSManaged public var index: Int32
    @NSManaged public var isVip: Bool
    @NSManaged public var isPay: Bool
    @NSManaged public var resourceUrl: String?
    @NSManaged public var tag: String?
    @NSManaged public var wordCount: String?
    @NSManaged public var start: Int64
    @NSManaged public var end: Int64
    @NSManaged public var startFragmentId: String?
    @NSManaged public var endFragmentId: String?
    @NSManaged public var variable: String?
}
```

---

## 3. BookSource (书源)

### 3.1 Android 字段

| 字段 | 类型 | 主键 | 默认值 | 语义 |
|------|------|------|--------|------|
| `bookSourceUrl` | String | ✅ | "" | 书源 URL（主键） |
| `bookSourceName` | String | ❌ | "" | 书源名称 |
| `bookSourceGroup` | String? | ❌ | null | 书源分组 |
| `bookSourceType` | Int | ❌ | 0 | 书源类型 |
| `bookUrlPattern` | String? | ❌ | null | 书籍 URL 正则 |
| `customOrder` | Int | ❌ | 0 | 自定义排序 |
| `enabled` | Boolean | ❌ | true | 是否启用 |
| `enabledExplore` | Boolean | ❌ | true | 是否启用发现 |
| `jsLib` | String? | ❌ | null | JS 库 |
| `enabledCookieJar` | Boolean? | ❌ | true | 是否启用 Cookie |
| `concurrentRate` | String? | ❌ | null | 并发限制 |
| `header` | String? | ❌ | null | 请求头 |
| `loginUrl` | String? | ❌ | null | 登录 URL |
| `loginUi` | String? | ❌ | null | 登录 UI 配置 |
| `loginCheckJs` | String? | ❌ | null | 登录检查 JS |
| `coverDecodeJs` | String? | ❌ | null | 封面解码 JS |
| `bookSourceComment` | String? | ❌ | null | 书源说明 |
| `variableComment` | String? | ❌ | null | 变量说明 |
| `lastUpdateTime` | Long | ❌ | 0 | 最后更新时间 |
| `respondTime` | Long | ❌ | 180000 | 响应时间 |
| `weight` | Int | ❌ | 0 | 权重 |
| `exploreUrl` | String? | ❌ | null | 发现 URL |
| `exploreScreen` | String? | ❌ | null | 发现屏幕 |
| `ruleExplore` | ExploreRule? | ❌ | null | 发现规则 |
| `searchUrl` | String? | ❌ | null | 搜索 URL |
| `ruleSearch` | SearchRule? | ❌ | null | 搜索规则 |
| `ruleBookInfo` | BookInfoRule? | ❌ | null | 书籍信息规则 |
| `ruleToc` | TocRule? | ❌ | null | 目录规则 |
| `ruleContent` | ContentRule? | ❌ | null | 正文规则 |
| `ruleReview` | ReviewRule? | ❌ | null | 评论规则 |

### 3.2 iOS 对应结构

```swift
@objc(BookSource)
public class BookSource: NSManagedObject {
    @NSManaged public var bookSourceUrl: String
    @NSManaged public var bookSourceName: String
    @NSManaged public var bookSourceGroup: String?
    @NSManaged public var bookSourceType: Int32
    @NSManaged public var bookUrlPattern: String?
    @NSManaged public var customOrder: Int32
    @NSManaged public var enabled: Bool
    @NSManaged public var enabledExplore: Bool
    @NSManaged public var jsLib: String?
    @NSManaged public var enabledCookieJar: Bool
    @NSManaged public var concurrentRate: String?
    @NSManaged public var header: String?
    @NSManaged public var loginUrl: String?
    @NSManaged public var loginUi: String?
    @NSManaged public var loginCheckJs: String?
    @NSManaged public var coverDecodeJs: String?
    @NSManaged public var bookSourceComment: String?
    @NSManaged public var variableComment: String?
    @NSManaged public var lastUpdateTime: Int64
    @NSManaged public var respondTime: Int64
    @NSManaged public var weight: Int32
    @NSManaged public var exploreUrl: String?
    @NSManaged public var exploreScreen: String?
    @NSManaged public var searchUrl: String?
    // 规则作为序列化数据存储
    @NSManaged public var ruleExploreData: Data?
    @NSManaged public var ruleSearchData: Data?
    @NSManaged public var ruleBookInfoData: Data?
    @NSManaged public var ruleTocData: Data?
    @NSManaged public var ruleContentData: Data?
    @NSManaged public var ruleReviewData: Data?
}
```

---

## 4. ReplaceRule (替换规则)

### 4.1 Android 字段

| 字段 | 类型 | 主键 | 默认值 | 语义 |
|------|------|------|--------|------|
| `id` | Long | ✅ | System.currentTimeMillis() | 规则 ID |
| `name` | String | ❌ | "" | 规则名称 |
| `group` | String? | ❌ | null | 分组 |
| `pattern` | String | ❌ | "" | 匹配模式 |
| `replacement` | String | ❌ | "" | 替换内容 |
| `scope` | String? | ❌ | null | 作用范围 |
| `scopeTitle` | Boolean | ❌ | false | 作用于标题 |
| `scopeContent` | Boolean | ❌ | true | 作用于正文 |
| `excludeScope` | String? | ❌ | null | 排除范围 |
| `isEnabled` | Boolean | ❌ | true | 是否启用 |
| `isRegex` | Boolean | ❌ | true | 是否正则 |
| `timeoutMillisecond` | Long | ❌ | 3000 | 超时时间 |
| `order` | Int | ❌ | 0 | 排序 |

### 4.2 iOS 对应结构

```swift
@objc(ReplaceRule)
public class ReplaceRule: NSManagedObject {
    @NSManaged public var ruleId: UUID
    @NSManaged public var name: String
    @NSManaged public var pattern: String
    @NSManaged public var replacement: String
    @NSManaged public var scope: String
    @NSManaged public var scopeId: String?
    @NSManaged public var isRegex: Bool
    @NSManaged public var enabled: Bool
    @NSManaged public var priority: Int32
    @NSManaged public var order: Int32
    @NSManaged public var timeoutMillisecond: Int64
    
    var isEnabled: Bool { get { enabled } set { enabled = newValue } }
    lazy var regex: NSRegularExpression? = { ... }()
}
```

---

## 5. RssSource (订阅源)

### 5.1 关键字段

| 字段 | 类型 | 主键 | 默认值 | 语义 |
|------|------|------|--------|------|
| `sourceUrl` | String | ✅ | "" | 订阅源 URL |
| `sourceName` | String | ❌ | "" | 订阅源名称 |
| `sourceIcon` | String | ❌ | "" | 图标 URL |
| `sourceGroup` | String? | ❌ | null | 分组 |
| `singleUrl` | Boolean | ❌ | false | 是否单 URL |
| `articleStyle` | Int | ❌ | 0 | 文章样式 |
| `ruleArticles` | String? | ❌ | null | 文章列表规则 |
| `ruleTitle` | String? | ❌ | null | 标题规则 |
| `ruleLink` | String? | ❌ | null | 链接规则 |
| `ruleContent` | String? | ❌ | null | 正文规则 |

---

## 6. 其他实体清单

| 实体 | 表名 | 主键 | iOS 迁移状态 |
|------|------|------|--------------|
| `BookGroup` | book_groups | groupId | ✅ 已完成 |
| `Bookmark` | bookmarks | time | ✅ 已完成 |
| `Cookie` | cookies | url | ⏳ 待迁移 |
| `RssArticle` | rssArticles | origin + link | ⏳ 待迁移 |
| `RssReadRecord` | rssReadRecords | record | ⏳ 待迁移 |
| `RssStar` | rssStars | origin + link | ⏳ 待迁移 |
| `SearchBook` | searchBooks | bookUrl | ⏳ 待迁移 |
| `SearchKeyword` | search_keywords | word | ⏳ 待迁移 |
| `TxtTocRule` | txtTocRules | id | ⏳ 待迁移 |
| `HttpTTS` | httpTTS | id | ⏳ 待迁移 |
| `DictRule` | dictRules | name | ⏳ 待迁移 |
| `RuleSub` | ruleSubs | id | ⏳ 待迁移 |

---

## 7. 序列化格式

### 7.1 JSON 导入导出

所有实体必须支持 JSON 序列化/反序列化，格式必须与 Android 完全兼容：

```swift
extension Book: Codable {
    enum CodingKeys: String, CodingKey {
        case bookUrl
        case tocUrl
        case origin
        // ... 保持字段名一致
    }
}
```

### 7.2 嵌套对象处理

| Android 嵌套类型 | iOS 处理方式 |
|------------------|--------------|
| `ReadConfig` | `Codable` 序列化为 Data 存储 |
| `ExploreRule` | `Codable` 序列化为 Data 存储 |
| `SearchRule` | `Codable` 序列化为 Data 存储 |
| `BookInfoRule` | `Codable` 序列化为 Data 存储 |
| `TocRule` | `Codable` 序列化为 Data 存储 |
| `ContentRule` | `Codable` 序列化为 Data 存储 |

---

## 8. 迁移进度

| 实体 | Android 完成 | iOS CoreData | iOS DAO | iOS 序列化 |
|------|--------------|--------------|---------|------------|
| Book | ✅ | ✅ | ⏳ | ✅ |
| BookChapter | ✅ | ✅ | ⏳ | ✅ |
| BookSource | ✅ | ✅ | ⏳ | ⏳ |
| BookGroup | ✅ | ✅ | ✅ | ✅ |
| Bookmark | ✅ | ✅ | ✅ | ✅ |
| ReplaceRule | ✅ | ✅ | ✅ | ✅ |
| RssSource | ✅ | ⏳ | ⏳ | ⏳ |
| RssArticle | ✅ | ⏳ | ⏳ | ⏳ |

---

*本文档由 Wave 0 基线采集自动生成*