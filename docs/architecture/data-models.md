# Data Models

## RouteCandidate

**Purpose:** Represents a potential transport route opportunity that the AI evaluates for construction viability and profitability.

**Key Attributes:**
- source_industry: Integer - OpenTTD Industry ID (converted to int for safety)
- destination: Integer - Destination tile index (converted to int)  
- cargo_type: Integer - Cargo type ID (0=Coal, 1=Ore, 2=Gold for simplicity)
- construction_cost: Integer - Total estimated build cost in game currency units
- expected_annual_revenue: Integer - Projected yearly revenue (integer to avoid float precision)
- roi_percentage_x100: Integer - ROI as percentage * 100 (e.g., 15000 = 150.00%)
- distance_tiles: Integer - Manhattan distance between source and destination
- production_capacity: Integer - Source industry monthly production volume

**Relationships:**
- Simple integer references to OpenTTD entities
- No complex nested objects or floating point calculations

## FinancialSnapshot

**Purpose:** Simplified financial state tracking with minimal object overhead.

**Key Attributes:**
- company_value: Integer - Total company valuation in game currency
- bank_balance: Integer - Current cash reserves
- loan_amount: Integer - Outstanding debt to bank
- month_year: Integer - Packed date for simple tracking (YYYYMM format)

**Relationships:**
- Single snapshot object, no historical arrays stored in memory
- Historical data exported to logs for external analysis

## RouteData

**Purpose:** Minimal operational data for active routes only.

**Key Attributes:**
- route_id: Integer - Simple numeric identifier
- monthly_profit: Integer - Last month's profit/loss
- active: Boolean - Whether route is still operational
- vehicle_count: Integer - Number of vehicles assigned

**Relationships:**
- No complex performance tracking in memory
- Detailed metrics exported via logging system only

---
