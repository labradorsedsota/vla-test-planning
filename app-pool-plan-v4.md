# 测试应用池构建方案 v4.0（mano-afk 端到端版）

> 版本：v4.0 | 日期：2026-04-21
> 定位：**mano-afk 端到端流程** — 一句话 prompt 开发 + mano-cua 自动验收
> 需求方：廖雨亭 | 方案设计：Pichai（PM）| 适配性分析：智子
> 具体交付内容按项目要求再定。本文件聚焦：**应用类型、应用编号、覆盖组件**。

---

## 与 v3.1 的主要变更

1. **去除不适配应用** — 移除 mano-afk ❌ 或 mano-cua 🔴 的 3 个应用（员工管理、文件管理器、主页生成器）
2. **组件回收** — 被移除应用中的 5 个 ⚠️ 可验收组件自然融入剩余应用（Calendar、Carousel、TreeSelect、Transfer、Tree）
3. **格式精简** — 聚焦应用类型、编号、覆盖组件，去除场景描述
4. **智子类型标签** — 每个应用标注智子 mano-afk 适配性分类

---

## 标注说明

**mano-cua 验收适配性：** 🟢 完全适配 | 🟡 基本适配，部分交互需策略
**mano-afk 开发适配性：** ✅ 完美（LLM 常识覆盖）| ⚠️ 可做（需 PRD 约束）

**智子应用类型分类：**

| 类型 | 特征 | mano-afk 适配 |
|------|------|---------------|
| 纯工具型 | 输入→处理→输出，无状态，单页面 | ✅ 完美 |
| 标准 CRUD 管理 | 单实体增删改查 + 筛选 + 列表 | ✅ 完美 |
| 配置/设置面板 | 开关、选项、偏好管理 | ✅ 完美 |
| 带状态机的 CRUD | 多实体 + 状态流转 | ⚠️ 可做 |
| 数据统计/看板 | KPI 卡片 + 筛选 + 图表 + 汇总 | ⚠️ 可做 |
| 表单密集型 | 多种输入控件组合 | ⚠️ 可做 |
| 多步骤流程型 | 分步表单/发布/审批链 | ⚠️ 勉强 |
| 多实体关联型 | 实体间引用，删除保护/级联更新 | ⚠️ 勉强 |

---

## 应用池

### ── P0（高适配 + 高覆盖增量）──

#### App 01: 📝 在线记事本 🟢 ✅

**智子类型：纯工具型**
**覆盖组件（11）：** Input, Button, Radio, Switch, Select, Dialog, Message, Alert, Tooltip, Link, Card

---

#### App 02: 🔧 JSON 格式化工具 🟢 ✅

**智子类型：纯工具型**
**覆盖组件（9）：** Input, Button, Radio, Alert, Message, Result, Card, Statistic, Segmented

---

#### App 03: ✅ 待办事项清单 🟢 ✅

**智子类型：带状态机的 CRUD**
**覆盖组件（14）：** Input, Form, Checkbox, DatePicker, Select, Tag, Table, Pagination, Empty, Tabs, Badge, Message Box, Button, Calendar ★

> ★ Calendar 为 v4.0 新增（任务日历视图），回收自原 App 12 员工管理

---

#### App 04: 📇 通讯录管理 🟢 ✅

**智子类型：标准 CRUD 管理**
**覆盖组件（15）：** Input, Form, Input Number, Autocomplete, Avatar, Table, Pagination, Descriptions, Tag, Drawer, Popconfirm, Empty, Breadcrumb, Menu, Button

---

#### App 05: 🔧 系统设置中心 🟢 ✅

**智子类型：配置/设置面板**
**覆盖组件（15）：** Form, Switch, Radio, Select, Input, Tabs, Descriptions, Dialog, Message, Alert, Popconfirm, Page Header, Menu, Divider, Watermark

---

### ── P1（中等适配，需 PRD 约束）──

#### App 06: 📖 个人博客后台 🟡 ⚠️

**智子类型：多步骤流程型**
**⚠️ 风险点：** 多步骤发布流程（编辑→预览→发布），步骤间状态依赖需 PRD 定义
**覆盖组件（16）：** Form, Input, InputTag, Select, Switch, DateTimePicker, Table, Pagination, Tag, Tabs, Dropdown, Dialog, Page Header, Skeleton, Steps, Carousel ★

