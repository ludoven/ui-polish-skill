# UI Polish Skill

一个面向 Codex 的跨平台 UI 审查、优化与静态高保真复刻 Skill。

它用于把已有界面打磨得更像成熟产品：改善信息层级、间距、字体、颜色、图标和状态一致性，同时尽量保持小范围改动，不擅自修改业务逻辑。

## 能做什么

- 审查截图、设计稿或 UI 代码，定位廉价感、模板感和 AI 味。
- 输出具体的颜色、字号、间距、圆角和组件修改参数。
- 按审查结果直接修改 UI 代码并执行相关验证。
- 根据截图用最终 Web 技术栈完成静态高保真复刻。
- 覆盖 Compose、Flutter、SwiftUI、React、Vue、HTML/CSS、桌面端和 TV 等平台。

## 安装

将仓库克隆到 Codex Skills 目录：

```bash
git clone https://github.com/ludoven/ui-polish-skill.git \
  "${CODEX_HOME:-$HOME/.codex}/skills/ui-polish"
```

更新已有安装：

```bash
git -C "${CODEX_HOME:-$HOME/.codex}/skills/ui-polish" pull
```

安装后，在 Codex 中直接使用 `ui-polish` 即可。它是工作流指令 Skill，不是独立命令行程序。

## 使用教程

### 1. 审查页面

提供截图、设计稿或项目路径，然后输入：

```text
使用 ui-polish 审查这个页面
```

Skill 会输出具体问题、调整方向、设计参数和可执行修改清单，不会直接改代码。

### 2. 优化现有 UI

```text
使用 ui-polish 按审查报告改代码，只改 UI，不改业务逻辑
```

Skill 会先定位真实页面、Theme 和 Design Tokens，再进行小范围修改并运行最快的相关检查。

### 3. 静态高保真复刻

附上目标截图，然后输入：

```text
使用 ui-polish 复刻模式，静态高保真复刻这张截图
```

第一阶段会：

1. 确认截图尺寸、CSS 视口、DPR、字体和素材。
2. 使用最终 Web 技术栈实现可运行的静态页面。
3. 生成同尺寸浏览器截图，与原图对比并修正差异。
4. 交付静态确认稿后暂停，不接入业务逻辑。

确认视觉后输入：

```text
视觉确认，进入产品化阶段
```

第二阶段会继续使用同一份代码，补充响应式、交互、真实状态和已授权的业务接入，不会重新实现一套页面。

## 常用指令

```text
使用 ui-polish 根据截图优化当前页面
消除这个页面的 AI 味
只改 UI，不改业务逻辑
检查深色模式、长文案和无障碍状态
```

## 使用边界

- 不默认修改接口、数据模型、路由、权限、存储或核心业务规则。
- 不使用生成图片代替可运行的 Web 复刻结果。
- 单张截图无法证明的响应式和交互行为会标记为假设或待确认项。
- 没有真实运行环境时，不能保证像素级结果已经通过浏览器或设备验证。
- 品牌策略、用户研究、复杂动效和正式无障碍认证不属于主要能力范围。

## 目录结构

```text
ui-polish-skill/
├── SKILL.md
└── references/
    ├── audit-checklist.md
    ├── implementation-playbook.md
    ├── platform-adapters.md
    └── replication-playbook.md
```

详细行为规则见 [SKILL.md](SKILL.md)。
