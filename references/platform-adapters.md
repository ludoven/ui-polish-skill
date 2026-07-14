# 平台适配参考

先复用项目已有设计系统和平台组件。下面参数是没有现成系统时的默认参考，不是强制品牌。

## 通用 token 换算

```text
Compose：dp / sp
Compose Multiplatform：dp / sp；桌面端同时检查窗口密度和指针输入
Flutter：logical pixels；文本走 TextTheme
SwiftUI：pt；文本走 Dynamic Type / Font
Web：px / rem；组件 token 用 CSS variables 或框架主题
桌面框架：DIP / pt，按窗口密度和平台规范调整
```

通用中性色：

```text
背景：#FFFFFF / #F7F8FA / #F8F9FB
容器：#FFFFFF
主文本：#1C1C1E
次级文本：#6E6E73
弱文本：#8E8E93
分割线：#E6E8EB
弱边框：#E5E7EB
主色：#3B82F6 / #2563EB
成功：#22C55E
警告：#F59E0B
错误：#EF4444
```

## Android Compose

优先使用 Material 3 的 `ColorScheme`、`Typography`、`Shapes` 和已有 theme。

默认参考：

```kotlin
// Color
val AppBackground = Color(0xFFFFFFFF)
val AppSurface = Color(0xFFF7F8FA)
val AppCard = Color(0xFFFFFFFF)
val TextPrimary = Color(0xFF1C1C1E)
val TextSecondary = Color(0xFF6E6E73)
val TextTertiary = Color(0xFF8E8E93)
val Divider = Color(0xFFE6E8EB)
val BrandBlue = Color(0xFF3B82F6)

// Radius
val RadiusSmall = 8.dp
val RadiusMedium = 12.dp
val RadiusLarge = 16.dp

// Spacing
val SpaceXs = 4.dp
val SpaceSm = 8.dp
val SpaceMd = 12.dp
val SpaceLg = 16.dp
val SpaceXl = 24.dp
val SpaceXxl = 32.dp
```

倾向：

- 少用嵌套 `Card`。
- 用 `Column` / `Row` / `Box`、`background`、`border`、分割线和留白控制层级。
- 弱化 elevation。
- 不要所有元素都 `RoundedCornerShape(24.dp)`。
- 列表项通常 52-64dp。
- 图标常用 20-24dp。
- 文本不要全都 `FontWeight.Bold`。
- 辅助文字不要小于 12sp。
- 检查系统返回、IME、safe drawing、深色模式和动态字体。

## Compose Multiplatform

先判断目标端：Android、Desktop、iOS、Web 或多端共享。

倾向：

- 将颜色、字号、间距、圆角放到 common token；平台差异通过 expect/actual、CompositionLocal 或目标端 theme 处理。
- 不把 Android 手机密度直接搬到 Desktop。
- Desktop 端减少大卡片和过高列表项，优先工具栏、侧边栏、列表、表格和分割线。
- 检查鼠标 hover、右键菜单、键盘快捷键、焦点顺序、窗口缩放。
- iOS 目标检查 safe area、导航栏、Dynamic Type 和系统手势。
- Android 目标遵循 Material 3 和触控目标。

## Flutter

优先使用 `ThemeData`、`ColorScheme`、`TextTheme`、`InputDecorationTheme`、`IconThemeData`。

倾向：

- 使用集中 token 或 `ThemeExtension`，不要在 widget 树里散落硬编码。
- Material 产品用 Material 3；iOS 强平台感场景考虑 Cupertino 组件或混合策略。
- 用 `SafeArea`、`LayoutBuilder`、`MediaQuery` 处理屏幕和窗口。
- 手机页面左右边距通常 16/20/24。
- 列表项通常 48/56/64。
- 按钮高度通常 40/44/48。
- 圆角通常 8/12/16，避免全局 24+。
- 检查 text scale、overflow、dark theme、hover/focus 和 disabled 状态。

## SwiftUI / iOS

优先使用系统语义颜色、SF 字体、Dynamic Type、NavigationStack、Toolbar、List/Form 等系统模式。

倾向：

