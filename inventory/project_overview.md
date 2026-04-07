# Legado iOS Migration - Project Overview

> 本文档为 Android Legado 到 iOS 原生严格 1:1 迁移项目的总览文档。
> 
> **生成日期**: 2026-04-08
> **Android 源码版本**: https://github.com/gedoor/legado (commit: a694b9c)

---

## 1. Android 工程模块清单

| 模块 | 路径 | 职责 |
|------|------|------|
| **app** | `/app` | 主应用模块，包含 UI、业务逻辑、数据库、服务 |
| **book** | `/modules/book` | 书籍解析库，处理 EPUB、TXT、PDF、MOBI 格式 |
| **rhino** | `/modules/rhino` | Rhino JS 引擎模块，执行书源规则脚本 |
| **web** | `/modules/web` | Web 界面模块，Vue.js 构建的书源编辑器 |

---

## 2. 根模块职责

### app 模块分层架构

| 层级 | 目录 | 职责 |
|------|------|------|
| **api** | `api/` | HTTP/WebSocket API 控制器，外部调用入口 |
| **base** | `base/` | Activity/Fragment/ViewModel 基类 |
| **constant** | `constant/` | 应用常量定义 |
| **data** | `data/` | 数据库、DAO、实体类 |
| **exception** | `exception/` | 异常处理 |
| **help** | `help/` | 辅助工具类 |
| **lib** | `lib/` | 第三方库集成 |
| **model** | `model/` | 业务模型，书籍解析、规则执行 |
| **receiver** | `receiver/` | 广播接收器 |
| **service** | `service/` | 后台服务 |
| **ui** | `ui/` | 所有界面组件 |
| **utils** | `utils/` | 工具函数 |
| **web** | `web/` | Web 服务 |

---

## 3. modules:book 职责

书籍解析库模块，提供统一的书内容读取接口：

| 类 | 职责 |
|------|------|
| `LocalBook` | 本地书籍解析入口 |
| `EpubFile` | EPUB 格式解析 |
| `TxtFile` | TXT 格式解析 |
| `PdfFile` | PDF 格式解析 |
| `MobiFile` | MOBI 格式解析 |
| `BookHelp` | 书籍缓存管理 |
| `ImageProvider` | 图片缓存和获取 |

---

## 4. modules:rhino 职责

Rhino JS 引擎模块，用于执行书源规则中的 JavaScript 代码：

| 功能 | 说明 |
|------|------|
| JS 执行环境 | 提供沙箱化的 JS 运行环境 |
| JS 库支持 | 支持自定义 JS 库 |
| 异常处理 | JS 执行错误捕获和日志 |
| 超时控制 | 防止 JS 死循环 |

---

## 5. 迁移总策略

### 5.1 核心原则

1. **严格 1:1 迁移** - 不允许功能删减或简化
2. **对照复刻** - 基于 Android 源码精确移植
3. **产品语义一致** - 保持用户操作习惯
4. **规则兼容** - 确保书源/订阅源/替换规则完全兼容

### 5.2 迁移优先级

| 优先级 | 模块 | 说明 |
|--------|------|------|
| P0 | 数据层 | 实体、DAO、CoreData |
| P0 | 规则引擎 | AnalyzeRule、JS 执行 |
| P0 | 阅读器核心 | 分页、排版、翻页 |
| P1 | 书架管理 | 书籍列表、分组、搜索 |
| P1 | 书源管理 | 导入、编辑、调试 |
| P2 | RSS 订阅 | 订阅源、文章阅读 |
| P3 | 配置与设置 | 主题、字体、备份 |

---

## 6. iOS 技术选型

| 领域 | 技术选型 | 说明 |
|------|----------|------|
| **语言** | Swift | 原生开发 |
| **UI** | UIKit + Auto Layout | 不使用 SwiftUI |
| **架构** | Feature-based Modular | 按功能模块划分 |
| **数据存储** | SQLite + CoreData | 对齐 Android Room |
| **网络** | URLSession | 自定义 Cookie/重试/缓存 |
| **规则引擎** | JavaScriptCore | 替代 Rhino |
| **HTML 解析** | SwiftSoup | 替代 Jsoup |
| **XPath** | Fuzi/Kanna | XPath 解析 |
| **阅读引擎** | TextKit 2 + CoreText | 分页排版 |
| **音视频** | AVFoundation | 播放控制 |
| **扫码** | AVFoundation | 二维码扫描 |
| **导入** | URL Scheme + Share Extension | 外部调用 |

---

## 7. 风险点

| 风险 | 影响 | 缓解措施 |
|------|------|----------|
| **Rhino → JavaScriptCore** | JS 行为差异 | 建立回归测试集 |
| **XPath 兼容性** | 规则解析差异 | 使用标准 XPath 库 |
| **TextKit 2 复杂度** | 阅读器开发周期 | 优先实现核心功能 |
| **Content Provider 替代** | 外部调用能力 | URL Scheme + HTTP API |
| **多语言资源** | 字符串对齐 | 严格对照 values 目录 |

---

## 8. 验收方式

### 8.1 功能验收

- [ ] 页面覆盖率 100%
- [ ] 功能覆盖率 100%
- [ ] 配置项覆盖率 100%

### 8.2 兼容性验收

- [ ] 书源导入/导出格式兼容
- [ ] 订阅源导入/导出格式兼容
- [ ] 替换规则导入/导出格式兼容
- [ ] URL Scheme 兼容
- [ ] HTTP API 兼容

### 8.3 体验验收

- [ ] Android/iOS 截图对照
- [ ] 操作路径对照
- [ ] 夜间模式对照
- [ ] 横屏模式对照
- [ ] 多语言对照

---

## 9. 文档清单

| 文档 | 用途 | 状态 |
|------|------|------|
| `project_overview.md` | 项目总览 | ✅ 已完成 |
| `module_map.md` | 模块映射 | 待生成 |
| `page_map.md` | 页面映射 | 待生成 |
| `data_map.md` | 数据映射 | 待生成 |
| `api_map.md` | API 映射 | 待生成 |
| `rule_engine_map.md` | 规则引擎映射 | 待生成 |
| `resource_map.md` | 资源映射 | 待生成 |
| `platform_diff_whitelist.md` | 平台差异白名单 | 待生成 |
| `acceptance_matrix.md` | 验收矩阵 | 待生成 |

---

## 10. Wave 规划

| Wave | 目标 | 状态 |
|------|------|------|
| **Wave 0** | 基线采集 | 🔄 进行中 |
| **Wave 1** | 工程骨架与基础设施 | 待开始 |
| **Wave 2** | App 骨架页 | 待开始 |
| **Wave 3** | 书架与书籍管理 | 待开始 |
| **Wave 4** | 搜索/发现/书源 | 待开始 |
| **Wave 5** | 阅读器核心 | 待开始 |
| **Wave 6** | RSS/订阅域 | 待开始 |
| **Wave 7** | 替换净化/字典/字体等 | 待开始 |
| **Wave 8** | 接口兼容与外部唤起 | 待开始 |
| **Wave 9** | 回归、比对、收尾 | 待开始 |

---

*本文档由 Wave 0 基线采集自动生成*