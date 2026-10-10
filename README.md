# Todo List + 电脑活动记录

一个单文件的个人效率工具，结合了待办事项、日历日程和 macOS 电脑活动记录。

## 功能

**首页**
- 显示当前时间、日期、实时天气（支持多国家/省份切换）
- 近期安排预览，支持内联编辑
- 日间/夜间主题切换

**日历页**
- 月历视图，有日程的日期显示小圆点
- 查看任意一天的待办事项
- 查看当天的电脑使用作息（需配合 `activity_tracker.py`）

**待办页**
- 按日期管理任务，添加/完成/删除
- 记录添加时间和完成时间
- 数据存在 `localStorage`，刷新不丢

**近期安排页**
- 创建/编辑/完成/删除安排项目
- 支持自由文本备注
- 可隐藏不想在首页显示的安排

**电脑活动记录**（需运行 `activity_tracker.py`）
- 每 5 秒记录一次当前前台软件
- 5 分钟无操作自动标记为离开
- 按天存为 `activity_log/YYYY-MM-DD.json`
- 在日历页可查看任意一天的使用时间线

## 使用方法

### 只用 Todo 功能

直接用浏览器打开 `index.html` 即可，不需要任何依赖。

### 开启电脑活动记录（此功能还在开发中，暂未开放使用）

需要 macOS，Python 3（系统自带，无需额外安装）。

```bash
python3 activity_tracker.py
```

然后用浏览器打开 http://127.0.0.1:8765

按 `Ctrl+C` 停止记录。

> 直接打开 `index.html` 文件时，活动记录功能不可用（浏览器安全限制），需通过 `http://127.0.0.1:8765` 访问才能连接到记录程序。

## 文件结构

```
todo_list/
├── index.html              # 主页面（单文件，所有功能都在这里）
├── activity_tracker.py     # macOS 电脑活动记录后台 + 本地 HTTP 服务器
└── activity_log/           # 每天的活动记录
    └── YYYY-MM-DD.json
```

## API

`activity_tracker.py` 提供两个本地接口（仅 127.0.0.1 可访问）：

| 方法 | 路径 | 说明 |
|------|------|------|
| GET | `/api/activity` | 获取今天的活动记录 |
| GET | `/api/activity?date=YYYY-MM-DD` | 获取指定日期的记录 |
| POST | `/api/activity/clear` | 清空今天的记录 |

## 依赖

- Python 标准库（无需 pip install）
- 现代浏览器
- macOS（活动记录功能依赖 `lsappinfo` 和 `ioreg` 命令）
