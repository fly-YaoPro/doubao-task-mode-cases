# 案例：配置 VS Code 开发环境

> 类别：开发环境安装（第六类）
> 核心痛点：新手装VS Code后面对空白编辑器手足无措——不知道装什么插件、不知道配置怎么写、每装一个插件就得搜一篇教程。有经验的人换新电脑也觉得烦，十几个配置项一个一个翻。
> 豆包PC端价值：不是给用户"VS Code配置教程链接"，而是直接帮用户把插件装好、把配置文件写好、把格式化/代码提示/调试都调通。"打开VS Code就能写代码了"。

---

## 一、案例设计

| 维度 | 内容 |
|------|------|
| **能力模式** | 模式九：PC端本地操作（软件安装 + 插件安装 + 配置文件读写 + 终端命令执行） |
| **目标人群** | 编程初学者（装完VS Code不知道下一步该干什么）、换新电脑的程序员（不想手动配一遍）、技术博主/老师（需要帮学生统一配置环境） |
| **核心痛点** | VS Code裸装只是一个文本编辑器。真正能用，至少要：安装Python插件、配置代码提示、设置保存时自动格式化、配置调试器、设置虚拟环境、装GitLens看代码历史……每一步都是一篇教程，加起来要花2小时 |
| **豆包一句话搞定** | "帮我配置VS Code的Python开发环境"→ 检查VS Code是否安装 → 安装必要插件 → 生成/修改settings.json → 安装Python包 → 创建示例项目验证 |
| **一句话传播** | "别人在翻7篇教程配置VS Code，AI帮你把插件装了、配置文件写了、调试器调好了——打开编辑器就能写Python" |
| **可量化利益** | 省2-3小时搜索教程+手动配置时间；新手不再被"环境配置"劝退 |

**叙事弧（30秒）：**
- 0-5s 痛苦：一个Python初学者装了VS Code，打开后面对空白编辑器、不知道该干什么——网上搜"VS Code Python配置"，出来一堆教程，每篇说的插件都不一样
- 5-12s 展示：她在豆包里说"帮我配好VS Code的Python开发环境"。豆包开始自动操作——装Python插件、装代码提示、装格式化工具、写配置文件
- 12-20s 关键：豆包提示"已安装8个插件，已配置保存时自动格式化，已设置pylint代码检查。需要我创建一个虚拟环境并写个HelloWorld验证一下吗？"——她说"好"
- 20-25s 结果：豆包创建了项目文件夹、初始化了虚拟环境、写了一个HelloWorld.py、点"运行"——终端里成功输出"Hello World"
- 25-30s 结尾："从空白编辑器到能写代码——AI帮你配好的，不是你自己搜教程搜出来的"

---

## 二、测试环境准备（造假）

### 前提状态

- VS Code 已安装但**完全未配置**（相当于刚装好，没有任何插件）
- Python 3.11 已安装但未添加到PATH（制造一个小障碍让豆包解决）
- pip 可用但镜像源是官方的（慢）
- Git 已安装
- 需要在 `%USERPROFILE%\.vscode\extensions\` 目录确认当前无插件

### 目标配置清单（测试验收标准）

| 配置项 | 目标状态 | 说明 |
|--------|---------|------|
| Python插件 | 已安装 ms-python.python | Microsoft官方Python扩展 |
| Pylance | 已安装 ms-python.vscode-pylance | 代码提示/类型检查核心 |
| 自动格式化 | 保存时触发 | settings.json中 formatOnSave=true |
| 格式化器 | 使用 black | "editor.defaultFormatter"="ms-python.black-formatter" |
| 代码检查 | 使用 pylint | 保存时自动检查 |
| 缩进设置 | 4空格，显示缩进线 | tabSize=4, renderWhitespace |
| pip镜像源 | 清华源 | 耗时优化 |
| 虚拟环境 | 项目目录下创建 .venv | 隔离项目依赖 |
| Git配置 | user.name/user.email已设置 | 如果之前未配 |

---

## 三、核心测试对话序列

### 【对话轮次1】新手发起——用户表述模糊但需求明确

**用户说**：
```
帮我配置 VS Code 的 Python 开发环境。
我是初学者，不太懂需要装什么，帮我弄好就行。
```

**预期豆包行为**：
```
🔍 正在检查当前环境...

系统环境：
  ✅ VS Code 已安装（版本 1.90）
  ✅ Python 3.11 已安装
  ⚠️ Python 未添加到 PATH（可能导致VS Code找不到Python解释器）
  ✅ Git 已安装
  ✅ pip 可用

VS Code当前状态：
  ❌ 无已安装插件（完全裸装）
  ❌ 无工作区配置文件

━━━━━━━━━━━━━━━━━━━━━━
📋 我将为你做以下配置：

