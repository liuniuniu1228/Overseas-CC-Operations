# Sales Operation Data Analysis
## 销售运营数据分析手册（GitHub 版）

---

## 1. Core Concept 核心理念
Sales operation is the job of **finding gaps**:
- Between good and bad
- Between good and better
- Between reality and goals

Make goals become reality.

---

## 2. Goal Setting 目标设定（Top-Down）
Goals are issued by **Central Operations** at the beginning of each month.

### Market Side Objectives
- Monthly market registration target
- Monthly conversion rate target
- Monthly average order value (AOV)

### Referral Side Objectives
- Referral registration target (by lifecycle)
- Referral conversion rate target (by lifecycle)
- Referral average order value
- Percentage of referrals

---

## 3. Indicator Definition 指标定义
- **Conversion Rate** = Orders ÷ Allocated Leads
- **Average Order Value** = Total Payment ÷ Order Number

---

## 4. Process Indicator Drill-down 过程指标拆解
### 4.1 Market Problem Analysis 市场问题思路
Key indicators to monitor:
- Registration
- Conversion Rate
- Orders
- AOV
- Revenue

**Market Volume 市场进量**
- Market volume rhythm (slightly ahead of BM)
- Channel proportion
- Adult proportion
- Regional proportion (e.g., non-Saudi in Middle East)
- Sales feedback for channel optimization

**Section Conversion Rate 截面转化率**
`(Current month new paid + previous month registered paid in current month) ÷ Current month new registered (allocated) users`

Influencing factors:
- Public pool data quality & activity
- Lead drop rule
- Sales calling time on historical leads
- Operating policies for historical users
- System behavior for historical users

**Funnel Conversion Rate 漏斗转化率**
Result of 3 sub-indicators:
1. Attendance → Payment rate
2. Reservation → Attendance rate
3. Registration → Reservation rate

#### 4.1.1 Attendance-Payment Rate 出席付费率
Influencing factors:
- User cycle (school season / exam season)
- Lesson experience (preview / review / big screen / punctuality / material / AC message)
- CC after-class follow-up efficiency
- CC closing skills
- Channel quality change
- On-site & off-site incentives
- Script materials

#### 4.1.2 Reservation-Attendance Rate 预约出席率
Influencing factors:
- User cycle
- Attendance policy & incentives
- CC pre-class calling efficiency
- Channel quality
- System reminders
- Script materials

#### 4.1.3 Registration-Reservation Rate 预约率
Influencing factors:
- User cycle
- Timeliness of call after registration
- Channel quality (self-booking ratio)

#### 4.1.4 AOV 客单价
Influencing factors:
- User salary cycle (Middle East / Taiwan tax / HK subsidy)
- Payment & installment habits
- Main push package strategy
- Incentive policy (order vs. amount oriented)
- Study reward / gift policy

---

### 4.2 Referral Problem Analysis 转介绍问题思路
Monitor:
- Referral registration
- Referral conversion rate
- Orders
- AOV
- Revenue

**Referral Volume 转介绍进量**
- Referral conversion cycle (slightly ahead of BM)
- Bring-new ratio by lifecycle
- Channel proportion (CC narrow / SS narrow / wide)
- Multi-account / multi-kid influence

**Referral Conversion 转介绍转化**
Use the **same funnel logic as market**:
- Section conversion rate
- Funnel conversion rate
- Attendance-payment rate
- Reservation rate

**Referral AOV 转介绍客单价**
- Same logic as market
- A→B same price effect (HK >65%)
- Price increase impact

---

## 5. Common Data Sources 常用数据源
### 5.1 Call Data 通话数据
- Lingyun Task: `1001307913`
```sql
SELECT
  c.*,
  b.dept_name,
  b.crm_name,
  b.crm_id,
  d.chnl1_name,
  d.cur_country_name,
  d.reg_time,
  d.first_1v1_nml_pay_time
FROM dw.dw_sale_fact_cc_call c
LEFT JOIN dw.dw_sal_dim_staff_base b
  ON c.cc_id = b.crm_id AND b.partition_id = date_sub(current_date(), 1)
LEFT JOIN dm.dm_stdt_tot_uvc_d d
  ON c.user_id = d.stdt_id AND d.partition_id = date_sub(current_date(), 1)
WHERE d.is_overseas = 1
  AND c.start_time >= '2024-XX-XX 00:00:00'
  AND b.dept_name IN ('HKCCTeam', ...);
```

### 5.2 Allocation Data 分配数据
- Lingyun Task: `1001215573`

### 5.3 Lesson Data 体验课数据
- Lingyun Task: `1001342988`
- Table: `label.stdt_label_all`

### 5.4 Order Data 订单数据
- CC Order Detail: `167424`
- Partner List: `79`

---

## 6. Key Dashboard 核心看板
### Market & Overall Dashboard
- Overall revenue / market / referral achievement
- Pre-class & after-class follow-up rate
- Preview / review / big screen usage
- Experience & payment call efficiency
- 24h / 48h / 72h follow-up rate
- Coverage rate by region

### Referral Dashboard
- Referral registration by lifecycle
- Referral conversion rate
- Bring-new ratio & volume