> ★ Carousel 为 v4.0 新增（文章配图轮播），回收自原 App 16 主页生成器

---

#### App 07: 💰 家庭记账本 🟡 ⚠️

**智子类型：数据统计/看板**
**⚠️ 风险点：** 涉及金额计算精度，PRD 需锁死计算规则
**覆盖组件（13）：** Form, Input, Input Number, DatePicker, Select, Radio, Table, Progress, Collapse, Timeline, Card, Message, Notification

---

#### App 08: 🛒 商品管理系统 🟡 ⚠️

**智子类型：多实体关联型**
**⚠️ 风险点：** 实体间引用关系、删除保护/级联更新是已知弱点
**覆盖组件（18）：** Form, Input, Input Number, Cascader, TreeSelect ★, Select, Switch, Rate, Table, Pagination, Image, Tag, Descriptions, Badge, Alert, Loading, Dialog, Popover

> ★ TreeSelect 为 v4.0 新增（商品分类树选择），回收自原 App 12 员工管理

---

#### App 09: 📋 问卷调查系统 🟡 ⚠️

**智子类型：表单密集型**
**覆盖组件（19）：** Form, Input, Radio, Checkbox, Rate, Input Number, Select, Switch, TimePicker, TimeSelect, Collapse, Statistic, Progress, Table, Empty, Backtop, Result, Tour, Transfer ★

> ★ Transfer 为 v4.0 新增（题库管理穿梭框：可选题目 ↔ 已选题目），回收自原 App 12 员工管理

---

#### App 10: 📰 内容管理平台 🟡 ⚠️

**智子类型：多步骤流程型**
**⚠️ 风险点：** 审核流程状态机（草稿→待审→已发布→归档）需 PRD 精确定义
**覆盖组件（16）：** Form, Input, Mention, Cascader, Table, Virtualized Table, Infinite Scroll, Image, Dropdown, Steps, Tag, Affix, Anchor, Popconfirm, Notification, Tree ★

> ★ Tree 为 v4.0 新增（频道/栏目层级树展示），回收自原 App 12 员工管理

---

### ── P2（场景补充 + 覆盖收尾）──

#### App 11: 📦 库存管理系统 🟢 ⚠️

**智子类型：带状态机的 CRUD**
**覆盖组件（15）：** Form, Input, Input Number, DatePicker, Select, Table, Pagination, Tag, Badge, Statistic, Timeline, Card, Alert, Dialog, Steps

---

#### App 12: 📊 销售数据看板 🟡 ⚠️

**智子类型：数据统计/看板**
**覆盖组件（15）：** Statistic, Card, DatePicker, Select, Virtualized Select, Table, Virtualized Table, Virtualized Tree, Progress, Segmented, Pagination, Skeleton, Loading, Affix, Backtop

---

#### App 13: 🎓 在线考试系统 🟡 ⚠️

**智子类型：表单密集型**
**⚠️ 风险点：** 日期时间密集，时区处理是 mano-afk 已知弱点
**覆盖组件（18）：** Form, Radio, Checkbox, Input, Input Number, Switch, DateTimePicker, Table, Pagination, Progress, Statistic, Steps, Result, Collapse, Tag, Alert, Message, Breadcrumb

---

## 覆盖率审计

### 累计覆盖统计