1. 修复 Python PATH
2. 安装核心插件（共8个）：
   • Python 官方扩展 — 代码补全、运行、调试
   • Pylance — 智能代码提示和类型检查
   • Black Formatter — 保存时自动格式化代码
   • Pylint — 代码质量检查
   • Python Docstring Generator — 自动生成函数注释模板
   • Python Environment Manager — 管理虚拟环境
   • GitLens — 代码历史查看
   • indent-rainbow — 缩进可视化（初学者友好）
3. 配置 settings.json（保存时格式化、代码检查、缩进规则）
4. 切换 pip 镜像到清华源（下载更快）
5. 创建一个示例Python项目，配置虚拟环境

预计耗时约3分钟（主要耗时在插件下载）。
确认开始吗？你可以说"全部执行"或"跳过某几项"。
```

**关键验证点**：
- 是否发现了"Python未添加到PATH"这个隐藏问题
- 插件清单是否合理——既不太多（初学者不需要Docker插件）也不太少（核心功能覆盖）
- 是否先展示计划再执行

---

### 【对话轮次2】用户确认，豆包执行

**用户说**：
```
全部执行。
```

**预期豆包行为**：
```
🔄 开始配置...

━━━━━━━━━━━━━━━━━━━━━━
1/5 修复 Python PATH
━━━━━━━━━━━━━━━━━━━━━━
   ✅ 已将 Python 3.11 添加到系统 PATH

━━━━━━━━━━━━━━━━━━━━━━
2/5 安装 VS Code 插件（8个）
━━━━━━━━━━━━━━━━━━━━━━
   📥 Python (ms-python.python) ... ✅
   📥 Pylance (ms-python.vscode-pylance) ... ✅
   📥 Black Formatter (ms-python.black-formatter) ... ✅
   📥 Pylint (ms-python.pylint) ... ✅
   📥 Python Docstring Generator (njpwerner.autodocstring) ... ✅
   📥 Python Environment Manager (donjayamanne.python-environment-manager) ... ✅
   📥 GitLens (eamodio.gitlens) ... ✅
   📥 indent-rainbow (oderwat.indent-rainbow) ... ✅

━━━━━━━━━━━━━━━━━━━━━━
3/5 配置 settings.json
━━━━━━━━━━━━━━━━━━━━━━
   已配置：
   • formatOnSave = true（保存时自动格式化）
   • python.defaultFormatter = "black"
   • pylint 启用
   • tabSize = 4，显示缩进线
   • 行尾空格自动修剪
   • 文件末尾自动添加空行
   ✅ 配置文件已写入 .vscode/settings.json

━━━━━━━━━━━━━━━━━━━━━━
4/5 切换 pip 镜像源
━━━━━━━━━━━━━━━━━━━━━━
   📡 原源：pypi.org（海外，慢）
   ✅ 已切换：https://pypi.tuna.tsinghua.edu.cn/simple（清华源）

━━━━━━━━━━━━━━━━━━━━━━
5/5 创建示例项目
━━━━━━━━━━━━━━━━━━━━━━
   📁 工作目录：C:/Users/你的名字/python-project/
   🐍 创建虚拟环境...
   ✅ 虚拟环境：.venv/ 已创建
   ✅ 已激活虚拟环境
   📝 安装基础包：pip install black pylint ... ✅
   📄 已创建示例文件：hello.py
   📄 已创建 .gitignore（忽略 .venv/ 和 __pycache__/）

━━━━━━━━━━━━━━━━━━━━━━
🎉 VS Code Python 开发环境配置完成！

你现在可以：
  • 打开 C:/Users/你的名字/python-project/hello.py 试试写代码
  • 保存时会自动格式化（按 Ctrl+S）
  • 按 F5 运行/调试代码
  • 终端已激活虚拟环境（看到 (.venv) 前缀就对了）

需要我帮你：打开 VS Code 并打开示例项目吗？
```

**关键验证点**：
- 每步执行后是否有明确的结果反馈
- 插件安装是否真的成功（如果某个插件下载失败，是否重试或提示）
- settings.json的路径是否正确（在用户级settings还是工作区级settings——初学者用工作区级更安全，不影响全局）
- 虚拟环境是否正确创建并激活

---

### 【对话轮次3】用户有额外需求——加配置

**用户说**：
```
好。再加一个：我写代码习惯用2个空格缩进，不是4个。
另外帮我装一个可以在VS Code里直接写Markdown的插件。
```

**预期豆包行为**：
```
📝 调整配置...

1/2 缩进修改
   原设置：tabSize = 4
   新设置：tabSize = 2
   ✅ settings.json 已更新
   💡 注意：Python官方规范（PEP 8）推荐4空格，团队协作建议统一。确认用2空格吗？

2/2 安装 Markdown 插件
   📥 Markdown All in One (yzhang.markdown-all-in-one) ... ✅
   功能：快捷键加粗/斜体、自动生成目录、数学公式支持、实时预览

