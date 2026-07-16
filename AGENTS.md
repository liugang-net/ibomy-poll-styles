# Repository Guidelines（仓库指南）

## 项目结构与模块组织

本仓库是一个 Discourse 主题组件，用于定制官方 Poll 插件的投票样式。

- `about.json`：定义组件名称、作者及最低 Discourse 版本。
- `common/common.scss`：存放桌面端与移动端共用样式，大多数样式调整应放在这里。
- `mobile/mobile.scss`：仅存放移动端覆盖规则，避免与 `common/` 中的规则重复。

仓库目前不包含 JavaScript、静态资源目录或自动化测试目录。

## 构建、测试与开发命令

项目没有包管理器配置或本地构建脚本。组件安装或预览时，由 Discourse 负责编译 SCSS。

- `git diff --check`：检查改动中的空白字符错误。
- `git status --short`：确认本次变更涉及的文件。
- `rg "poll-container|poll-voters" common mobile`：添加规则前查找现有选择器，避免重复或冲突。

进行可视化开发时，应将此目录作为主题组件安装到本地 Discourse 实例，启用 Poll 插件，并分别检查桌面端和移动端效果。

## 编码风格与命名约定

JSON 和 SCSS 统一使用两个空格缩进。保留 `@charset "utf-8";` 作为 SCSS 文件的第一条语句。仅在能清楚表达父子关系时使用 SCSS 嵌套；除非覆盖 Discourse 默认样式确有需要，否则避免过深、特异性过高的选择器。

自定义 CSS 类使用短横线命名法，CSS 自定义属性应语义明确，例如 `--poll-bar-color--chosen`。适用时优先复用 Discourse 的语义颜色变量。若选择器依赖 Poll 插件的 DOM 结构，请添加简短注释说明。

## 测试指南

仓库目前没有自动化测试框架或覆盖率要求。每次样式修改都应手动检查：单选与多选投票、选中与未选中状态、结果进度条、长选项文本以及窄屏移动端布局。确认所有规则均限定在 `.poll-outer` 下，不影响普通按钮或列表。可见样式变更应提供修改前后的截图。

## 提交与合并请求规范

近期提交使用了 `style`、`fix`、`color` 等简短小写主题。提交应保持单一职责，并尽量使用更明确的祈使句，例如 `fix poll result bar overflow`。

合并请求应说明视觉调整目的、测试过的 Discourse 与 Poll 插件版本，以及桌面端和移动端检查结果；可见变更必须附截图。有对应问题时请关联 Issue。无关的格式整理或选择器重构应拆分为独立变更。
