# A 股资讯路由预检｜最近一天｜2026-08-24

- intent：`recent`
- 统计窗口：2026-08-24 00:00:00 至 2026-08-24 23:59:59（America/Los_Angeles，PDT）
- as_of：2026-08-24T21:34:16.6413709-07:00
- browseros_state：`unknown`（本次未选 interactive 路线，未调用 BrowserOS）
- allow_browser_fallback：`false`
- 选定路线：`last30days`
- 路由状态：`ready`
- 是否允许继续：`true`

## 必需检查

- `news-ops-skill/tool_doctor.py --json --intent recent`：`route.status=ready`，`route.selected=last30days`。
- `last30days --preflight`：Ready；浏览器 Cookie 读取关闭；无计划写入。
- `last30days --diagnose`：版本 3.14.0，Python 3.14.7；可用来源包括 Reddit、TikTok、Instagram、X、YouTube、Hacker News、Polymarket、GitHub、Brave grounding；X 后端为 xAI，Web 后端为 Brave，YouTube 后端为 yt-dlp。
- `last30days doctor --json`：`permissions.status=ready`、`setup.setup_complete=true`；TikTok/Instagram/Reddit ScrapeCreators、X xAI、YouTube yt-dlp、Hacker News、Polymarket、GitHub 与 Brave 可用。
- `agent-reach doctor --json`：GitHub/YouTube/Reddit/Twitter/Instagram/Bilibili/Xiaohongshu/RSS/Exa/Web 等实际后端状态已保存；雪球为 `warn`（SSL EOF，未作为唯一来源）。

## 运行边界与回退

- 预检阶段未抓取网页、未登录、未读取 Cookie、未安装组件。
- 仅允许在 `ready` 路由继续；不使用未经授权的浏览器降级。
- 所有完整诊断 JSON 与 preflight 文本保存在同目录：`route-report.json`、`tool-doctor.json`、`last30days-preflight.txt`、`last30days-diagnose.json`、`last30days-doctor.json`、`agent-reach-doctor.json`。

