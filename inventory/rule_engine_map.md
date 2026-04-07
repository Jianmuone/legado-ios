# Legado iOS Migration - Rule Engine Map

> 本文档记录 Android Legado 规则引擎到 iOS 的映射关系。
> 
> **生成日期**: 2026-04-08

---

## 1. 规则引擎总览

### 1.1 Android 规则执行流程

```
用户操作 → 书源规则 → AnalyzeRule → HTML/XPath/JSONPath/JS 解析 → 结果返回
```

### 1.2 iOS 规则执行流程

```
用户操作 → 书源规则 → AnalyzeRule → SwiftSoup/Fuzi/JavaScriptCore 解析 → 结果返回
```

---

## 2. 规则类型

### 2.1 书源规则

| 规则类型 | Android 实现 | iOS 实现 | 状态 |
|----------|--------------|----------|------|
| **搜索规则** | `SearchRule` | `SearchRule.swift` | ⏳ 待迁移 |
| **发现规则** | `ExploreRule` | `ExploreRule.swift` | ⏳ 待迁移 |
| **书籍信息规则** | `BookInfoRule` | `BookInfoRule.swift` | ⏳ 待迁移 |
| **目录规则** | `TocRule` | `TocRule.swift` | ⏳ 待迁移 |
| **正文规则** | `ContentRule` | `ContentRule.swift` | ⏳ 待迁移 |

### 2.2 订阅源规则

| 规则类型 | Android 实现 | iOS 实现 | 状态 |
|----------|--------------|----------|------|
| **文章列表规则** | `ruleArticles` | `RssRule.swift` | ⏳ 待迁移 |
| **标题规则** | `ruleTitle` | `RssRule.swift` | ⏳ 待迁移 |
| **链接规则** | `ruleLink` | `RssRule.swift` | ⏳ 待迁移 |
| **正文规则** | `ruleContent` | `RssRule.swift` | ⏳ 待迁移 |

### 2.3 替换规则

| 规则类型 | Android 实现 | iOS 实现 | 状态 |
|----------|--------------|----------|------|
| **正则替换** | `NSRegularExpression` | `NSRegularExpression` | ✅ 已完成 |
| **普通替换** | `String.replace` | `String.replacingOccurrences` | ✅ 已完成 |

---

## 3. 规则语法

### 3.1 JSOUP Default

**Android:**
```kotlin
class.odd.0@tag.a.0@text##全文阅读
```

**iOS:**
```swift
// 使用 SwiftSoup 解析
let doc = try SwiftSoup.parse(html)
let element = try doc.select(".odd").first()?.select("a").first()
let text = try element?.text()
```

### 3.2 CSS Selector

**Android:**
```kotlin
@css:.articleDiv p@textNodes
```

**iOS:**
```swift
// 使用 SwiftSoup
let elements = try doc.select(".articleDiv p")
let texts = elements.map { try $0.text() }
```

### 3.3 XPath

**Android:**
```kotlin
//*[@id="content"]//text()
```

**iOS:**
```swift
// 使用 Fuzi/Kanna
import Kanna
let doc = try HTML(html: html, encoding: .utf8)
let nodes = doc.xpath("//*[@id='content']//text()")
```

### 3.4 JSONPath

**Android:**
```kotlin
$.chapter.body
```

**iOS:**
```swift
// 使用 JSONPath 实现
import Foundation
let json = try JSONSerialization.jsonObject(with: data)
let value = json.value(forKeyPath: "chapter.body")
```

### 3.5 JavaScript

**Android (Rhino):**
```javascript
<js>
result.map(item => ({
  name: item.title,
  url: item.link
}))
</js>
```

**iOS (JavaScriptCore):**
```swift
import JavaScriptCore
let context = JSContext()!
context.evaluateScript(jsCode)
let result = context.objectForKeyedSubscript("result")
```

---

## 4. AnalyzeRule 核心类

### 4.1 Android 实现

