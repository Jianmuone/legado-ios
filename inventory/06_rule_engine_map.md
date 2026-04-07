# 规则引擎映射 (Rule Engine Map)

**创建时间**: 2026-04-08

---

## 1. 规则引擎架构

### 1.1 Android 规则引擎架构

```
Android 规则引擎
├── Rhino JS 引擎
│   ├── JavaScript 执行环境
│   ├── JS 库支持
│   └── 自定义函数注入
├── HTML 解析器
│   ├── Jsoup (CSS 选择器)
│   └── XPath
├── JSON 解析器
│   └── JSONPath
├── 正则表达式
│   └── Regex
└── 规则执行流程
    ├── URL 模板渲染
    ├── 规则解析与执行
    └── 结果处理
```

### 1.2 iOS 规则引擎架构

```
iOS 规则引擎
├── JavaScriptCore
│   ├── JSContext 执行环境
│   ├── JSBridge 自定义函数
│   └── JSValue 类型转换
├── SwiftSoup
│   └── CSS 选择器
├── Kanna
│   └── XPath 解析
├── Foundation
│   └── NSRegularExpression
└── 规则执行流程
    ├── TemplateEngine 模板渲染
    ├── RuleEngine 规则执行
    └── RuleAnalyzer 结果分析
```

---

## 2. 规则类型映射

### 2.1 书源规则类型

| 规则类型 | Android 实现 | iOS 实现 | 状态 |
|----------|--------------|----------|------|
| CSS 选择器 | Jsoup | SwiftSoup | ✅ |
| XPath | Javax XPath | Kanna | ✅ |
| JSONPath | 自定义 | 自定义 | ✅ |
| 正则表达式 | Java Regex | NSRegularExpression | ✅ |
| JavaScript | Rhino | JavaScriptCore | ✅ |
| 混合规则 | RuleAnalyzer | RuleAnalyzer | ✅ |

### 2.2 规则执行优先级

1. JavaScript 规则 (`@js:`)
2. XPath 规则 (`//` 或 `xpath:`)
3. CSS 选择器 (默认)
4. JSONPath (`$.`)
5. 正则表达式 (`regex:`)

---

## 3. 规则字段详细映射

### 3.1 搜索规则 (ruleSearch)

| 字段 | 功能 | iOS 实现 | 状态 |
|------|------|----------|------|
| bookList | 书籍列表规则 | RuleEngine.execute() | ✅ |
| name | 书名规则 | RuleEngine.execute() | ✅ |
| author | 作者规则 | RuleEngine.execute() | ✅ |
| bookUrl | 书籍URL规则 | RuleEngine.execute() | ✅ |
| coverUrl | 封面URL规则 | RuleEngine.execute() | ✅ |
| intro | 简介规则 | RuleEngine.execute() | ✅ |
| kind | 分类规则 | RuleEngine.execute() | ✅ |
| lastChapter | 最新章节规则 | RuleEngine.execute() | ✅ |
| time | 更新时间规则 | RuleEngine.execute() | ✅ |
| wordCount | 字数规则 | RuleEngine.execute() | ✅ |
| bookComment | 书评规则 | RuleEngine.execute() | ✅ |

### 3.2 发现规则 (ruleExplore)

| 字段 | 功能 | iOS 实现 | 状态 |
|------|------|----------|------|
| bookList | 书籍列表规则 | RuleEngine.execute() | ✅ |
| ... | 同搜索规则 | ... | ✅ |

### 3.3 书籍信息规则 (ruleBookInfo)

| 字段 | 功能 | iOS 实现 | 状态 |
|------|------|----------|------|
| init | 预处理规则 | RuleEngine.executeWithSplit() | ✅ |
| name | 书名规则 | RuleEngine.execute() | ✅ |
| author | 作者规则 | RuleEngine.execute() | ✅ |
| intro | 简介规则 | RuleEngine.execute() | ✅ |
| coverUrl | 封面URL规则 | RuleEngine.execute() | ✅ |
| tocUrl | 目录URL规则 | RuleEngine.execute() | ✅ |
| wordCount | 字数规则 | RuleEngine.execute() | ✅ |
| lastChapter | 最新章节规则 | RuleEngine.execute() | ✅ |
| canReName | 是否可重命名 | RuleEngine.execute() | ✅ |

### 3.4 目录规则 (ruleToc)

| 字段 | 功能 | iOS 实现 | 状态 |
|------|------|----------|------|
| chapterList | 章节列表规则 | RuleEngine.execute() | ✅ |
| chapterName | 章节名规则 | RuleEngine.execute() | ✅ |
| chapterUrl | 章节URL规则 | RuleEngine.execute() | ✅ |
| isVip | VIP标志规则 | RuleEngine.execute() | ✅ |
| isPay | 付费标志规则 | RuleEngine.execute() | ✅ |
| updateTime | 更新时间规则 | RuleEngine.execute() | ✅ |
| nextTocUrl | 下一页目录URL | RuleEngine.execute() | ✅ |

