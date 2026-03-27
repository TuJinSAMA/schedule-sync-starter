# 🦐 Schedule Sync Starter

一套完整的 OpenClaw Agent 设定，开箱即用的**飞书日历智能协作团队，覆盖会议全生命周期管理**。

给你的 Agent 发送这套文件，它会自动读取并融入自己的能力体系，无需手动配置。

## 这套东西包含什么

### 🧠 Agent 人格设定（`workspace/`）

| 文件 | 说明 |
|------|------|
| `SOUL.md` | 核心人格 — 角色定位、工作原则、上下文管理策略 |
| `IDENTITY.md` | 身份卡片 — 名称、人设、风格 |
| `AGENTS.md` | 运行规范 — Session 启动流程、记忆管理、安全边界 |
| `USER.md` | 用户画像 — 需要新用户自行填写 |
| `TOOLS.md` | 工具备忘 |
| `HEARTBEAT.md` | 心跳检查 — 任务进度监控规则 |

### 🛠️ 团队成员 Skills（`skills/`）

| cross-platform-messenger-claw | 跨渠道消息推送与联络协调。核心职责：打通各类通讯工具与邮件的接口，确保预警和报告能精准推送到目标人员。业务价值：信... |
| interview-scheduler-claw | 面试邀约自动化协调。核心职责：自动联系候选人并协调面试官时间。业务价值：日程同步——自动查询全员日历空档，实现精准... |
| meeting-assistant-claw | 全流程会议助理虾。核心职责：录音转写、提炼待办并分发任务。业务价值：结果闭环——直接将待办指派到人的协作软件中，防... |
| schedule-sync-claw | 飞书日历智能协作 Skill。核心能力：(1) 智能约会——查询多人空闲时间、自动创建会议并发送邀请，(2) 日程... |
| sensevoice-transcribe | Transcribe audio files (WAV/MP3/M4A/FLAC) to timestamped ... |

## 快速上手

### 1. 前提条件

- 已安装并运行 OpenClaw
- 已有一个可用的 Agent（任何 agent 都行，它会自己融入新设定）

### 2. 环境依赖

pip install funasr torch modelscope

### 3. 把文件给 Agent

把整个 `schedule-sync-starter/` 目录放到你的 Agent 可以访问的位置，然后对 Agent 说：

> 请读取 `schedule-sync-starter/AGENT-SETUP.md`，按照里面的指引完成接入。

Agent 会自动：
1. 读取所有设定文件
2. 将团队设定融入自己的人格体系
3. 安装 Skills
4. 引导你设置用户信息

### 4. 开始使用

接入完成后，你可以：

- 📅 智能约会议 — 查空闲、创建日程、发邀请
- 🎙️ 会议录音转纪要 — 转写录音、提炼待办、分发任务
- 🤝 批量约面 — 面试官空闲查询、一键创建面试日程
- 📨 跨平台消息推送 — 飞书/WhatsApp/Telegram 等多渠道通知

## 目录结构

```
schedule-sync-starter/
├── README.md                          ← 你正在看的这份
├── AGENT-SETUP.md                     ← Agent 接入指引（给 Agent 看的）
├── workspace/                         ← 人格设定文件
│   ├── SOUL.md
│   ├── IDENTITY.md
│   ├── AGENTS.md
│   ├── USER.md                        ← ⚠️ 使用前需填写用户信息
│   ├── TOOLS.md
│   └── HEARTBEAT.md
└── skills/                            ← 团队成员 Skills
├── cross-platform-messenger-claw/
├── interview-scheduler-claw/
├── meeting-assistant-claw/
├── schedule-sync-claw/
└── sensevoice-transcribe/
```

## 📎 Skill 依赖关系

```
schedule-sync-claw          ← 📅 日程协办（核心 Skill）
interview-scheduler-claw    ← 🤝 约面招聘（依赖 schedule-sync-claw 查空闲/创建日程）
cross-platform-messenger-claw ← 📨 跨平台消息（独立，常与其他 Skill 协作发通知）
meeting-assistant-claw      ← 🎙️ 会议助理
  └── sensevoice-transcribe   ← 🗣️ 语音转写（meeting-assistant-claw 的转写依赖）
```

**说明：**
- `interview-scheduler-claw` 内部会调用飞书日历能力，与 `schedule-sync-claw` 功能互补
- `meeting-assistant-claw` 执行录音转写时依赖 `sensevoice-transcribe` 提供的 SenseVoice-Small 转写环境
- `cross-platform-messenger-claw` 是独立的通信层，常作为其他 Skill 的下游用于消息分发
- 安装时建议按以上顺序，确保依赖的 Skill 先就位

## 自定义建议

拿到手后你可以按需修改：

- **`workspace/USER.md`** — 填写你的名字和偏好，Agent 接入时会读取
- **`workspace/IDENTITY.md`** — 不喜欢"虾队长"可以改成你想要的名字
- **`workspace/SOUL.md`** — 调整工作风格（比如要不要每步都汇报进度）
- **各 Skill 的 `SKILL.md`** — 微调每个团队成员的专业行为

## 许可

自由使用，随意修改。🦞
