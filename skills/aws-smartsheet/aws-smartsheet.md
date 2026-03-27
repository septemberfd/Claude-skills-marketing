# AWS Smartsheet 表单生成器

根据 Zilliz 客户案例网页，生成 AWS Partner AI Customer Success Public References 表单的 markdown 文档。

## 输入

客户案例网页链接：$ARGUMENTS

## 任务步骤

1. **抓取网页**：使用 WebFetch 读取上面的客户案例链接，提取以下信息：
   - 公司名称和描述
   - 面临的问题/挑战
   - 实施的解决方案（架构、技术、功能）
   - 所有量化结果和指标（百分比、数字、性能提升）— 原文提取
   - 所有引言/testimonials，包含完整归属（姓名、职位、公司）
   - 行业/垂直领域
   - 规模数据（向量数、用户数、数据量）
   - 国家/地区信息
   - 技术细节（embedding 模型、搜索架构、AWS 服务）

2. **生成 markdown 文档**：按照下方模板格式填写，结合默认字段和从网页提取的信息。

3. **确认**：将生成的内容展示给用户确认，**得到用户同意后**再写入文件。

4. **写入文件**：保存到 `~/Downloads/ai content/AWS smart sheet/` 目录下，文件名格式为 `AWS-Smartsheet-{客户名}.md`。

## 默认字段（所有客户通用）

以下字段不需要从网页提取，直接使用默认值：

| 字段 | 默认值 |
|------|--------|
| Your Company Name | Zilliz |
| AWS Partner Type | ISV |
| Your company's primary GEO focus | APJ, EMEA, GCR, GLBL, LATAM, NAMER（勾选除 Unknown 外所有） |
| Is the solution in production? | In Production |
| Is your company enrolled in the AI Competency? | Yes: Agentic |
| AWS AI Services used | Amazon Bedrock |
| AI Assessment Funded Opportunity? | Not sure |
| ACE Opportunity ID | [需要 wenjie 确认，来不及可先不填] |
| ACE Opportunity launch date | [需要 wenjie 确认，来不及可先不填] |
| Date customer reference was published | [需去 Strapi 确认发布日期] |
| Additional Comments | （不填） |
| Email Receipt | fendy.feng@zilliz.com |

## 需要从网页提取的字段

| 字段 | 提取方式 |
|------|----------|
| Reference customer name | 从网页提取客户公司名称 |
| URL to published AI customer reference | 即输入的客户案例链接 |
| What makes this customer success story unique? 30 second pitch | 从网页提取关键信息，撰写一段简洁有力的描述，包含：公司是谁、面临什么问题、用 Zilliz Cloud 做了什么、取得了什么成果、关键数据指标 |
| Quantify the business outcome or impact | 从网页提取所有量化指标，用 bullet points 列出 |
| Customer reference industry | 根据客户所属行业选择合适的分类 |

## 重要规则

- **Milvus 品牌规范**：在 "What makes this customer success story unique? 30 second pitch" 和 "Quantify the business outcome or impact" 这两个字段中，不允许单独出现 "Milvus"。必须替换为 "Zilliz Cloud (fully managed Milvus)"。即使客户案例原文中使用的是 "Milvus"，也需要替换。原因：表单提交给 AWS，需要体现 Zilliz Cloud 产品。
- **禁止使用 `<br>` 换行符**："Quantify the business outcome or impact" 字段中的 bullet points 直接用换行分隔，不要使用 `<br>` 标签。

## 输出模板

```markdown
# AWS Partner AI Customer Success Public References — {客户名}

表单链接: https://app.smartsheet.com/b/form/e86ef88a3d264da184773f1efd55406e

---

| 字段 | 内容 |
|------|------|
| **Your Company Name** | Zilliz |
| **AWS Partner Type** | ISV |
| **Your company's primary GEO focus** | APJ, EMEA, GCR, GLBL, LATAM, NAMER（勾选除 Unknown 外所有） |
| **Reference customer name** | {客户名} |
| **URL to published AI customer reference** | {客户案例链接} |
| **Is the solution in production?** | In Production |
| **Is your company enrolled in the AI Competency?** | Yes: Agentic |
| **AWS AI Services used** | Amazon Bedrock |
| **What makes this customer success story unique? 30 second pitch** | {从网页提取并撰写} |
| **Quantify the business outcome or impact** | {从网页提取量化指标} |
| **AI Assessment Funded Opportunity?** | Not sure |
| **ACE Opportunity ID** | [需要 wenjie 确认，来不及可先不填] |
| **ACE Opportunity launch date** | [需要 wenjie 确认，来不及可先不填] |
| **Customer reference industry** | {根据客户行业选择} |
| **Date customer reference was published** | [需去 Strapi 确认发布日期] |
| **Additional Comments** | |
| **Email Receipt** | fendy.feng@zilliz.com |

---

## 参考引言

> "{引言1}"
> — **{姓名}**, {职位}, {公司}

> "{引言2}"
> — **{姓名}**, {职位}, {公司}
```
