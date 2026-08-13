# Template管理概念页 — 需求Spec（v0.1）

> 说明：本文档中所有业务相关名称均以占位符表示，实际填充时替换为真实内容。

## 页面定位

Hybrid结构：**左侧模板目录（Sidebar List）+ 右侧模板详情页（Detail View）**

- 本期先做透 [Template Name]（BSP management模板）一个详情页
- 目录位预留、可扩展，为未来多模板做准备
- 整体设计原则：**简洁、图优先**，避免大段文字，多用状态标签/图标/卡片代替说明性文字

---

## 一、左侧目录（Sidebar List）

| 字段 | 说明 |
|---|---|
| 模板名称 | [Template Name] |
| 负责人 | [Owner Name] |
| Last Update Time | 最近一次更新的时间戳 |
| 排序方式 | 按Recent Update排序（最新在前） |

- 极简版可只显示名称；负责人/更新时间作为hover或次要信息展示
- 当前阶段只有1个模板条目，但结构要支持后续追加

---

## 二、右侧详情页

### 1. 模板概览（Overview）
- 名称：[Template Name]
- 适用场景 / 覆盖的Use Case：[Use Case A] / [Use Case B] / [Use Case C]
- 一句话定位：模板解决的核心问题（简短，一行）
- 负责人：[Owner Name]

### 2. 用户旅程（User Journeys）
- 核心旅程（Core Journey）+ 分支旅程（Branch Journey）
- **状态标注**：每个旅程/节点标记当前状态
  - 已落地 / 设计中（用状态标签或颜色区分，不用文字说明）
- 展示形式建议：流程图 + 状态Tag，而非文字列表

### 3. 环境UI Link
| 环境 | Link | 状态 |
|---|---|---|
| [Env: Dev] | [URL] | — |
| [Env: SIT] | [URL] | — |
| [Env: UAT] | [URL] | — |
| [Env: Prod] | [URL] | — |

- 如某环境版本落后于最新Design，建议加小标注提示（避免用户点进去发现和Figma不一致）

### 4. 最新Design
- Figma Link：[Figma URL]
- 版本号 / 更新日期
- 一句话说明最近一次更新了什么（非必须，但建议保留，避免链接无上下文）

### 5. 动向总结（Roadmap / Status Board）
三栏看板形式，图优先（卡片+状态色，不用大段文字）：

| Ongoing需求 | 在做的 | 已Confirm |
|---|---|---|
| [需求条目] + Figma Link + 负责人/提出方 | 同上 + 预计完成时间 | 同上 + 完成日期 |

- 每条建议附：Figma Link、提出方/负责人
- 可选：简单Changelog（"vX.X — 改了什么"一行式记录），呼应"模板与项目共同成长"这个叙事

### 6. 一致性规范（Consistency）
- **页面结构说明**：Header/操作区/内容区的固定布局规则（示意图优先）
- **Common Field命名规范**，例如：
  - Status类字段统一枚举：Draft / Pending / Confirmed / Deprecated
  - 时间字段命名统一：如统一用 "Created Date"
  - 旅程节点命名前缀：Core-xxx / Branch-xxx
- **组件依赖声明**：本模板使用了[Component Library]中的哪些组件（便于其他use case对照复用是否走样）

### 7. 联系方式（Feedback占位）
- 本期只做前端展示，不做完整反馈流程
- 页面留一处联系方式占位：[Contact: Name / Email / Slack Handle]

---

## 待确认/后续可迭代项
- ~~目录位未来支持多模板后，是否需要筛选/搜索~~ → 已确认，见下方决策记录（简单按名称过滤）
- Changelog是否需要更结构化的版本历史页（仍推迟，本版只做节点级"最近一次更新"单条记录）
- ~~Adoption情况（哪些use case已采用/评估中）是否在后续版本加入~~ → 已确认为真实机制，纳入本版

---

## 决策记录 v0.2（grill-me 讨论 + 原型反馈整理，供确认后再改原型）

