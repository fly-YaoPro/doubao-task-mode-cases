# doubao-task-mode-cases

为豆包任务模式设计达人选题案例的 Codex Skill。覆盖 App 端和 PC 端，以 Skill 生态系统为推广核心。

## 目录结构

```
├── SKILL.md                  # 核心手册：筛选框架、方法论、沟通口径、铁律
├── cases/
│   ├── _index.md             # 案例总索引（29个案例的速览表）
│   ├── 能力模式一~八.md       # 按能力模式组织的完整案例库
│   └── ...
└── references/
    ├── Skill选型与测试入库流程.md
    ├── 提示词双模式与普通用户共创流程.md
    └── 外网搜索与本地化方法.md
```

## 功能概要

- **五道硬筛 + PC 场景三维**：选题筛选框架，确保每个案例能过筛且符合传播需求
- **九大能力模式**：从云端操作公共系统到 Skill 调用 + 多模态内容自动生产
- **29 个已实测/已设计案例**：含过筛表格、造假背景、测试提示词、预期行为；未实测案例单独标注
- **提示词双模式**：默认普通用户五轮共创，专家级直接执行提示词作为严格测试与成熟方案的备用模式
- **沟通口径**：达人推广场景下的推荐讲法和不建议讲法

## 安装

将本仓库放入 `~/.codex/skills/` 或 `~/.agents/skills/` 目录下，Codex 会自动识别。

```bash
git clone https://github.com/YOUR_USERNAME/doubao-task-mode-cases.git ~/.codex/skills/doubao-task-mode-cases
```

## 使用

在 Codex 中通过 `$doubao-task-mode-cases` 调用。
