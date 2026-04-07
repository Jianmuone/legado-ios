# Legado iOS Migration - API Map

> 本文档记录 Android Legado API 到 iOS 的映射关系。
> 
> **生成日期**: 2026-04-08

---

## 1. URL Scheme

### 1.1 导入协议

```
legado://import/{path}?src={url}
```

| path | 用途 | iOS 实现 | 状态 |
|------|------|----------|------|
| `/bookSource` | 导入书源 | `URLSchemeHandler` | ⏳ 待迁移 |
| `/rssSource` | 导入订阅源 | `URLSchemeHandler` | ⏳ 待迁移 |
| `/replaceRule` | 导入替换规则 | `URLSchemeHandler` | ⏳ 待迁移 |
| `/textTocRule` | 导入 TXT 目录规则 | `URLSchemeHandler` | ⏳ 待迁移 |
| `/httpTTS` | 导入 HTTP TTS | `URLSchemeHandler` | ⏳ 待迁移 |
| `/dictRule` | 导入字典规则 | `URLSchemeHandler` | ⏳ 待迁移 |
| `/theme` | 导入主题 | `URLSchemeHandler` | ⏳ 待迁移 |
| `/readConfig` | 导入阅读配置 | `URLSchemeHandler` | ⏳ 待迁移 |
| `/addToBookshelf` | 添加到书架 | `URLSchemeHandler` | ⏳ 待迁移 |
| `/importonline` | 在线导入（自动识别） | `URLSchemeHandler` | ⏳ 待迁移 |

### 1.2 iOS 实现

```swift
// Core/URLScheme/URLSchemeHandler.swift
class URLSchemeHandler {
    func handle(url: URL) -> Bool {
        guard let scheme = url.scheme, scheme == "legado" else { return false }
        guard let host = url.host, host == "import" else { return false }
        
        let path = url.path
        let src = URLQueryItem(name: "src", value: url.queryItems?.first?.value)
        
        switch path {
        case "/bookSource":
            showImportBookSource(url: src)
        case "/rssSource":
            showImportRssSource(url: src)
        // ...
        }
        
        return true
    }
}
```

### 1.3 Info.plist 配置

```xml
<key>CFBundleURLTypes</key>
<array>
    <dict>
        <key>CFBundleURLSchemes</key>
        <array>
            <string>legado</string>
        </array>
    </dict>
</array>
```

---

## 2. HTTP API

### 2.1 端点列表

#### 书源管理

| 端点 | Method | 用途 | iOS 实现 |
|------|--------|------|----------|
| `/saveBookSource` | POST | 保存单个书源 | `WebServer` |
| `/saveBookSources` | POST | 保存多个书源 | `WebServer` |
| `/getBookSource` | GET | 获取书源 | `WebServer` |
| `/getBookSources` | GET | 获取所有书源 | `WebServer` |
| `/deleteBookSources` | POST | 删除书源 | `WebServer` |

#### 订阅源管理

| 端点 | Method | 用途 | iOS 实现 |
|------|--------|------|----------|
| `/saveRssSource` | POST | 保存订阅源 | `WebServer` |
| `/saveRssSources` | POST | 保存多个订阅源 | `WebServer` |
| `/getRssSource` | GET | 获取订阅源 | `WebServer` |
| `/getRssSources` | GET | 获取所有订阅源 | `WebServer` |
| `/deleteRssSources` | POST | 删除订阅源 | `WebServer` |

#### 替换规则管理

| 端点 | Method | 用途 | iOS 实现 |
|------|--------|------|----------|
| `/getReplaceRules` | GET | 获取替换规则 | `WebServer` |
| `/saveReplaceRule` | POST | 保存替换规则 | `WebServer` |
| `/deleteReplaceRule` | POST | 删除替换规则 | `WebServer` |
| `/testReplaceRule` | POST | 测试替换规则 | `WebServer` |

#### 书籍管理

| 端点 | Method | 用途 | iOS 实现 |
|------|--------|------|----------|
| `/saveBook` | POST | 保存书籍 | `WebServer` |
| `/deleteBook` | POST | 删除书籍 | `WebServer` |
| `/getBookshelf` | GET | 获取书架 | `WebServer` |
| `/getChapterList` | GET | 获取章节列表 | `WebServer` |
| `/getBookContent` | GET | 获取正文 | `WebServer` |
| `/cover` | GET | 获取封面 | `WebServer` |
| `/image` | GET | 获取图片 | `WebServer` |
| `/saveBookProgress` | POST | 保存阅读进度 | `WebServer` |

### 2.2 iOS WebServer 实现

