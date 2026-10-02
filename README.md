# Prompt Vault · 提示词管理器

一个**单文件**的 Prompt 管理工具：整个应用只有 `index.html`，HTML / CSS / JS 全部内联，零依赖、零构建、零网络请求。

## 特性

- **左列表右编辑**：搜索框 + 标签筛选下拉，每条显示标题、标签、收藏星标，收藏项自动置顶
- **变量占位符**：正文里写 `{{变量名}}`，自动生成对应输入框；填值后实时渲染最终 Prompt，一键复制
- **顶部工具栏**：新建 / 删除 / 导出 JSON / 导入 JSON
- **本地持久化**：数据存在浏览器 `localStorage`，键名 `prompt_vault_v1`，刷新不丢
- **首次打开**：预置「代码审查」「周报生成」「SQL 优化」三条示例
- **深色主题**：配色由 CSS 变量统一管理，窗口宽度 < 768px 自动切换为上下布局

## 使用

双击 `index.html` 即可，无需任何服务器或安装步骤。

> 数据只保存在当前浏览器本地，不会上传到任何地方。换电脑请用「导出 JSON」迁移。

## 快捷键

| 快捷键 | 功能 |
| --- | --- |
| `Ctrl/Cmd + S` | 立即保存到本机 |
| `Ctrl/Cmd + K` | 聚焦搜索框 |
| `Esc` | 清空搜索（搜索框聚焦时） |

## 部署到 GitHub Pages

推送到 `main` 分支后，在仓库 **Settings → Pages → Source 选 `Deploy from a branch` → 分支选 `main` / 目录选 `/ (root)`** 即可。

访问地址：<https://user-yang11.github.io/prompt-vault/>

## 架构说明

- 全局只有**一个** `state` 对象，所有界面变化都走 `render()` 系列函数，事件回调只负责「改 state → 调 render」
- 为保住输入光标，`render` 拆成 `renderList` / `renderEditor` / `renderVars` / `renderPreview` / `renderTagOptions`，输入时只重绘受影响的那一块
- 纯原生 ES6+，未使用任何框架或第三方库
