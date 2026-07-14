# UI Polish Skill

一个面向 Codex 的跨平台 UI 设计实现、审查、优化与静态高保真复刻 Skill。

它既能把截图或 UI 设计稿实现为可运行界面，也能审查和打磨已有 UI：改善信息层级、间距、字体、颜色、图标和状态一致性，同时尽量沿用项目现有架构，不擅自修改业务逻辑。

## 能做什么

- 审查截图、设计稿或 UI 代码，定位廉价感、模板感和 AI 味。
- 根据截图或 UI 设计稿，在目标技术栈中实现可运行界面。
- 输出具体的颜色、字号、间距、圆角和组件修改参数。
- 按审查结果直接修改 UI 代码并执行相关验证。
- 根据截图用最终 Web 技术栈完成静态高保真复刻。
- 覆盖 Compose、Flutter、SwiftUI、React、Vue、HTML/CSS、桌面端和 TV 等平台。

## 安装

复制下面这段内容发送给 Codex：

```text
请从这个 GitHub 仓库安装 ui-polish Skill：
https://github.com/ludoven/ui-polish-skill
```

Codex 会将 Skill 安装到本地 Skills 目录。安装完成后，从下一轮对话开始使用。

### 手动安装（备用）

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

### 2. 根据 UI 设计稿实现界面

附上 UI 设计稿或截图，并提供项目或目标页面，然后输入：

```text
使用 ui-polish 根据这张 UI 设计图，在当前项目中实现对应界面。
沿用现有技术栈和设计系统，只实现 UI，不修改业务逻辑。
```

Skill 会定位项目结构、Theme 和目标页面，将设计稿中的布局、字体、颜色、图标和组件层级实现为目标技术栈中的可运行界面，并执行最快的编译、预览或截图验证。

未在设计稿中体现的业务数据、交互和状态不会被擅自补成真实逻辑；缺少的素材或行为会明确标记为占位或待确认项。

如果目标是 Compose、Flutter、SwiftUI 或常规响应式 Web 页面，使用本节；只有明确要求按截图尺寸进行 1:1、原尺寸静态 Web 还原时，才使用复刻模式。

### 3. 优化现有 UI

```text
使用 ui-polish 按审查报告改代码，只改 UI，不改业务逻辑
```

Skill 会先定位真实页面、Theme 和 Design Tokens，再进行小范围修改并运行最快的相关检查。

### 4. 静态高保真复刻

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
使用 ui-polish 根据这张 UI 设计图，在当前项目中实现对应界面，只实现 UI，不修改业务逻辑
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

## 开源许可证

本项目基于 [MIT License](LICENSE) 开源。
