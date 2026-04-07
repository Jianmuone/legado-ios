# API 映射 (API Map)

**创建时间**: 2026-04-08

---

## 1. URL Scheme 映射

### 1.1 基础格式

**格式**: `legado://import/{path}?src={url}`

### 1.2 支持的路径

| 路径 | 功能 | iOS 实现 | 状态 |
|------|------|----------|------|
| `/bookSource` | 书源导入 | URLSchemeHandler | ✅ |
| `/rssSource` | 订阅源导入 | URLSchemeHandler | ✅ |
| `/replaceRule` | 替换规则导入 | URLSchemeHandler | ✅ |
| `/textTocRule` | TXT 目录规则导入 | URLSchemeHandler | ❌ |
| `/httpTTS` | 在线朗读引擎导入 | URLSchemeHandler | ✅ |
| `/theme` | 主题导入 | URLSchemeHandler | ❌ |
| `/readConfig` | 阅读排版导入 | URLSchemeHandler | ❌ |
| `/dictRule` | 字典规则导入 | URLSchemeHandler | ✅ |
| `/addToBookshelf` | 添加到书架 | URLSchemeHandler | ❌ |
| `/importonline` | 自动识别导入 | URLSchemeHandler | ✅ |

### 1.3 iOS 实现方式

```swift
// Info.plist 配置
<key>CFBundleURLTypes</key>
<array>
    <dict>
        <key>CFBundleURLSchemes</key>
        <array>
            <string>legado</string>
        </array>
    </dict>
</array>

// AppDelegate 处理
func application(_ app: UIApplication, open url: URL, options: [UIApplication.OpenURLOptionsKey: Any] = [:]) -> Bool {
    return URLSchemeHandler.shared.handle(url)
}
```

---

## 2. 本地 HTTP API 映射

### 2.1 书源管理接口

| 接口 | Method | 路径 | iOS 实现 | 状态 |
|------|--------|------|----------|------|
| 插入单个书源 | POST | `/saveBookSource` | BookSourceAPI.saveSource() | ✅ |
| 插入多个书源 | POST | `/saveBookSources` | BookSourceAPI.saveSources() | ✅ |
| 获取书源 | GET | `/getBookSource?url=xxx` | BookSourceAPI.getSource() | ✅ |
| 获取所有书源 | GET | `/getBookSources` | BookSourceAPI.getSources() | ✅ |
| 删除多个书源 | POST | `/deleteBookSources` | BookSourceAPI.deleteSources() | ✅ |

### 2.2 订阅源管理接口

| 接口 | Method | 路径 | iOS 实现 | 状态 |
|------|--------|------|----------|------|
| 插入多个订阅源 | POST | `/saveRssSources` | ❌ | ❌ |
| 获取订阅源 | GET | `/getRssSource?url=xxx` | ❌ | ❌ |
| 获取所有订阅源 | GET | `/getRssSources` | ❌ | ❌ |
| 删除多个订阅源 | POST | `/deleteRssSources` | ❌ | ❌ |

### 2.3 替换规则管理接口

| 接口 | Method | 路径 | iOS 实现 | 状态 |
|------|--------|------|----------|------|
| 获取替换规则 | GET | `/getReplaceRules` | ❌ | ❌ |
| 删除替换规则 | POST | `/deleteReplaceRule` | ❌ | ❌ |
| 插入替换规则 | POST | `/saveReplaceRule` | ❌ | ❌ |
| 测试替换规则 | POST | `/testReplaceRule` | ❌ | ❌ |

### 2.4 书籍管理接口

| 接口 | Method | 路径 | iOS 实现 | 状态 |
|------|--------|------|----------|------|
| 插入书籍 | POST | `/saveBook` | BookAPI.saveBook() | ✅ |
| 删除书籍 | POST | `/deleteBook` | BookAPI.deleteBook() | ✅ |
| 获取所有书籍 | GET | `/getBookshelf` | BookAPI.getBookshelf() | ✅ |
| 获取章节列表 | GET | `/getChapterList?url=xxx` | BookAPI.getChapterList() | ✅ |
| 获取书籍内容 | GET | `/getBookContent?url=xxx&index=1` | BookAPI.getBookContent() | ✅ |
| 获取封面 | GET | `/cover?path=xxx` | BookAPI.getCover() | ✅ |
| 获取正文图片 | GET | `/image?url=&path=&width=` | ❌ | ❌ |
| 保存书籍进度 | POST | `/saveBookProgress` | BookAPI.saveBookProgress() | ✅ |

### 2.5 调试接口

| 接口 | Protocol | 路径 | iOS 实现 | 状态 |
|------|----------|------|----------|------|
| 书源调试 | WebSocket | `/bookSourceDebug` | ❌ | ❌ |
| 订阅源调试 | WebSocket | `/rssSourceDebug` | ❌ | ❌ |
| 搜索在线书籍 | WebSocket | `/searchBook` | ❌ | ❌ |

---

## 3. Content Provider 替代方案

### 3.1 平台差异

Android 使用 Content Provider 实现：
- 外部应用查询/写入书籍、书源数据
- 跨应用数据共享

iOS 无法原样实现 Content Provider，需要替代方案。

### 3.2 iOS 替代方案

| Android 能力 | iOS 替代方案 | 说明 |
|--------------|--------------|------|
| `content://.../bookSource/insert` | URL Scheme + 本地 HTTP API | 功能等价 |
| `content://.../bookSource/query` | 本地 HTTP API `/getBookSource` | 功能等价 |
| `content://.../books/query` | 本地 HTTP API `/getBookshelf` | 功能等价 |
| 跨应用数据共享 | App Group + 本地 HTTP | 语义一致 |

### 3.3 差异白名单

详见 `08_platform_diff_whitelist.md`

---

## 4. WebSocket 接口

### 4.1 书源调试接口

**Android 实现**:
```
URL: ws://127.0.0.1:1235/bookSourceDebug
Message: { key: String, tag: String }
```

**iOS 实现**: 需要使用 URLSessionWebSocketTask

### 4.2 搜索在线书籍

**Android 实现**:
```
URL: ws://127.0.0.1:1235/searchBook
Message: { key: String }
```

**iOS 实现**: 需要使用 URLSessionWebSocketTask

---

## 5. 兼容性要点

### 5.1 必须兼容

- ✅ URL Scheme 所有路径
- ✅ HTTP API 请求/响应格式
- ✅ JSON 数据格式
- ✅ 端口号（1234/1235）

### 5.2 待实现

- ❌ WebSocket 调试接口
- ❌ 订阅源 HTTP API
- ❌ 替换规则 HTTP API
- ❌ 正文图片代理

---

## 6. 参考实现

### 6.1 Android 源码

- HTTP API: `app/src/main/java/io/legado/app/web/`
- WebSocket: `app/src/main/java/io/legado/app/web/source/`
- URL Scheme: `app/src/main/java/io/legado/app/ui/association/`

### 6.2 iOS 当前实现

- HTTP Server: `Core/WebServer/WebServerCoordinator.swift`
- URL Scheme: `Core/Import/URLSchemeHandler.swift`
- API Handler: `Core/API/`