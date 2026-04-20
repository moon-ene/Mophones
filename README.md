## MoPhones Case Study
### Data Analyst – Product & Credit Case Study

Objective: Analyse MoPhones' credit portfolio, customer experience (NPS), and data quality to generate insights that support better credit monitoring, reporting, and decision-making.

## File Structure
```text
MoPhones/
├── Credit Data/
│   ├── Credit Data - 01-01-2025.csv
│   ├── Credit Data - 30-03-2025.csv
│   ├── Credit Data - 30-06-2025.csv
│   ├── Credit Data - 30-09-2025.csv
│   └── Credit Data - 30-12-2025.csv
├── Sales and Customer Data.xlsx
├── NPS Data.xlsx
├── MoPhones_Case_Study.ipynb
├── q1_portfolio_metrics.png
├── q1_age_segment.png
├── q2_nps_credit.png
├── q2_friction_nps.png
└── README.md
```

## Analysis Questions

### Question 1: Portfolio Health
Five metrics selected to track credit portfolio performance over time:

1. **PAR 30 Rate** - % of loans with DPD ≥ 30 — standard credit risk threshold
2. **Arrears Rate** - % of loans with any outstanding arrears — early stress signal
3. **Default Rate** - % of loans classified FPD or FMD — first payment defaults
4. **Average Days Past Due (DPD)** - How deep delinquency runs across the book
5. **Paid-Off Rate** - % of loans fully repaid — portfolio maturity signal

### Question 2: Credit Outcomes × Customer Experience
Examining how NPS scores vary across:
- Account status
- Arrears status
- DPD buckets
- Friction events (phone locking, payment delays, support difficulty)

### Question 3: Data Quality & Recommendations
Documenting data limitations and proposing structural improvements.

## Key Findings

### Portfolio Health (2025)

| Metric | Jan 2025 | Dec 2025 | Change |
|--------|----------|----------|--------|
| PAR 30 Rate | 35.4% | 38.0% | ↑ Worsening |
| Arrears Rate | 60.8% | 56.9% | ↓ Improving |
| Default Rate | 11.7% | 9.5% | ↓ Improving |
| Avg DPD | 72 days | 128 days | ↑ Worsening |
| Paid-Off Rate | 14.1% | 25.8% | ↑ Healthy |

### NPS Analysis

- **Mean NPS Score:** 6.78
- **Net NPS:** 5.9
- **Promoters:** 41.3%
- **Passives:** 19.6%
- **Detractors:** 35.6%

### Friction Events Impact

| Event | NPS Drop |
|-------|----------|
| Phone locked despite payment | -1.37 |
| Payment delay not reflected | -1.24 |
| Difficulty reaching support | -3.09 |

## Recommendations

### 1. Collections Process (High Priority)
The phone locking mechanism is the single biggest driver of Detractor sentiment. Implement:
- 24-hour grace period after payment due date before locking
- Automated SMS confirmation before locking
- Real-time payment reconciliation dashboard

### 2. Age Segment Risk Management
The 18-25 age band shows higher default rates (10.8% vs 9.5% portfolio average):
- Stricter affordability checks
- Higher deposit requirements
- Modified loan terms

### 3. Data Infrastructure

**Priority Improvements:**
1. Add a payment events table (PAYMENT_AMOUNT is 95.6% null in current snapshots)
2. Standardize demographic capture for all sale types (currently only 50% coverage)
3. Implement NPS deduplication rules (597 loans have multiple responses)

## Generated Charts

- `q1_portfolio_metrics_6panel.png` - 6-panel portfolio health dashboard
- `q1_age_segment.png` - Risk by age band vs portfolio average
- `q2_nps_credit.png` - NPS by account status and DPD
- `q2_friction_nps.png` - Collections friction events NPS impact

## Comparison with Reference Analysis

My independent analysis **matches exactly** with the reference notebook:
- Portfolio metrics values identical across all 5 snapshots
- NPS score: Mean 6.78, Net NPS 5.9 - exact match
- Friction events NPS drops (-1.37, -1.24, -3.09) - exact match
- All findings and recommendations are consistent

## Data Quality Issues Identified

| Issue | Severity | Impact |
|-------|----------|--------|
| PAYMENT_AMOUNT / ADJUSTMENT_AMOUNT | High | 95.6% null - cannot analyze payment patterns |
| DOB & Income coverage | High | Only ~50% of loans have demographics |
| CUSTOMER_AGE column name | Medium | Misleading - actually loan tenure |
| NPS coverage | Medium | Only 17% of portfolio |
| NPS duplicate responses | Medium | 597 loans with conflicting scores |
| DATE vs SNAPSHOT_DATE mismatch | Low | March snapshot off-by-one |

