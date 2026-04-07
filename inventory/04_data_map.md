# 数据实体映射 (Data Map)

**创建时间**: 2026-04-08

---

## 1. 实体总览

| Android 实体 | iOS 实体 | 状态 | 差异说明 |
|--------------|----------|------|----------|
| Book | Book | ✅ | 字段完全对齐 |
| BookChapter | BookChapter | ✅ | 字段完全对齐 |
| BookGroup | BookGroup | ✅ | 字段完全对齐 |
| Bookmark | Bookmark | ✅ | 字段完全对齐 |
| BookSource | BookSource | ✅ | 字段完全对齐 |
| BookProgress | BookProgress | ✅ | 字段完全对齐 |
| Cookie | Cookie | ✅ | 字段完全对齐 |
| ReplaceRule | ReplaceRule | ✅ | 字段完全对齐 |
| RssSource | RssSource | ✅ | 字段完全对齐 |
| RssArticle | RssArticle | ✅ | 字段完全对齐 |
| RssReadRecord | RssReadRecord | ✅ | 字段完全对齐 |
| RssStar | RssStar | ✅ | 字段完全对齐 |
| SearchBook | SearchBook | ✅ | 字段完全对齐 |
| SearchKeyword | SearchKeyword | ✅ | 字段完全对齐 |
| HttpTTS | HttpTTS | ✅ | 字段完全对齐 |
| DictRule | DictRule | ✅ | 字段完全对齐 |
| RuleSub | RuleSub | ✅ | 字段完全对齐 |
| TxtTocRule | TxtTocRule | ✅ | 字段完全对齐 |
| Cache | CacheEntry | ✅ | 字段完全对齐 |
| ReadRecord | ReadRecord | ✅ | 字段完全对齐 |
| Server | ❌ | ❌ | 未迁移 |
| KeyboardAssist | ❌ | ❌ | 未迁移 |
| BookChapterReview | ❌ | ❌ | 未迁移 |
| BookSourcePart | ❌ | ❌ | 未迁移 |

---

## 2. Book 实体详细映射

### 2.1 字段对照表

| Android 字段 | 类型 | iOS 字段 | 类型 | 主键 | 索引 | 默认值 | 说明 |
|--------------|------|----------|------|------|------|--------|------|
| bookUrl | String | bookUrl | String | ✅ | ✅ | - | 详情页URL（主键） |
| bookId | - | bookId | UUID | - | - | 自动生成 | iOS 内部主键 |
| tocUrl | String | tocUrl | String | - | - | "" | 目录页URL |
| origin | String | origin | String | - | - | - | 书源URL |
| originName | String | originName | String | - | - | - | 书源名称 |
| name | String | name | String | - | - | - | 书籍名称 |
| author | String | author | String | - | - | - | 作者 |
| kind | String? | kind | String? | - | - | null | 分类 |
| customTag | String? | customTag | String? | - | - | null | 自定义标签 |
| coverUrl | String? | coverUrl | String? | - | - | null | 封面URL |
| customCoverUrl | String? | customCoverUrl | String? | - | - | null | 自定义封面 |
| intro | String? | intro | String? | - | - | null | 简介 |
| customIntro | String? | customIntro | String? | - | - | null | 自定义简介 |
| charset | String? | charset | String? | - | - | null | 字符集 |
| type | Int | type | Int32 | - | - | 0 | 类型 |
| group | Long | group | Int64 | - | - | 0 | 分组索引 |
| latestChapterTitle | String? | latestChapterTitle | String? | - | - | null | 最新章节标题 |
| latestChapterTime | Long | latestChapterTime | Int64 | - | - | 0 | 最新章节时间 |
| lastCheckTime | Long | lastCheckTime | Int64 | - | - | 0 | 最后检查时间 |
| lastCheckCount | Int | lastCheckCount | Int32 | - | - | 0 | 最后检查数量 |
| totalChapterNum | Int | totalChapterNum | Int32 | - | - | 0 | 总章节数 |
| durChapterTitle | String? | durChapterTitle | String? | - | - | null | 当前章节标题 |
| durChapterIndex | Int | durChapterIndex | Int32 | - | - | 0 | 当前章节索引 |
| durChapterPos | Int | durChapterPos | Int32 | - | - | 0 | 当前阅读位置 |
| durChapterTime | Long | durChapterTime | Int64 | - | - | 0 | 当前阅读时间 |
| wordCount | String? | wordCount | String? | - | - | null | 字数 |
| canUpdate | Boolean | canUpdate | Bool | - | - | true | 是否可更新 |
| order | Int | order | Int32 | - | - | 0 | 手动排序 |
| originOrder | Int | originOrder | Int32 | - | - | 0 | 书源排序 |
| variable | String? | variable | String? | - | - | null | 自定义变量 |
| readConfig | ReadConfig? | readConfigData | Data? | - | - | null | 阅读配置 |
| infoHtml | String? | infoHtml | String? | - | - | null | 详情页HTML缓存 |
| tocHtml | String? | tocHtml | String? | - | - | null | 目录页HTML缓存 |
| downloadUrls | String? | downloadUrls | String? | - | - | null | 下载URLs |
| folderName | String? | folderName | String? | - | - | null | 文件夹名 |
| - | - | createdAt | Date | - | - | 自动 | 创建时间 |
| - | - | updatedAt | Date | - | - | 自动 | 更新时间 |
| - | - | syncTime | Int64 | - | - | 0 | 同步时间 |

