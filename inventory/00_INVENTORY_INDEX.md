# Legado iOS 迁移盘点索引

**状态**: Wave 2 App 骨架页 ✅  
**创建时间**: 2026-04-08  
**目标**: 将 Android 开源项目 Luoyacheng/legado 严格 1:1 移植到 iOS 原生实现  
**最新构建**: Run 24098731438 (Wave 2)

---

## 盘点文档清单

| 文档 | 状态 | 描述 |
|------|------|------|
| [01_project_overview.md](./01_project_overview.md) | ✅ 完成 | 项目概述、模块职责、技术选型 |
| [02_module_map.md](./02_module_map.md) | ✅ 完成 | Android -> iOS 模块映射 |
| [03_page_map.md](./03_page_map.md) | 🔄 进行中 | 页面映射表（最重要） |
| [04_data_map.md](./04_data_map.md) | ✅ 完成 | 数据实体映射 |
| [05_api_map.md](./05_api_map.md) | ✅ 完成 | HTTP/WebSocket/URL Scheme API 映射 |
| [06_rule_engine_map.md](./06_rule_engine_map.md) | ✅ 完成 | 规则引擎架构映射 |
| [07_resource_map.md](./07_resource_map.md) | 🔄 进行中 | 布局/资源映射 |
| [08_platform_diff_whitelist.md](./08_platform_diff_whitelist.md) | ✅ 完成 | 平台差异白名单 |
| [09_acceptance_matrix.md](./09_acceptance_matrix.md) | ✅ 完成 | 验收矩阵 |

---

## 核心约束

### 迁移原则

1. **严格一比一** - 逐行对照 Android 原版代码移植
2. **不允许功能删减、合并、简化**
3. **产品语义一致，不是功能类似即可**
4. **页面结构、层级、布局、控件位置、文案、交互路径必须一致**

### 禁止事项

- ❌ 为了"更符合 iOS 习惯"擅自改交互
- ❌ 为了"更美观"擅自改布局
- ❌ 为了"更现代"擅自改信息架构
- ❌ 为了"时间紧"删掉长尾功能
- ❌ 把 Android 的两个页面合并成一个 iOS 页面
- ❌ 把多级菜单扁平化
- ❌ 做 MVP 或"以后再补"

### 真相来源优先级

| 优先级 | 来源 |
|--------|------|
| P0 | Android 原仓库源码、资源文件、页面目录结构、配置项、菜单弹窗 |
| P1 | Android 原项目 README/api.md、运行时行为、截图录屏 |
| P2 | iOS 平台实现细节、UIKit/Auto Layout/TextKit 等 |

---

## 统计概览

### Android 项目规模

- **UI 页面目录**: 18 个主目录 + 40+ 子目录
- **布局文件**: 100+ 个 XML
- **数据实体**: 30 个
- **API 接口**: 25+ 个 HTTP + WebSocket + Content Provider

### iOS 当前状态

- **CoreData 实体**: 19 个
- **Swift 文件**: 100+ 个
- **功能覆盖**: 约 60%

### 差距分析

详见 [09_acceptance_matrix.md](./09_acceptance_matrix.md)

---

## 开发波次

| Wave | 目标 | 状态 |
|------|------|------|
| Wave 0 | 基线采集 | ✅ 完成 |
| Wave 1 | 工程骨架与基础设施 | ✅ 完成 |
| Wave 2 | App 骨架页 | ✅ 完成 |
| Wave 3 | 书架与书籍管理 | 🔄 待开始 |
| Wave 4 | 搜索/发现/书源 | ⏳ 待开始 |
| Wave 5 | 阅读器核心 | ⏳ 待开始 |
| Wave 6 | RSS/订阅域 | ⏳ 待开始 |
| Wave 7 | 替换净化/字典/字体/二维码/浏览器/视频/登录/插件 | ⏳ 待开始 |
| Wave 8 | 接口兼容与外部唤起 | ⏳ 待开始 |
| Wave 9 | 回归、比对、收尾 | ⏳ 待开始 |

---

## 下一步

开始 Wave 3: 书架与书籍管理