```kotlin
// model/AnalyzeRule.kt
class AnalyzeRule {
    fun setSource(source: Any)
    fun setContent(content: String)
    fun getElements(rule: String): List<Any>
    fun getString(rule: String): String?
    fun getStringList(rule: String): List<String>
}
```

### 4.2 iOS 实现（进行中）

```swift
// Core/Rules/AnalyzeRule.swift
class AnalyzeRule {
    var source: Any?
    var content: String?
    
    func setSource(_ source: Any)
    func setContent(_ content: String)
    func getElements(_ rule: String) -> [Any]
    func getString(_ rule: String) -> String?
    func getStringList(_ rule: String) -> [String]
}
```

---

## 5. 规则执行链路

### 5.1 搜索流程

```
1. 用户输入关键词
2. 构建 SearchUrl（替换 {{key}}, {{page}}）
3. 发送 HTTP 请求
4. 解析响应内容（根据 ruleSearch.bookList）
5. 提取书籍列表
6. 显示结果
```

### 5.2 目录流程

```
1. 打开书籍
2. 构建 TocUrl
3. 发送 HTTP 请求
4. 解析章节列表（根据 ruleToc.chapterList）
5. 提取章节信息
6. 显示目录
```

### 5.3 正文流程

```
1. 点击章节
2. 构建 ChapterUrl
3. 发送 HTTP 请求
4. 解析正文内容（根据 ruleContent.content）
5. 应用替换规则
6. 显示正文
```

---

## 6. 缓存策略

| 缓存类型 | Android 实现 | iOS 实现 | 状态 |
|----------|--------------|----------|------|
| 书源缓存 | 内存缓存 | NSCache | ⏳ 待迁移 |
| 章节缓存 | 文件缓存 | FileManager | ✅ 已完成 |
| 图片缓存 | LruCache | NSCache | ✅ 已完成 |

---

## 7. 异常处理

### 7.1 错误类型

| 错误类型 | Android 处理 | iOS 处理 |
|----------|--------------|----------|
| 网络错误 | 重试机制 | URLSession 重试 |
| 解析错误 | 日志记录 | 日志记录 |
| JS 执行错误 | 异常捕获 | JSContext 异常 |
| 超时 | TimeoutException | URLRequest timeout |

### 7.2 超时处理

| 场景 | 超时时间 | 配置项 |
|------|----------|--------|
| HTTP 请求 | 30s | `respondTime` |
| JS 执行 | 3s | `timeoutMillisecond` |
| 正则执行 | 3s | `timeoutMillisecond` |

---

## 8. 兼容性测试清单

### 8.1 必测场景

| 场景 | 测试内容 | 状态 |
|------|----------|------|
| 书源搜索 | 关键词搜索 → 结果匹配 | ⏳ 待测试 |
| 书源发现 | 发现页列表 → 书籍信息 | ⏳ 待测试 |
| 目录解析 | 章节列表 → 正确顺序 | ⏳ 待测试 |
| 正文解析 | 正文内容 → 图片/链接 | ⏳ 待测试 |
| 替换规则 | 正则替换 → 内容净化 | ⏳ 待测试 |
| RSS 订阅 | 文章列表 → 正文内容 | ⏳ 待测试 |

### 8.2 样本书源

需要准备以下类型的测试书源：

- 纯 HTML 书源
- JSON API 书源
- XPath 书源
- 需要 JS 执行的书源
- 需要登录的书源
- 需要正则的书源

---

## 9. JS 库支持

### 9.1 内置 JS 库

| 库名 | 功能 | iOS 支持 |
|------|------|----------|
| `JSON` | JSON 序列化/反序列化 | ✅ |
| `AES` | AES 加解密 | ⏳ |
| `RSA` | RSA 加解密 | ⏳ |
| `Base64` | Base64 编解码 | ✅ |
| `MD5` | MD5 哈希 | ✅ |

### 9.2 自定义 JS 库

用户可自定义 JS 库，注入到 JSContext：

```swift
let context = JSContext()!
let jsLib = bookSource.jsLib
context.evaluateScript(jsLib)
```

---

*本文档由 Wave 0 基线采集自动生成*