### 3.5 正文规则 (ruleContent)

| 字段 | 功能 | iOS 实现 | 状态 |
|------|------|----------|------|
| content | 正文内容规则 | RuleEngine.execute() | ✅ |
| nextContentUrl | 下一页URL规则 | RuleEngine.execute() | ✅ |
| webJs | WebView注入JS | ❌ | ❌ |
| sourceRegex | 资源正则 | RuleEngine.execute() | ✅ |
| replaceRegex | 替换正则 | ReplaceEngine.apply() | ✅ |
| imageStyle | 图片样式 | ❌ | ❌ |
| payAction | 付费动作 | ❌ | ❌ |

### 3.6 段评规则 (ruleReview)

| 字段 | 功能 | iOS 实现 | 状态 |
|------|------|----------|------|
| reviewList | 段评列表规则 | ❌ | ❌ |
| ... | 其他段评字段 | ❌ | ❌ |

---

## 4. 模板变量系统

### 4.1 内置变量

| 变量 | 功能 | iOS 实现 | 状态 |
|------|------|----------|------|
| `{{key}}` | 搜索关键词 | TemplateEngine | ✅ |
| `{{page}}` | 页码 | TemplateEngine | ✅ |
| `{{page-1}}` | 页码-1 | TemplateEngine | ✅ |
| `{{key,default}}` | 带默认值 | TemplateEngine | ✅ |
| `{{$.jsonPath}}` | JSONPath取值 | TemplateEngine | ✅ |
| `@put,{key,value}` | 变量存储 | TemplateEngine | ✅ |
| `@get,{key}` | 变量读取 | TemplateEngine | ✅ |

### 4.2 书源变量

书源可以定义自定义变量，在规则中使用：
- Android: `source.variable` (JSON 字符串)
- iOS: `source.variable` (JSON 字符串，已对齐)

---

## 5. JS 桥接函数

### 5.1 内置函数

| 函数 | 功能 | iOS 实现 | 状态 |
|------|------|----------|------|
| `baseUrl` | 获取当前URL | JSBridge.baseUrl | ✅ |
| `result` | 上一步结果 | JSBridge.result | ✅ |
| `java` | Java 调用 | ❌ 不支持 | ⚠️ |
| `source` | 书源对象 | JSBridge.source | ✅ |
| `book` | 书籍对象 | JSBridge.book | ✅ |

### 5.2 网络函数

| 函数 | 功能 | iOS 实现 | 状态 |
|------|------|----------|------|
| `ajax(url)` | 发起请求 | JSBridge.ajax | ✅ |
| `get(url)` | GET 请求 | JSBridge.get | ✅ |
| `post(url, body)` | POST 请求 | JSBridge.post | ✅ |

---

## 6. 兼容性测试清单

### 6.1 必须测试的规则类型

- [ ] CSS 选择器规则
- [ ] XPath 规则
- [ ] JSONPath 规则
- [ ] 正则表达式规则
- [ ] JavaScript 规则
- [ ] 混合规则
- [ ] 多值规则（`##` 分隔）
- [ ] 规则链（`@get/@put`）
- [ ] 模板变量替换

### 6.2 必须测试的书源样本

1. 纯 CSS 选择器书源
2. XPath 书源
3. JSON API 书源
4. JavaScript 书源
5. 正则书源
6. 混合规则书源
7. 需要登录的书源
8. 需要 Cookie 的书源

---

## 7. 已知差异

| 差异 | 原因 | 影响 | 处理 |
|------|------|------|------|
| Rhino vs JavaScriptCore | 引擎不同 | 部分高级 JS 特性可能不兼容 | 测试回归 |
| Java 调用 | 平台限制 | 无法使用 `java.*` 类 | 提供替代方案 |
| WebView 注入 | 平台限制 | 正文 `webJs` 规则实现不同 | 使用 WKWebView |

---

## 8. 参考实现

### 8.1 Android 源码

- 规则引擎: `modules/book/src/main/java/io/legado/book/model/analyzeRule/`
- Rhino: `modules/rhino/`
- JS 桥接: `app/src/main/java/io/legado/app/model/SharedJsScope.kt`

### 8.2 iOS 当前实现

- 规则引擎: `Core/RuleEngine/RuleEngine.swift`
- JS 桥接: `Core/RuleEngine/JSBridge.swift`
- 模板引擎: `Core/RuleEngine/TemplateEngine.swift`