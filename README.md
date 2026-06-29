# nonebot_plugin_speakrank_Baize

群聊发言活跃统计插件，自动记录群消息并生成排行榜图片。

## 功能

- 自动记录群聊发言（含机器人自身消息）
- 支持多种排行查询，生成精美卡片图
- 每日/每周定时自动发送统计
- 活跃趋势折线图（支持自定义天数）
- 可通过 WebUI 直接编辑所有配置项

## 效果预览

### 发言排行榜卡片

<img src="https://raw.githubusercontent.com/sangonomiya249/nonebot_plugin_speakrank_baize/main/screenshots/rank.png" width="400" alt="排行卡片">

### 活跃趋势折线图

<img src="https://raw.githubusercontent.com/sangonomiya249/nonebot_plugin_speakrank_baize/main/screenshots/chart.png" width="400" alt="活跃趋势">

## 命令

| 命令 | 说明 |
|------|------|
| `/今日发言排行` | 本群今日发言排行 |
| `/周发言排行` | 本群近 7 天发言排行 |
| `/月发言排行` | 本群近 30 天发言排行 |
| `/发言排行 <天数>` | 本群近 N 天发言排行（1-365） |
| `/活跃统计 <天数>` | 本群近 N 天每日发言折线图（2-360，默认 7） |
| `/群发言排行 <天数>` | 所有群近 N 天排行（默认 30） |
| `/历史发言排行` | 本群历史总排行 |
| `/群历史发言排行` | 所有群历史总排行 |

## 定时任务

- **每日排行**：每天 23:15 自动发送各群今日发言排行
- **每周趋势**：每周日 23:30 自动发送各群近 7 天活跃折线图

时间可在配置中修改。

## ⚙️ 配置

所有配置项可通过 `.env` 或 WebUI 插件管理修改：

| `.env` 变量 | 默认值 | 说明 |
| ----------- | ------ | ---- |
| `SPEAKRANK_DATA_PATH` | `data/activity_stat` | SQLite 数据库存放目录 |
| `SPEAKRANK_DAILY_RANK_HOUR` | `23` | 每日排行发送：几点触发 (0-23) |
| `SPEAKRANK_DAILY_RANK_MINUTE` | `15` | 每日排行发送：几分触发 (0-59) |
| `SPEAKRANK_WEEKLY_CHART_HOUR` | `23` | 每周趋势图发送：几点触发（仅周日） |
| `SPEAKRANK_WEEKLY_CHART_MINUTE` | `30` | 每周趋势图发送：几分触发 |
| `SPEAKRANK_MAX_DISPLAY_RANK` | `10` | 排行榜最多显示前 N 名 |
| `SPEAKRANK_MAX_QUERY_DAYS` | `365` | 发言排行允许查询的最大天数 |
| `SPEAKRANK_FONT_PATH` | `font.ttf` | 首选字体路径 |
| `SPEAKRANK_RANK_IMAGE_WIDTH` | `1080` | 排行榜图片宽度 |
| `SPEAKRANK_RANK_IMAGE_HEIGHT` | `1260` | 排行榜图片高度 |
| `SPEAKRANK_DAILY_QUOTE_URL` | 一言 API | 图片底部每日语录 API |
| `SPEAKRANK_DAILY_QUOTE_MAX_LENGTH` | `34` | 语录最大显示字数 |

完整列表见 [config.py](config.py)。

## 字体

将任意 `.ttf` 中文字体放到插件目录下，命名为 `font.ttf` 即可自动加载。未找到时自动回退到系统字体（微软雅黑 / 文泉驿 / PingFang）。

## 依赖

- `nonebot_plugin_apscheduler`
- `Pillow` (PIL)
- `aiosqlite`
- `httpx`