- iOS 触控目标不小于 44pt。
- 页面边距常用 16/20。
- 卡片圆角通常 12/16。
- 不滥用自定义阴影和毛玻璃；系统 Material 只在导航、侧栏、浮层等合理位置使用。
- 使用 `.foregroundStyle(.primary/.secondary)` 和语义色，避免大量硬编码。
- 检查 safe area、Dynamic Type、本地化、VoiceOver label、深色模式。

## macOS / 桌面 SwiftUI

桌面软件不要简单放大移动端卡片。

倾向：

- 优先考虑 sidebar、toolbar、inspector、table、split view、menu command。
- 内容密度比移动端更高：列表行常用 28-44pt。
- 页面边距常用 16/20/24，数据密集区可更紧凑。
- hover、focus ring、keyboard navigation、快捷键和窗口缩放必须可用。
- 减少巨大圆角、巨大图标、巨大空白和移动端式底部操作栏。
- 工具栏图标优先系统符号并配 tooltip。

## Web / React / Vue / HTML CSS

优先使用项目已有 CSS variables、Tailwind config、shadcn/theme、组件库或 design tokens。

倾向：

- App 和工具产品不要默认做营销式 hero。
- 不要模板站式大渐变背景。
- 不要每个模块都是大圆角白卡。
- 工具型产品优先信息密度、清晰操作和扫描效率。
- Landing page、品牌页、作品集可以有更强视觉，但主视觉必须真实服务品牌/产品。
- 使用语义 HTML、`focus-visible`、hover/active/disabled 状态。
- 检查响应式断点、移动端溢出、长单词、表格横向滚动、深色模式。

默认 CSS token：

```css
:root {
  --color-bg: #ffffff;
  --color-surface: #f7f8fa;
  --color-card: #ffffff;
  --color-text-primary: #1c1c1e;
  --color-text-secondary: #6e6e73;
  --color-text-tertiary: #8e8e93;
  --color-border: #e6e8eb;
  --color-brand: #3b82f6;

  --radius-sm: 8px;
  --radius-md: 12px;
  --radius-lg: 16px;

  --space-xs: 4px;
  --space-sm: 8px;
  --space-md: 12px;
  --space-lg: 16px;
  --space-xl: 24px;
  --space-xxl: 32px;
}
```

## React Native

倾向：

- 使用 `StyleSheet`、theme provider 或 token 文件集中管理样式。
- 同时检查 iOS 和 Android 平台差异，不把一个平台的控件质感硬套到另一个平台。
- 使用 `Pressable` 状态反馈，保证 hit slop 和触控目标。
- 检查 safe area、字体缩放、深色模式和长文案。

## Electron / Tauri / Qt / WPF 等桌面端

倾向：

- 优先桌面信息架构：菜单、toolbar、sidebar、status bar、table、split pane。
- 不要把移动端大卡片、大按钮、大留白直接搬到桌面。
- 行高、按钮、输入框更紧凑，但不能牺牲可点击性。
- 检查窗口最小尺寸、缩放、键盘焦点、快捷键、右键菜单、hover 和禁用态。
- 系统原生控件可用时优先使用，避免自绘出廉价感。

## TV / 大屏 / 遥控器

倾向：

- 远距离阅读优先：字号、图标、焦点区域都要更大。
- 保留安全边距，常用 48/64。
- 可聚焦项通常 64/72/80 高。
- 焦点态必须明显，遥控器方向顺序必须稳定。
- 避免小字、密集表格、仅靠 hover 的交互。

## 产品类型例外

- B 端、开发者工具、数据面板：优先密度、对齐、表格、筛选、状态清晰。
- 消费级 App：可以更柔和、更有情绪，但不要牺牲任务完成。
- 品牌官网、作品集、内容页：可以使用大图、品牌色、动效和更强版式，但避免空泛模板文案。
- 游戏 UI：允许强风格化、动效、HUD 和装饰，但必须保证状态可读、操作清楚。
- 创意工具：可以有更丰富的面板和画布，但工具栏、属性面板和快捷操作要符合专业软件习惯。
