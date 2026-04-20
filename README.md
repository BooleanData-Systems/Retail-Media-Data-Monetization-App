# Retail Media & Data Monetization Accelerator

AI-powered retail media intelligence, ad revenue attribution, customer lifetime value, and data monetization analytics built natively on Snowflake.

## Overview

One platform to measure every dollar of ad revenue, incremental growth, customer value, and data monetization. Full-funnel visibility from campaign spend to customer lifetime value.

### Key Features

- **Executive Dashboard** -- Total platform revenue, blended ROAS, gross profit, CLV, CTR/CVR trends
- **Revenue Drivers** -- Revenue mix by stream (ads, recommendations, data licensing), campaign type breakdown
- **Campaign Performance** -- Per-campaign ROAS, CPA, conversion funnel, spend vs revenue trends
- **Customer Intelligence** -- RFM segmentation (Champions, Loyal, At Risk), CLV by segment, purchase propensity
- **Data Monetization** -- Revenue by usage type, dataset, consumer account; margin per query

## Setup

### Required Table References

#### 1. Ad Performance (Required)

| Column | Type | Description |
|--------|------|-------------|
| CAMPAIGN_ID | VARCHAR | Campaign identifier |
| PERFORMANCE_DATE | DATE | Date of ad delivery |
| IMPRESSIONS | NUMBER | Ad impressions |
| CLICKS | NUMBER | Ad clicks |
| CONVERSIONS | NUMBER | Purchase conversions |
| SPEND | NUMBER | Ad spend amount |
| CONVERSION_REVENUE | NUMBER | Revenue from conversions |

#### 2. Campaigns (Required)

| Column | Type | Description |
|--------|------|-------------|
| CAMPAIGN_ID | VARCHAR | Campaign identifier |
| CAMPAIGN_NAME | VARCHAR | Campaign name |
| ADVERTISER_NAME | VARCHAR | Advertiser/brand name |
| CAMPAIGN_TYPE | VARCHAR | Type (search, display, video, sponsored) |
| PLACEMENT_TYPE | VARCHAR | Placement location |
| PRICING_MODEL | VARCHAR | CPM or CPC |
| CPM | NUMBER | Cost per thousand impressions |
| CPC | NUMBER | Cost per click |
| GROSS_MARGIN | NUMBER | Margin rate (0-1) |
| AD_DELIVERY_COST_RATE | NUMBER | Ad serving cost rate |
| TARGET_CATEGORY | VARCHAR | Target product category |
| REC_MARGIN_RATE | NUMBER | Recommendation margin rate |

#### 3. Customer Transactions (Required)

| Column | Type | Description |
|--------|------|-------------|
| TRANSACTION_ID | VARCHAR | Transaction identifier |
| CUSTOMER_ID | VARCHAR | Customer identifier |
| TRANSACTION_DATE | TIMESTAMP | Purchase date |
| TOTAL_AMOUNT | NUMBER | Transaction amount |
| PRODUCT_CATEGORY | VARCHAR | Product category |

#### 4. Recommendation Events (Required)

| Column | Type | Description |
|--------|------|-------------|
| EVENT_TIMESTAMP | TIMESTAMP | Event time |
| PRODUCT_CATEGORY | VARCHAR | Recommended category |
| REVENUE | NUMBER | Revenue generated |

#### 5. Monetization Usage (Required)

| Column | Type | Description |
|--------|------|-------------|
| USAGE_DATE | DATE | Usage date |
| USAGE_TYPE | VARCHAR | License type |
| DATASET_NAME | VARCHAR | Data product name |
| CONSUMER_ACCOUNT | VARCHAR | Consumer account |
| FEE_AMOUNT | NUMBER | Fee charged |
| QUERY_COUNT | NUMBER | Queries executed |
| COST_PER_QUERY | NUMBER | Cost per query |

### Binding References (SQL Alternative)

The app will prompt you to bind tables on first launch. If you prefer SQL:

```sql
CALL <APP_NAME>.CONFIG.REGISTER_SINGLE_REFERENCE(
  'AD_PERFORMANCE_TABLE', 'ADD',
  SYSTEM$REFERENCE('TABLE', 'your_db.your_schema.clean_ad_performance', 'PERSISTENT', 'SELECT'));

CALL <APP_NAME>.CONFIG.REGISTER_SINGLE_REFERENCE(
  'CAMPAIGNS_TABLE', 'ADD',
  SYSTEM$REFERENCE('TABLE', 'your_db.your_schema.clean_campaigns', 'PERSISTENT', 'SELECT'));

CALL <APP_NAME>.CONFIG.REGISTER_SINGLE_REFERENCE(
  'TRANSACTIONS_TABLE', 'ADD',
  SYSTEM$REFERENCE('TABLE', 'your_db.your_schema.clean_transactions', 'PERSISTENT', 'SELECT'));

CALL <APP_NAME>.CONFIG.REGISTER_SINGLE_REFERENCE(
  'RECOMMENDATION_EVENTS_TABLE', 'ADD',
  SYSTEM$REFERENCE('TABLE', 'your_db.your_schema.recommendation_events', 'PERSISTENT', 'SELECT'));

CALL <APP_NAME>.CONFIG.REGISTER_SINGLE_REFERENCE(
  'MONETIZATION_USAGE_TABLE', 'ADD',
  SYSTEM$REFERENCE('TABLE', 'your_db.your_schema.monetization_usage', 'PERSISTENT', 'SELECT'));
```

### Enable Cortex AI (Required)

Grant the Cortex user role via the **Permissions** tab in Snowsight.

## Data Privacy

- Data never leaves your account
- All monetized data is aggregated and anonymized
- AI processing occurs entirely within Snowflake Cortex
- Only SELECT privileges requested

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0.0 | 2026-04 | Initial Marketplace release |