> 本节是目前为止所有已敲定的决定的汇总，改动原型前先在这里对齐，避免零散来回改。

### 保真度与内容
- 产出物：可点击原型（假数据），不接真实后端
- 示例内容用虚构占位（如"Fish Management"），不暴露真实业务名称/内容
- 视觉参照：ballpark.ing 提取的设计系统（暗色主题、圆角药丸按钮、teal 强调色）

### 侧边栏（Sidebar）
- 顶部新增搜索框：纯前端按模板名称实时过滤，不需要后端
- 每个模板条目只显示：模板名 + 一个状态徽章，**不再显示负责人和更新时间**
  - 状态徽章取值：**Live**（模板已上线在用）/ **In Progress**（还在做）
  - 演示用两个条目：`Fish Management`（Live）、`Assumption Management`（In Progress，内容不深入，纯粹用来证明目录支持多条目）

### User Journeys（Core + Branch 结构）
- 真实结构对应：1 个 Core 节点（主表页，如 BSP 数据表）+ N 个 Branch 节点（挂在主表页上的 CRUD 类分支操作，如 Create / View-Edit / Delete）
- **布局：横向、从左到右排列**（不是之前做的纵向 Core 在上、Branch 在下），更符合通常阅读 user journey 的方向
- 每个节点：名称 + 状态徽章（Backlog / In Progress / Implemented），点击展开显示：负责人、Figma 链接、"设计已更新"记录
  - "设计已更新"是独立于状态之外的第二维度：不会让已完成的节点因为设计改了而状态倒退，只在旁边追加一条"最近一次更新说明 + 已修订次数"
- 下方的 Roadmap/动向总结版块，是同一份 Journey 节点数据按状态重新分组后的另一视图，不单独维护第二份数据

### Overview
- 显示：负责人、适用场景、Adoption（被哪些 use case 采用 / 评估中）
- Adoption 是团队真实存在的机制，正式纳入本版，不再是"后续迭代项"
- **适用场景不做成 pill 标签列表**，改成两条描述性说明文字（讲"这个模板适合什么样的场景"，不是罗列具体 use case 名字）：
  1. 其他跟 Fish Management 同构的 use case —— 明确适用
  2. table 背后挂着更复杂信息、需要表单处理的场景 —— 大方向如此，具体措辞待你确认后再定稿
  - 注：这两条的最终文案还需要再打磨，先记录方向，不动原型代码

### 环境 UI Link + 最新 Design（v0.3：简化 + 挪位置）
- 状态简化为两个取值：**Live**（跟最新设计一致） / **Legacy**（沿用旧版本，还没跟上最新设计）—— 名字用 Legacy，不用 Heritage（Legacy 是更通用的工程术语，且不像 Deprecated 那样暗示"即将废弃"）
- 环境固定为 Dev / SIT / UAT / Prod 四个（已核实）
- **最新 Design 不放版本号 / 改动说明这些细节了，只给一个 Figma 链接**（原来的 v2.3 + 一句话说明去掉）
- **位置调整**：环境 UI Link 和 最新 Design 这两块，从原来的独立区块挪到 **Overview 下面**——这两个是开发最想直接参考的信息，紧跟在 Overview 后面，不用往下翻

### 一致性规范（替代原 spec 第6节的写法）
- 目的重新定义：不是给设计规范本身（团队已经有一套独立的设计规范了），而是让其他开发者能**正确套用这个模板**去搭建新页面 —— 讲的是页面结构，不是视觉/字段规范
- 详情页固定结构（自上而下）：
  1. 顶部：面包屑（Breadcrumb）
  2. 页面标题
  3. 基础信息区块
  4. 内容区：按实际需求用 **Section Header** 分组展示（不同模板的 section 数量/内容可以不同，但都遵循"标题 + 内容"这个分组方式）
  5. 底部：**sticky action bar**（吸底操作栏）
