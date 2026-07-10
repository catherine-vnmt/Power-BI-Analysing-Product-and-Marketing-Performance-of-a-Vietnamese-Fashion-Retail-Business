# 📊 [Power BI] Analysing Product and Marketing Performance of a Vietnamese Fashion Retail Business

Author: Vu Nguyen Minh Thi
Date: 2025
Tools Used: Power BI (DAX, Data Modeling)

---

## 📑 Table of Contents
1. [📌 Background & Overview](#-background--overview)
2. [📂 Dataset Description & Data Structure](#-dataset-description--data-structure)
3. [🧠 Design Thinking Process](#-design-thinking-process)
4. [📊 Key Insights & Visualizations](#-key-insights--visualizations)
5. [🔎 Final Conclusion & Recommendations](#-final-conclusion--recommendations)

---

## 📌 Background & Overview

### 🎯 Business questions:

A Vietnamese fashion retail business is running 175 marketing campaigns across multiple product lines simultaneously — with no unified view of which products and campaigns are actually delivering results.

> *"Which products are generating the most revenue and orders — and is our marketing spend behind the right ones?"*

This dashboard was built to answer that question by helping the Business Owner / General Director:

✔️ **Monitor overall business health** — Track revenue, orders, ROAS, and AOV across all products and channels in one place

✔️ **Identify top-performing products** — Understand which seasonal collections and sub-products drive the most revenue and orders, and which are underperforming

✔️ **Connect marketing spend to product results** — See which campaigns are supporting which products, and whether the spend is generating proportional returns (ROAS)

✔️ **Make faster restocking and budget decisions** — Backed by product-level and campaign-level data rather than intuition

---

### 👤 Who Is This For?

✔️ **Business Owners & General Directors of Vietnamese fashion SMEs** — to make fast, product-centric decisions on what to stock, promote, and cut

✔️ **Operations & Sales Managers** — to understand which product lines to prioritise and which are underperforming

✔️ **Marketing Analysts** — to assess which campaigns are efficiently supporting product sales and where budget is being wasted

---

## 📂 Dataset Description & Data Structure

### 📌 Data Source
- **Source:** Internal business data from a Vietnamese fashion retailer
- **Format:** .xlsx
- **Period covered:** May 2024 (5 weeks of campaign data)

### 📊 Data Structure & Relationships

#### 1️⃣ Tables Used

| Table | Role | Rows | Description |
|---|---|---|---|
| `mkt_camp_by_sku_cost` | Fact table | 3,874 | Campaign performance by product SKU and day — includes spend, impressions, CTR, CPM, CPC, inbox, new/returning customers |
| `order` | Fact table | 3,451 | All orders — includes customer info, product, price, COGS, discount, status |
| `danh_sach_san_pham` | Dimension | 2,250 | Product master list — includes product code, category, cost price, selling price, color, material |
| `mkt_camp_cost` | Dimension | 854 | Campaign-level cost by day — includes total spend, budget, CPM, CPC, impressions, clicks |

#### 2️⃣ Table Schema & Data Snapshot

**Table 1: mkt_camp_by_sku_cost (Fact — Marketing Campaign by SKU)**

<details>
<summary>View Table Schema</summary>

| Column Name | Data Type | Description |
|---|---|---|
| Tên chiến dịch | Text | Campaign name |
| Ngày | Date | Date of campaign activity |
| Số tiền đã chi tiêu | Number | Actual amount spent (VND) |
| Phân phối chiến dịch | Text | Campaign distribution type (Open / Remarketing) |
| Ngân sách chiến dịch | Number | Allocated campaign budget |
| CPM | Number | Cost per 1,000 impressions |
| CPC | Number | Cost per click |
| CTR | Number | Click-through rate |
| Lần bắt đầu cuộc trò chuyện | Number | New inbox conversations |
| Bình luận về bài viết | Number | Post comments |
| Lượt hiển thị | Number | Total impressions |
| Mã Sản phẩm | Text | Product SKU code |
| Tên Sản Phẩm | Text | Product name |
| Giá bán | Number | Selling price |
| Khách mới / Khách cũ | Number | New vs. returning customers |
| SL bán tổng | Number | Total units sold |
| SL bán được phân bổ | Number | Units sold attributed to this campaign |

</details>

---

**Table 2: order (Fact — Sales Orders)**

<details>
<summary>View Table Schema</summary>

| Column Name | Data Type | Description |
|---|---|---|
| ID | Integer | Unique order identifier |
| Thời gian | DateTime | Order timestamp |
| Nguồn | Text | Order source (Ads / Direct) |
| Tên khách hàng | Text | Customer name |
| Mã khách hàng | Text | Customer ID |
| Cấp độ khách hàng | Text | Customer tier (Membership, Silver VIP, Gold VIP, Diamond VIP, Platinum VIP) |
| Thành phố | Text | City |
| Sản phẩm | Text | Product name |
| Mã sản phẩm | Text | Product SKU |
| Danh mục sản phẩm | Text | Product category (Hàng hè, Hàng thu, Hàng đông) |
| Chiết khấu | Number | Discount applied |
| Giá | Number | Selling price |
| Số lượng | Number | Quantity ordered |
| Giá vốn | Number | Cost of goods sold (COGS) |
| Trạng thái | Text | Order status |
| Lý do hủy | Text | Cancellation reason (if applicable) |

</details>

---

**Table 3: danh_sach_san_pham (Dimension — Product List)**

<details>
<summary>View Table Schema</summary>

| Column Name | Data Type | Description |
|---|---|---|
| Mã sản phẩm | Text | Product SKU |
| Tên sản phẩm | Text | Product name |
| Loại sản phẩm | Text | Product type |
| Giá nhập | Number | Import/purchase price |
| Giá bán | Number | Selling price |
| Giá vốn | Number | Cost of goods |
| Mã danh mục nội bộ | Text | Internal category code (seasonal classification) |
| Danh mục | Text | Product category |
| Màu sắc | Text | Color |
| Chất liệu | Text | Material |
| Trạng thái | Text | Product status |

</details>

---

#### 3️⃣ Data Relationships

<img width="2336" height="1522" alt="1" src="https://github.com/user-attachments/assets/3fbaac6f-3141-43e0-822f-f0a2c362ba13" />
<img width="1394" height="477" alt="1b" src="https://github.com/user-attachments/assets/f580a775-c338-426b-b250-1571fe50fbd8" />

---

## 🧠 Design Thinking Process

### 1️⃣ Empathize

#### 5W1H Stakeholder Analysis to understand the problem
<img width="2000" height="1153" alt="2" src="https://github.com/user-attachments/assets/a5a2d516-9d0a-4a65-93db-909a6a61f69a" />

#### Empathy map to map the problem with the user
<img width="1996" height="962" alt="2a" src="https://github.com/user-attachments/assets/910ee6b9-9897-4ec1-aa84-adf92467ce05" />

---

### 2️⃣ Define Point of View

#### Define Point of View and Northstar Metrics to determine the most critical values to measure
<img width="2007" height="841" alt="2b" src="https://github.com/user-attachments/assets/8c7ed94c-9381-4c4e-a43d-b17938fe79d5" />

---

### 3️⃣ Ideate
<img width="1651" height="829" alt="2c" src="https://github.com/user-attachments/assets/b373a7fa-fe15-4f25-ae41-3f1022bf6ecd" />

---

### 4️⃣ Prototype & Review

---

## 📊 Key Insights & Visualizations

### 🔍 Page 1: Business Overview

<img width="3032" height="1681" alt="3" src="https://github.com/user-attachments/assets/f5d7df05-62c6-4f6a-947c-343750ec8cd5" />

**📌 Analysis 1: Overall business performance**
- Total Revenue: $4.66bn | Total Orders: 3K | Total Cost: $4.58bn | ROAS: 7.67 | AOV: $1.63M | New Customers: 3K
- Revenue and cost move closely together across all 5 weeks — indicating thin headroom between income and spend at every point in the period
- ROAS fluctuates week-on-week, with notable dips suggesting certain weeks see disproportionately high spend relative to revenue generated
- 82.75% of the total marketing budget ($394M of $476M) has been utilised across the period

**📌 Analysis 2: Ads Sales is generating revenue below its cost — Direct Sales is the only profitable channel**
- Ads Sales generates higher total revenue ($2.95bn) than Direct Sales ($1.70bn) — however, Ads Sales cost ($3.11bn) exceeds its revenue, meaning this channel is currently operating at a loss before accounting for COGS
- Direct Sales, by contrast, shows revenue ($1.70bn) exceeding cost ($1.47bn) — making it the only channel currently generating a positive return
- AOV from Direct Sales ($1.64M) is higher than Ads Sales ($1.51M) — indicating that customers who come directly tend to place higher-value orders
- This raises a critical question: is the marketing spend behind Ads Sales actually driving profitable orders, or simply inflating revenue volume at a net loss?

**📌 Analysis 3: Marketing budget is largely utilised but funnel efficiency remains low**
- 82.75% of the total marketing budget ($394M of $476M) has been spent across the 5-week period
- Overall funnel: 5,108,967 impressions → 41,649 clicks (0.82% CTR) → 11,438 leads (27.46%) → 2,268 orders (19.83%)
- CTR of 0.82% indicating ad creatives are not compelling enough to drive sufficient click-through relative to impressions served
- CP Ib+Cmt, CPM, and CPC all trend downward across the 5 weeks — a positive signal that the algorithm is becoming more cost-efficient over time
- New customer acquisition tracks upward in Weeks 3–4 but CAC spikes simultaneously — suggesting the cost of acquiring each new customer is increasing as the audience pool narrows


---

### 🔍 Page 2: Product Performance

<img width="3036" height="1685" alt="3B" src="https://github.com/user-attachments/assets/b2bde7c6-8940-41b3-8b9a-f75cd6362e04" />

**📌 Analysis 4: Revenue is heavily concentrated in the Summer collection**
- Summer collection (Hàng hè) contributes $663M — 95.2% of total contribution
- Autumn collection (Hàng thu) contributes $31M (4.5%) with Winter (Hàng đông) at minimal volume
- Despite lower revenue, the Autumn collection shows a higher closing rate (32.63%) vs. Summer (23.61%) — suggesting autumn products convert more effectively when shown to the right audience

**📌 Analysis 5: Váy chiết eo xoè (Hàng hè) is the most valuable product line**
- Highest revenue and profit contribution among all sub-products
- High ROAS, with both Ads Sales and Direct Sales performing strongly
- This product line is currently cross-subsidizing underperforming products

**📌 Analysis 6: Open spend exceeds Remarketing spend, but Remarketing closes more orders**
- For almost all products, Open marketing expense > Remarketing expense
- Yet Remarketing engagement funnel shows a higher conversion rate at every stage
- This misalignment between budget allocation and conversion efficiency represents a major optimization opportunity

**📌 Analysis 7: Customer acquisition patterns differ by product**
- Váy chiết eo xoè and Váy suông xoè attract the highest number of new customers — making them key acquisition products
- Almost sub-products show a high ratio of existing customers — indicating strong repeat purchase behaviour
- This behaviour may benefit more from Remarketing than Open campaigns

---

### 🔍 Page 3: Campaign by Product Drill

This page is accessed by hover on any sub-product in the Product page and selecting Drill through → Marketing campaigns. The following examples illustrate two contrasting performance patterns.

<img width="3032" height="1683" alt="3c" src="https://github.com/user-attachments/assets/30e4223a-c77c-4864-a7db-5ac3d3e5ca3b" />

**📌 Analysis 8: Váy Chiết Eo Xoè (Hàng hè) — Best-performing product with efficient campaign support**
- Total campaigns: 66 | Total spend: $125,053,488 (82.25% of $152,044,762 budget)
- Remarketing significantly outperforms Open across all key metrics:
    - Remarketing Lead Rate: 35.45% vs. Open: 16.88%
    - Remarketing Closing Rate: 18.05% vs. Open: 16.52%
    - Remarketing Mkt CR: 6.40% vs. Open: 2.79%
- ROAS for Remarketing consistently holds above Open across all 5 weeks — confirming that re-engaging existing audiences is far more efficient for this product than acquiring new ones
- The scatter plot shows most campaigns cluster at low spend and low ROAS — only a handful of campaigns at mid-range spend ($2M–$4M) achieve meaningfully higher ROAS, suggesting budget is spread too thinly across too many campaigns
- AOV from both Open and Remarketing remains stable at ~$1.6M–$1.7M throughout the period — indicating consistent order value regardless of campaign type

<img width="3034" height="1692" alt="3d" src="https://github.com/user-attachments/assets/ad90ec1a-b595-438f-bde2-1c1f3d98ee6c" />

**📌 Analysis 9: Áo Tách Set (Hàng hè) — High spend, low return — a clear candidate for budget reallocation**
- Total campaigns: 32 | Total spend: $89,675,363 (87.26% of $102,765,476 budget)
- Despite a weak entry point, mid-to-bottom funnel metrics are notably strong — and actually outperform Váy Chiết Eo Xoè across most conversion stages:
    - Lead Rate: 40.41% vs. 20.37% (Váy Chiết Eo Xoè)
    - Closing Rate: 23.93% vs. 17.02%
    - Mkt CR: 9.67% vs. 3.47%
    - Overall CR: 0.06% vs. 0.03%
- However, CTR sits at only 0.65% — significantly below both Váy Chiết Eo Xoè (0.98%) and the portfolio average (0.89%) — indicating the ad creative is failing to capture attention at the impression stage before users even reach the funnel
- Remarketing shows a notably higher Lead Rate (43.91%) than Open (38.71%), confirming that audiences already familiar with the product engage and convert more readily
- The ROAS scatter plot shows most campaigns clustered at low-to-mid spend with moderate ROAS — not as strong as top performers, but not a clear loss-making pattern either

---

## 🔎 Final Conclusion & Recommendations

Based on the analysis, we recommend the business owner consider the following strategic actions:

**📍 Key Takeaways:**

✔️ **Reallocate budget from Ads Sales towards improving Direct Sales conversion:** Ads Sales is currently operating at a loss ($2.95bn revenue vs. $3.11bn cost). Before increasing ad spend, the business should investigate what is driving strong Direct Sales performance ($1.70bn revenue vs. $1.47bn cost) — and replicate those conditions across the broader customer base through loyalty programmes, CRM, and repeat purchase incentives.

✔️ **Shift approximately 20–30% of Open campaign budget to Remarketing:** — Remarketing consistently delivers higher Lead Rate, Closing Rate, and Mkt CR than Open across all product lines — yet receives less budget. Rebalancing towards Remarketing would directly improve overall campaign efficiency without increasing total spend. This applies particularly to Váy Chiết Eo Xoè, where the Remarketing efficiency gap vs. Open is most pronounced.

✔️ **Prioritise Váy Chiết Eo Xoè as the primary product for marketing investment:** This sub-product delivers the strongest combination of revenue volume, campaign efficiency, and stable AOV across the period. Concentrating budget behind this product — particularly through Remarketing — would maximise returns from existing spend before expanding to other product lines.

✔️ **Fix the creative for Áo Tách Set — do not cut the budgeta:** Áo Tách Set has a strong conversion funnel (Lead Rate 40.41%, Closing Rate 23.93%) but a critically weak CTR (0.65%). The product converts well once users engage — the problem is getting them to click in the first place. A/B testing new ad creatives focused on stronger hooks and visuals would address the top-of-funnel weakness without abandoning a product that demonstrably converts.

✔️ **Consolidate campaigns and concentrate spend behind proven performers:** The scatter plot across both product drill-throughs shows the majority of campaigns delivering low ROAS regardless of spend level. Running fewer, better-funded campaigns behind proven creative and audience combinations would likely outperform the current approach of spreading budget thinly across 66+ campaigns simultaneously.