| 优先级 | 应用 | 智子类型 | cua | afk | 新增 | 累计 | 覆盖率 |
|--------|------|---------|-----|-----|------|------|--------|
| P0 | App 01 在线记事本 | 纯工具型 | 🟢 | ✅ | 11 | 11 | 17% |
| P0 | App 02 JSON 格式化 | 纯工具型 | 🟢 | ✅ | 3 | 14 | 22% |
| P0 | App 03 待办事项 | 带状态机的 CRUD | 🟢 | ✅ | 11 | 25 | 38% |
| P0 | App 04 通讯录 | 标准 CRUD 管理 | 🟢 | ✅ | 8 | 33 | 51% |
| P0 | App 05 系统设置 | 配置/设置面板 | 🟢 | ✅ | 3 | 36 | 55% |
| P1 | App 06 博客后台 | 多步骤流程型 | 🟡 | ⚠️ | 6 | 42 | 65% |
| P1 | App 07 家庭记账 | 数据统计/看板 | 🟡 | ⚠️ | 4 | 46 | 71% |
| P1 | App 08 商品管理 | 多实体关联型 | 🟡 | ⚠️ | 6 | 52 | 80% |
| P1 | App 09 问卷调查 | 表单密集型 | 🟡 | ⚠️ | 5 | 57 | 88% |
| P1 | App 10 内容管理 | 多步骤流程型 | 🟡 | ⚠️ | 6 | 63 | 97% |
| P2 | App 11 库存管理 | 带状态机的 CRUD | 🟢 | ⚠️ | 0 | 63 | 97% |
| P2 | App 12 销售看板 | 数据统计/看板 | 🟡 | ⚠️ | 2 | 65 | 100% |
| P2 | App 13 在线考试 | 表单密集型 | 🟡 | ⚠️ | 0 | 65 | 100% |

> 覆盖率以 65 个可验收组件为分母（总 69 个交互组件 - 4 个 ❌ 排除组件）。

### 按智子类型分布

| 智子类型 | 应用数 | mano-afk 适配 |
|---------|--------|---------------|
| 纯工具型 | 2 | ✅ 完美 |
| 标准 CRUD 管理 | 1 | ✅ 完美 |
| 配置/设置面板 | 1 | ✅ 完美 |
| 带状态机的 CRUD | 2 | ✅/⚠️ |
| 数据统计/看板 | 2 | ⚠️ 可做 |
| 表单密集型 | 2 | ⚠️ 可做 |
| 多步骤流程型 | 2 | ⚠️ 勉强 |
| 多实体关联型 | 1 | ⚠️ 勉强 |

### 排除组件（4 个，均为 ❌ mano-cua 不可验收）

| 组件 | 原所在应用 | 排除原因 |
|------|-----------|---------|
| Upload | 文件管理器 | 触发系统文件对话框，mano-cua 无法控制 OS 级 UI |
| Slider | 文件管理器/主页生成器 | 拖拽操作，mano-cua 无法精确定位 |
| Color Picker | 主页生成器 | 色板区域拖拽 + 精确取色 |
| Splitter | 主页生成器 | 面板边界拖拽调节 |

### v4.0 组件回收记录

| 回收组件 | 融入应用 | 融入方式 | 原所在应用 |
|---------|---------|---------|-----------|
| Calendar | App 03 待办事项 | 任务日历视图 | 原 App 12 员工管理 |
| Carousel | App 06 博客后台 | 文章配图轮播 | 原 App 16 主页生成器 |
| TreeSelect | App 08 商品管理 | 商品分类树选择 | 原 App 12 员工管理 |
| Transfer | App 09 问卷调查 | 题库管理穿梭框 | 原 App 12 员工管理 |
| Tree | App 10 内容管理 | 频道/栏目层级树 | 原 App 12 员工管理 |

---

## v3.1 → v4.0 变更记录

| 变更 | 说明 |
|------|------|
| 移除原 App 12 员工管理系统 | mano-afk ❌（多角色权限矩阵，LLM 常识猜不准） |
| 移除原 App 15 文件管理器 | mano-afk ❌ + mano-cua 🔴（Upload/Slider） |
| 移除原 App 16 主页生成器 | mano-afk ❌ + mano-cua 🔴（Color Picker/Splitter） |
| App 03 待办事项 + Calendar | 回收组件，任务日历视图 |
| App 06 博客后台 + Carousel | 回收组件，文章配图轮播 |
| App 08 商品管理 + TreeSelect | 回收组件，商品分类树选择 |
| App 09 问卷调查 + Transfer | 回收组件，题库管理穿梭框 |
| App 10 内容管理 + Tree | 回收组件，频道/栏目层级树 |
| 全部应用标注智子类型 | 纯工具型/标准CRUD/配置面板/带状态机CRUD/数据看板/表单密集/多步骤/多实体 |
| 格式精简 | 去除场景描述，聚焦应用类型、编号、覆盖组件 |
| 重新编号 App 01-13 | 原 App 13→新 App 12，原 App 14→新 App 13 |