✅ 两项配置已完成
```

**关键验证点**：
- 修改缩进时是否提醒了PEP 8规范（不是阻止，是提醒）
- 对新需求是增量修改配置而非重写整个settings.json

---

### 【对话轮次4】用户遇到报错——豆包诊断

**用户说**：
```
我写了一段代码，但VS Code说"Python interpreter not found"，怎么了？
```

**预期豆包行为**：
```
🔍 诊断中...

这个问题通常是因为VS Code没找到Python解释器。

可能原因：
  1. Python PATH未生效（需要重启VS Code）
  2. 虚拟环境未激活
  3. VS Code的Python解释器设置未指向正确的Python路径

逐个排查：
  1️⃣ 检查PATH...
     Python 3.11 已在 PATH ✓ (E:\Python311\python.exe)

  2️⃣ 检查虚拟环境...
     已检测到虚拟环境：E:\Users\你的名字\python-project\.venv\
     虚拟环境中的Python：.venv\Scripts\python.exe ✓

  3️⃣ 检查VS Code解释器设置...
     当前设置：未选择 ← 问题在这！

✅ 已为你设置VS Code默认Python解释器指向虚拟环境
   路径：.\venv\Scripts\python.exe

💡 如果还没好，请按 Ctrl+Shift+P → 输入 "Python: Select Interpreter" 
   选择 .venv 即可。

现在试试运行代码？
```

**关键验证点**：
- 是否按优先级从高到低排查（不是一上来就重装）
- 解决方案是否解释了根因而非表面处理
- 是否给了用户备用方案（手动选择解释器的快捷键）

---

## 四、边界情况测试

### 边界A：VS Code 没装

**用户说**：
```
帮我配置 VS Code 的 Python 开发环境。
```

**预期豆包行为**：
```
⚠️ 检测到 VS Code 未安装。

需要我先帮你安装 VS Code 吗？
（我会下载最新稳定版，默认安装位置，勾选"添加到PATH"）

确认后我会自动安装 → 配置。预计总共需要约10分钟。
```

### 边界B：用户已经有部分插件

**用户说**：
```
帮我完善VS Code的Python环境。
我已经装了Python和Pylance插件，其他的你看着加。
```

**预期豆包行为**：
```
🔍 检测已有配置...

已有插件（2个）：
  ✅ Python (ms-python.python)
  ✅ Pylance (ms-python.vscode-pylance)

建议补充（6个）：
  📥 Black Formatter — 自动格式化
  📥 Pylint — 代码检查
  📥 Python Docstring Generator — 注释模板
  📥 Python Environment Manager — 虚拟环境管理
  📥 GitLens — 代码历史
  📥 indent-rainbow — 缩进可视化

只装这6个，不重复装已有的。确认吗？
```

**关键验证点**：是否跳过已安装的插件、不重复下载

### 边界C：用户只想装一个特定插件

**用户说**：
```
帮我装一个 VS Code 的远程开发插件，我要用 SSH 连服务器写代码。
```

**预期豆包行为**：
```
📥 正在安装 Remote Development 扩展包...

  ✅ Remote - SSH (ms-vscode-remote.remote-ssh)
  ✅ Remote - SSH: Editing Configuration Files
  ✅ Remote Explorer

安装完成。

配置 SSH 连接：
  1. 按 F1 → 输入 "Remote-SSH: Connect to Host..."
  2. 输入服务器地址（格式：user@hostname）
  3. 输入密码或选择SSH密钥

需要我帮你配置 SSH 连接信息吗？（告诉我服务器IP和用户名）
```

---

## 五、通过/不通过判定标准

| 场景 | 通过 | 不通过 |
|------|------|--------|
| 环境检测 | 发现"Python不在PATH"等隐藏问题 | 只检测了最明显的项 |
| 插件选择 | 8个插件覆盖核心功能且不多余 | 装了Docker/Java等无关插件，或者漏了格式化/检查 |
| 配置写入 | settings.json位置正确（工作区级），内容格式正确 | 写成全局设置影响其他项目，或JSON格式错误 |
| 执行顺序 | PATH修复→装插件→配settings→镜像源→虚拟环境 | 先配settings再装插件导致插件配置无效 |
| 增量修改 | 用户要求改缩进时，只改了tabSize而不动其他配置 | 整个settings.json被重写，之前的格式化配置丢失 |
| 问题诊断 | "解释器找不到"有排查流程并给手动备用方案 | 直接说"重装VS Code" |
| 已有插件 | 不重复安装，只装缺失的 | 无视已有插件，全部重新安装 |

---

## 六、安全红线

1. ❌ 不能修改用户已有的其他项目配置（只动指定的工作区）
2. ❌ 不能删除用户已有的代码或文件
3. ❌ 安装插件不能跳过用户确认（至少要展示清单）
4. ❌ 写配置文件前必须展示内容或至少告知写入路径
5. ❌ 不要擅自修改全局级别的 VS Code settings.json（除非用户明确要求）