### 2.2 关系映射

| Android 关系 | iOS 关系 | 类型 | 说明 |
|--------------|----------|------|------|
| source: BookSource? | source: BookSource? | 多对一 | 所属书源 |
| chapters: List<BookChapter> | chapters: NSSet? | 一对多 | 章节列表 |
| bookmarks: List<Bookmark> | bookmarks: NSSet? | 一对多 | 书签列表 |

---

## 3. BookSource 实体详细映射

### 3.1 字段对照表

| Android 字段 | 类型 | iOS 字段 | 类型 | 主键 | 索引 | 默认值 | 说明 |
|--------------|------|----------|------|------|------|--------|------|
| bookSourceUrl | String | bookSourceUrl | String | ✅ | - | - | 书源URL（主键） |
| - | - | sourceId | UUID | - | - | 自动 | iOS 内部主键 |
| bookSourceName | String | bookSourceName | String | - | - | - | 书源名称 |
| bookSourceGroup | String? | bookSourceGroup | String? | - | - | null | 分组 |
| bookSourceType | Int | bookSourceType | Int32 | - | - | 0 | 类型 |
| bookUrlPattern | String? | bookUrlPattern | String? | - | - | null | 详情页URL正则 |
| customOrder | Int | customOrder | Int32 | - | - | 0 | 手动排序 |
| enabled | Boolean | enabled | Bool | - | - | true | 是否启用 |
| enabledExplore | Boolean | enabledExplore | Bool | - | - | true | 是否启用发现 |
| enabledCookieJar | Boolean | enabledCookieJar | Bool | - | - | false | 启用Cookie |
| concurrentRate | String? | concurrentRate | String? | - | - | null | 并发率 |
| header | String? | header | String? | - | - | null | 请求头 |
| loginUrl | String? | loginUrl | String? | - | - | null | 登录地址 |
| loginUi | String? | loginUi | String? | - | - | null | 登录UI |
| loginCheckJs | String? | loginCheckJs | String? | - | - | null | 登录检测JS |
| coverDecodeJs | String? | coverDecodeJs | String? | - | - | null | 封面解密JS |
| jsLib | String? | jsLib | String? | - | - | null | JS库 |
| bookSourceComment | String? | bookSourceComment | String? | - | - | null | 注释 |
| variableComment | String? | variableComment | String? | - | - | null | 变量说明 |
| lastUpdateTime | Long | lastUpdateTime | Int64 | - | - | 0 | 最后更新时间 |
| respondTime | Long | respondTime | Int64 | - | - | 0 | 响应时间 |
| weight | Int | weight | Int32 | - | - | 0 | 权重 |
| exploreUrl | String? | exploreUrl | String? | - | - | null | 发现URL |
| exploreScreen | String? | exploreScreen | String? | - | - | null | 发现筛选 |
| searchUrl | String? | searchUrl | String? | - | - | null | 搜索URL |
| variable | String? | variable | String? | - | - | null | 自定义变量 |
| ruleExplore | Rule? | ruleExploreData | Data? | - | - | null | 发现规则（JSON） |
| ruleSearch | Rule? | ruleSearchData | Data? | - | - | null | 搜索规则（JSON） |
| ruleBookInfo | Rule? | ruleBookInfoData | Data? | - | - | null | 书籍规则（JSON） |
| ruleToc | Rule? | ruleTocData | Data? | - | - | null | 目录规则（JSON） |
| ruleContent | Rule? | ruleContentData | Data? | - | - | null | 正文规则（JSON） |
| ruleReview | Rule? | ruleReviewData | Data? | - | - | null | 段评规则（JSON） |

### 3.2 规则数据存储方式

**Android**: 使用 Room 的 `@Embedded` 嵌套对象  
**iOS**: 使用 `Data?` 存储 JSON 序列化后的规则对象

---

## 4. 序列化格式兼容

### 4.1 JSON 导入格式

iOS 必须兼容 Android 导出的 JSON 格式：

```json
{
  "bookSourceUrl": "https://example.com",
  "bookSourceName": "示例书源",
  "bookSourceGroup": "小说",
  "bookSourceType": 0,
  "enabled": true,
  "searchUrl": "https://example.com/search?key={{key}}",
  "ruleSearch": {
    "bookList": "div.book-item",
    "name": "h2@text",
    "author": "span.author@text"
  },
  "ruleBookInfo": {...},
  "ruleToc": {...},
  "ruleContent": {...}
}
```

### 4.2 字段命名规则

- **禁止**为了 Swift 风格改字段名（如 `bookUrl` 改 `bookURL`）
- **必须**保持与 Android JSON 格式完全一致
- **内部**可使用不同的 Swift 属性名，但 Codin gKeys 必须映射

---

## 5. 迁移策略

### 5.1 已完成

- ✅ 所有核心实体已迁移
- ✅ 字段类型已对齐
- ✅ 关系已定义
- ✅ JSON 序列化已兼容

### 5.2 待优化

- ⚠️ 部分字段命名不完全一致（内部可优化，外部必须兼容）
- ⚠️ 规则数据使用 Data 存储，需手动序列化/反序列化
- ⚠️ 缺少 Server、KeyboardAssist、BookChapterReview、BookSourcePart 实体