- 之前草稿里写的"字段命名规范"（Status 枚举/"Updated Date"等）和"组件依赖声明"（Pill Button 等 chips）先移除，不属于这里要表达的内容
- **组件依赖：确认不用做**（团队已有独立设计规范，这里不重复）

#### Page Anatomy（考虑中，未定案，不进本版原型）
- 可能会加一个 Page Anatomy 小节，介绍详情页/主表页各自的设计要点
- 已提到的具体点（先记录，后续再补充完善）：
  - 详情页：像 Entity、Global Business 这类多选/长字段，展示时用 bullet point 呈现（不是逗号平铺的一行文字）
  - 主表页（Core 页）：也会有类似的展示设计要点，具体内容还没定

#### 字段命名（讨论中，未定呈现方式）
- 字段分两类：**业务类**字段 和 **Generic 类**字段（比如 Status、Updated Date 这种通用字段 vs 业务专属字段）
- 当前字段总数不多，大约十来个
- 怎么在页面上呈现这个分类（分组展示？打标签？）还没想好，先记录方向，不进本版原型

#### Build Review 要点（新增，需要确认放置位置）
- 背景：团队负责 build review，领导在 present 时会宣讲几条硬性要点：使用 Component Library、遵循 Design Patterns、Accessibility、Customer Thinking、Quality
- 我的建议：作为"一致性规范"下面的一个子模块呈现（比如叫"构建 Review 要点"），跟上面的页面结构规则放在一起 —— 因为这两者本质都是"照着这个模板开发时要满足的要求"，没必要拆成单独一个大版块，跟文档开头"简洁、避免堆砌"的原则也一致
- 待你确认：是否认可这个位置，还是想要更醒目地单独占一个区块（因为这是领导会重点讲的内容，也许值得更突出）

### User Journeys 细化（v0.3，讨论中）
- Add / View / Remove 确认是平行的三个分支（跟原型结构一致），但 **View 和 Edit 应该拆成两个独立页面/节点**，不再合并成一个 "View / Edit Fish"：
  - **Fish Management（主表页，即 Core 节点）**：模板的入口列表页
  - **Create new Fish**：点 Add → 在 "Create Fish Management" 里编辑 → Save → 跳转到刚创建记录的 View 页
  - **View Fish**：点某一行 → 进入 view 页 → 可以点进 edit → 编辑完回到（刚编辑过的）view 页
  - **Edit Fish**：从 View Fish 页进入的编辑态，不是独立入口
  - **Remove**：点小垃圾桶图标，属于轻量操作，不是一个独立"页面"
- 上面这些点击路径细节要不要体现在原型里、体现到什么颗粒度（比如卡片展开详情里加一行流程说明，还是更详细的图示），还没定，先记录

### Page Anatomy（追加一点）
- 追加一条讨论中的点：某些操作入口，团队现在有的用 **disabled（置灰但可见）**、有的用**直接隐藏**两种不同处理方式。这是一个真实的 UX 判断点，但对这张概览页来说偏细节，不放进主流程（Overview / Journeys）里讲，归到 Page Anatomy 小节里（跟"多选长字段用 bullet point"一类，都是设计要点，不是页面主干内容）

### 动向总结版块调整（替换原 spec 第5节）
- **删除**"按状态归组的三栏看板"这个视图（跟 Journey 卡片是同一份数据，展示意义不大，已确认删除）
- **改为 What's New 版块**：
  - 逐条展示：某个页面最新的设计变化是什么、这个设计变化对应哪个 use case 提出的需求、当前状态是什么
  - 支持 **Tab 筛选**：`All related pages`（= Fish Management 模板自己这几个页面的汇总，不跨其他已采用的 use case）/ `Fish Management`（主表页）/ `Create new Fish` / `Edit Fish` / `View Fish`
  - Remove 因为不是独立页面，大概率不出现在这个筛选维度里（待确认）

### 其他约定
- 页面不出现"由 AI 生成"相关的说明文字
- 详情页整体为单页滚动，配吸顶锚点导航（Overview / User Journeys / Environments / Latest Design / Consistency / Contact）
