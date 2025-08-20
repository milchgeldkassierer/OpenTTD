# Database Schema

The Ultimate OpenTTD AI system does not use traditional external databases. Instead, it works within OpenTTD's embedded environment using Squirrel's native data structures and relies on external log files for persistent data storage.

## Data Storage Architecture

**In-Memory Structures (Squirrel Tables/Arrays):**
```squirrel
// Financial state tracking
financial_state <- {
    company_value = 0,
    bank_balance = 0, 
    loan_amount = 0,
    month_year = 0  // YYYYMM format
}

// Active route tracking
active_routes <- [
    {
        route_id = 1,
        monthly_profit = 0,
        active = true,
        vehicle_count = 0
    }
    // Additional routes...
]

// Route candidate evaluation cache
route_candidates <- [
    {
        source_industry = 0,      // Industry ID
        destination = 0,          // Tile index
        cargo_type = 0,           // 0=Coal, 1=Ore, 2=Gold
        construction_cost = 0,
        expected_annual_revenue = 0,
        roi_percentage_x100 = 0,  // ROI * 100 for integer precision
        distance_tiles = 0,
        production_capacity = 0
    }
    // Additional candidates...
]
```

## Persistent Storage Strategy

**Log-Based Persistence:**
- **Performance Logs:** Machine-readable debug output in standardized format
- **Configuration Files:** Simple text files for AI parameters and thresholds
- **Serena MCP Memory:** External knowledge base for optimization history

**File Storage Locations:**
```
docs/iteration_logs/
├── iteration-01-YYYYMMDD-HHMMSS.log    # Complete performance data
├── iteration-02-YYYYMMDD-HHMMSS.log    # Subsequent test runs
└── analysis-results/                    # Bash script outputs

.serena/
├── optimization_attempts.md             # MCP memory files
├── failed_optimizations.md
├── parameter_experiments.md
└── strategic_decisions.md
```

## Data Integrity Approach

**No ACID Transactions:** Squirrel environment doesn't support database transactions
**Validation Strategy:** Input sanitization and data type verification before processing
**Recovery Method:** Rebuild state from OpenTTD API calls after game load
**Backup Strategy:** All critical data flows through comprehensive logging system

---
