##🛡️ Campus Intel | 校园情报收割者 V4.4

"Turn Chaos into Order."

一个基于 Python + DeepSeek + NapCat 的全自动校园情报聚合系统。
专为 “每日仅开机 1 小时” 的极简主义者设计。

![alt text](https://img.shields.io/badge/Python-3.12-blue?logo=python&logoColor=white)


![alt text](https://img.shields.io/badge/AI-DeepSeek%20V3-blueviolet)


![alt text](https://img.shields.io/badge/Protocol-OneBot11-green)


![alt text](https://img.shields.io/badge/Build-Modular-orange)

#📖 项目背景 (Background)

作为一名设计专业的学生，我每天只有 22:00 - 23:00 会打开电脑。但我所在的十几个 QQ 群（班级、社团、竞赛）全天都在产生海量的碎片化信息。

痛点：

信息过载：几千条未读消息，爬楼太累，容易漏掉重要通知。

时效性差：关机期间错过的消息，普通的机器人无法补录。

整理繁琐：手动把讲座时间填入日历非常浪费生命。

解决方案：
Project Harvester (收割者) —— 一个主动式的情报抓取系统。它利用我开机的这 1 小时，自动回溯过去 24~72 小时的所有群消息，利用 DeepSeek 大模型进行语义分析，清洗出结构化的情报，并生成可视化仪表盘。

#✨ 核心功能 (Features)

🕵️‍♂️ 主动收割 (Active Polling)

不依赖实时在线。脚本启动后，主动向 QQ 客户端 (NapCat) 拉取指定群组的历史记录。

支持自定义回溯时间（如：抓取过去 30 小时内的消息）。

#🧠 AI 语义分析 (DeepSeek Powered)

利用 DeepSeek-V3 模型，剔除闲聊、表情包和无效复读。

四大象限分类法：

🔴 学业必修 (考试/截止/作业)

🟠 竞赛项目 (互联网+/大创/组队)

🟢 二课志愿 (讲座/时长)

🔵 休闲活动 (社团/失物/闲聊)

📊 动态仪表盘 (Interactive Dashboard)

自动生成 HTML 网页，支持 时间轴/分类 双视图切换。

时间流布局：情报广场按收录时间倒序，配备彩色分类标签。

来源溯源：每一条情报都标注了来源群组，方便回查。

#☁️ 云端同步 (Cloud Sync)

自动将生成的报告部署到 GitHub Pages。

移动端交付：关机后，依然可以通过手机浏览器随时查看今日情报。

#📅 日历集成

一键生成 .ics 文件，直接导入 iOS/Android 系统日历。

#🏗️ 技术架构 (Architecture)
code
Mermaid
download
content_copy
expand_less
graph LR
    A[QQ 群聊] -->|NapCat HTTP API| B(Python 收割者)
    B -->|Raw Text| C{DeepSeek V3}
    C -->|JSON Data| B
    B -->|生成| D[database.json]
    D -->|渲染| E[Dashboard.html]
    D -->|打包| F[.ics 日历]
    E -->|PyGithub| G[GitHub Pages]
    G -->|访问| H[📱 手机端]
核心模块

main.py: 指挥中心。负责参数配置、多模块调度、云端部署。

backend.py: 逻辑核心。负责多线程数据抓取、去重清洗、AI 接口调用（含动态进度条交互）。

frontend.py: 视觉呈现。负责生成带 JS 交互的 HTML 报告和 ICS 文件。

deployer.py: 物流系统。负责将产物自动 Push 到 GitHub 仓库。

#🚀 快速开始 (Quick Start)

注意：本项目依赖本地 QQ 客户端环境。

环境准备

安装 Python 3.12+。

部署 NapCatQQ 并开启 HTTP 服务端口 (3000)。

安装依赖

code
Bash
download
content_copy
expand_less
pip install requests openai ics PyGithub

配置密钥

在 main.py 中填入你的：

API_KEY: DeepSeek API Key

GITHUB_TOKEN: GitHub Personal Access Token

GROUPS: 需要监听的群号列表

一键运行

双击 开始收割.bat。

输入你想回溯的小时数（默认 30h）。

等待“收割”完成，网页自动弹出。

#⚠️ 隐私说明 (Privacy)

本项目是一个 本地优先 (Local-First) 的工具。

所有聊天记录仅在 本地电脑 与 DeepSeek API 之间传输。

生成的网页虽然托管于 GitHub，但仅包含提取后的脱敏/摘要信息，不包含原始聊天记录。

请勿将包含真实 API Key 的 main.py 上传到公开仓库！ (建议使用环境变量或 .gitignore)。

#🗺️ 未来计划 (Roadmap)

V4.4: 模块化重构、云端同步、交互式网页。

V5.0: 电子义眼。接入 Qwen-VL 视觉模型，识别群聊海报中的文字信息。

V5.x: 智能黑名单。自动屏蔽特定“话痨”用户的无效发言。

#👨‍💻 Author

10Lollipop
Tech-savvy Designer / 2025级设计系

# 💖 致谢 (Acknowledgments)

本项目站在了巨人的肩膀上。特别感谢以下开源项目提供的底层支持：

*   **[NapCatQQ](https://github.com/NapNeko/NapCatQQ)**: 
    提供了稳定、高效的无头 QQ 客户端 (基于 NTQQ)，是本项目获取情报的基石。
    *Without NapCat, this project would be deaf.*

*   **[Streamlit](https://streamlit.io/)** & **[Ics.py](https://icspy.readthedocs.io/)**:
    提供了优秀的数据可视化与日历生成方案。
