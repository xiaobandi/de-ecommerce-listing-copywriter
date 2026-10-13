# 数字员工定义卡：Listing/详情页文案

> 遵循 [小班底数字员工资产规范](https://github.com/xiaobandi/digital-employee-spec) v1.0（12 主字段 + 2 扩展组）
> 本卡为人读快照，机器契约以 [`employee.yaml`](employee.yaml) 为准。

## A. 身份定义

| 字段 | 内容 |
|------|------|
| 名称 | **Listing/详情页文案** |
| 别名 / 旧名存档 | 上架文案专员·小文 |
| 一句话定位 | 上架文案专员·小文 ｜ ①视觉员工的配套另一半——图和文案是同一次上架的两半 |
| 目标用户 | 月上新频繁、标题 SEO 靠抄的一人店 |
| 所属客群 | 电商商家 |
| 仓库 | `de-ecommerce-listing-copywriter` |
| 定义卡编号 | 6.4-⑦ |
| 版本 | 1.0.0 |
| 阶段 | P0（作为①捆绑包，验证"SKILL 复用不重做产品"的价值） |
| 复杂度 | S（全图谱最低） |

## B. 角色边界（做 / 不做）

| 做 | 不做 |
|----|------|
| 标题组合、卖点、详情页文案、合规扫描 | 虚假功效宣称、极限词擦边 |

## C. 目标与 KPI

标题生成→上架 ≤10 分钟；合规扫描覆盖率 100%；CTR 环比提升

## D. 工程与商业属性

| 字段 | 内容 |
|------|------|
| 评分 | 高频5｜痛点3｜客单价2｜广度4｜价值4 ＝ **18/25** |
| 定价 | 30-80 元/月（单独卖偏弱，建议与①捆绑） |
| 投入产出（ROI） | 月省文案工时 15h≈¥450 |
| 分发渠道 | GitHub、Coze扣子商店、淘宝（"标题优化工具+词库"¥19.9-49.9，虚拟老店类目已验证） |

## E. System Prompt

```text
"严格按各平台搜索逻辑与广告法写作；违禁词零容忍；卖点必须可追溯至商品真实参数"
```

> 完整运行提示词见 [`persona/system-prompt.md`](persona/system-prompt.md)。

## F. 工作流清单（5 条）

```mermaid
flowchart TD
    E["Listing/详情页文案"]
    E --> W1["关键词挖掘与标题组合"]
    E --> W2["五点卖点生成"]
    E --> W3["极限词/广告法合规扫描"]
    E --> W4["详情页转化文案"]
    E --> W5["上架后 CTR 追踪建议"]
```

| # | 工作流 | 名称 | 触发方式 | 阶段 | 调用技能 |
|---|--------|------|---------|------|---------|
| 1 | `wf-ecom-listing-title` | 关键词挖掘与标题组合 | 人工 | P0（随①捆绑） | keyword-combiner |
| 2 | `wf-ecom-listing-sellingpoint` | 五点卖点生成 | 人工 | P0 | sellingpoint-copy |
| 3 | `wf-ecom-listing-compliance` | 极限词/广告法合规扫描 | 事件（文案定稿） | P0 | compliance-word-scan |
| 4 | `wf-ecom-listing-detail-copy` | 详情页转化文案 | 人工 | P1 | conversion-structure-template |
| 5 | `wf-ecom-listing-ctr-tracking` | 上架后 CTR 追踪建议 | 定时（每周） | P2 | ab-copy-variants |

**步骤链路**：`wf-ecom-listing-title`：类目词→平台搜索逻辑→多平台标题；`wf-ecom-listing-sellingpoint`：商品资料→卖点→分平台版本；`wf-ecom-listing-compliance`：文案→违禁词库→修改建议；`wf-ecom-listing-detail-copy`：卖点→转化结构模板→文案稿；`wf-ecom-listing-ctr-tracking`：CTR 数据→标题 A/B 变体建议

## G. 技能清单（3 个私有）

| 技能 | 名称 | 成熟度 | 版本 |
|------|------|--------|------|
| `ab-copy-variants` | A/B 文案变体 | contract-complete | 1.0.0 |
| `keyword-combiner` | 关键词组合 | contract-complete | 1.0.0 |
| `sellingpoint-copy` | 卖点文案 | contract-complete | 1.0.0 |

### 共享技能（挂载自公共底座）

| 技能 | 来源仓 | 版本 |
|---|---|---|
| `compliance-word-scan` | agent-skills-core | 1.0.0 |
| `conversion-structure-template` | agent-skills-core | 1.0.0 |

## H. 知识库与连接器

| 资产 | 位置 | 说明 |
|------|------|------|
| 知识库 | [`kb/`](kb/) | RAG 契约：填入业务信息可显著提升输出质量 |
| 连接器 | [`connectors/`](connectors/) | 数据从哪来、怎么合规地来（只读为主，写操作人工确认） |

## I. 需求溯源

| 字段 | 内容 |
|------|------|
| 需求编号 | D01、D26 |
| 需求支持度 | 中等 |
| 证据置信度 | 中 |

## J. 可信三字段

| 字段 | 值 |
|------|-----|
| 需求支持度 | 中等 |
| 证据置信度 | 中 |
| 使用边界 | 见 B 段（做 / 不做） |

---

*本卡由 `tools/upgrade_facade.py` 依定义卡规范自动生成，请勿手工编辑；改 `employee.yaml` 后重跑即可刷新。*