```swift
// Core/WebServer/WebServer.swift
import Swifter

class WebServer {
    private let server = HttpServer()
    
    func start(port: Int = 1234) throws {
        // 书源管理
        server["/saveBookSource"] = { request in
            let source = try JSONDecoder().decode(BookSource.self, from: request.body)
            BookSourceRepository.shared.save(source)
            return .ok(.text("success"))
        }
        
        server["/getBookSources"] = { _ in
            let sources = BookSourceRepository.shared.getAll()
            let data = try JSONEncoder().encode(sources)
            return .ok(.data(data))
        }
        
        // ... 其他端点
        
        try server.start(in_port_t(port))
    }
}
```

---

## 3. WebSocket API

### 3.1 端点列表

| 端点 | 用途 | 消息格式 | iOS 实现 |
|------|------|----------|----------|
| `/bookSourceDebug` | 调试书源 | `{"key": "关键词", "tag": "书源URL"}` | `WebSocketServer` |
| `/rssSourceDebug` | 调试订阅源 | `{"key": "关键词", "tag": "订阅源URL"}` | `WebSocketServer` |
| `/searchBook` | 搜索书籍 | `{"key": "关键词"}` | `WebSocketServer` |

### 3.2 iOS WebSocket 实现

```swift
// Core/WebSocket/DebugWebSocket.swift
import Starscream

class BookSourceDebugSocket: WebSocketDelegate {
    private var socket: WebSocket?
    
    func connect(port: Int = 1235) {
        let url = URL(string: "ws://127.0.0.1:\(port)/bookSourceDebug")!
        socket = WebSocket(request: URLRequest(url: url))
        socket?.delegate = self
        socket?.connect()
    }
    
    func debug(key: String, sourceUrl: String) {
        let message: [String: Any] = ["key": key, "tag": sourceUrl]
        let data = try! JSONSerialization.data(withJSONObject: message)
        socket?.write(data: data)
    }
    
    func didReceive(event: WebSocketEvent, client: WebSocket) {
        switch event {
        case .text(let string):
            // 处理调试输出
            print("Debug output: \(string)")
        default:
            break
        }
    }
}
```

---

## 4. Content Provider 替代方案

### 4.1 Android Content Provider 能力

- 外部应用批量查询书源/书籍
- 外部应用批量写入书源/书籍
- 跨应用数据同步

### 4.2 iOS 替代方案

| Android 能力 | iOS 替代方案 | 说明 |
|--------------|--------------|------|
| Content Provider | URL Scheme | 单次导入 |
| Content Provider | Share Extension | 从其他应用分享导入 |
| Content Provider | App Group | 跨应用数据共享 |
| Content Provider | HTTP API | 批量操作 |

### 4.3 App Group 实现

```swift
// Core/AppGroup/AppGroupManager.swift
class AppGroupManager {
    static let shared = AppGroupManager()
    
    let containerURL: URL? = FileManager.default
        .containerURL(forSecurityApplicationGroupIdentifier: "group.com.legado.ios")
    
    func sharedDefaults() -> UserDefaults? {
        return UserDefaults(suiteName: "group.com.legado.ios")
    }
}
```

---

## 5. Share Extension

### 5.1 导入入口

从其他应用分享内容到 Legado：

| 分享类型 | 处理逻辑 |
|----------|----------|
| 文本 | 检测是否为书源 JSON |
| URL | 检测是否为书源/订阅源 URL |
| 文件 | 检测是否为书籍文件 |

### 5.2 Info.plist 配置

```xml
<key>NSExtension</key>
<dict>
    <key>NSExtensionAttributes</key>
    <dict>
        <key>NSExtensionActivationRule</key>
        <dict>
            <key>NSExtensionActivationSupportsText</key>
            <true/>
            <key>NSExtensionActivationSupportsWebURLWithMaxCount</key>
            <integer>1</integer>
            <key>NSExtensionActivationSupportsFileWithMaxCount</key>
            <integer>1</integer>
        </dict>
    </dict>
</dict>
```

---

## 6. 外部调用能力对照

| Android | iOS | 兼容性 |
|---------|-----|--------|
| `legado://import/bookSource?src=xxx` | ✅ 完全支持 | 100% |
| Content Provider 查询 | HTTP API `/getBookSources` | 90% |
| Content Provider 写入 | HTTP API `/saveBookSource` | 90% |
| Intent Filter 导入 | Share Extension | 95% |
| 快捷方式 | Siri Shortcuts | 待实现 |

---

## 7. 差异白名单

| 差异项 | Android | iOS | 原因 | 替代方案 |
|--------|---------|-----|------|----------|
| Content Provider | ✅ | ❌ | iOS 不支持 | HTTP API + App Group |
| 快捷方式 | ShortcutManager | Siri Shortcuts | 平台差异 | Shortcuts.app 集成 |

---

*本文档由 Wave 0 基线采集自动生成*