# PERFORMANCE LOGGING SPECIFICATION

*Standardized Debug Output for AI Performance Measurement*
*Version 1.0 - For 5-Year Test Runs*
*Last Updated: 2025-01-28*

---

## **🎯 LOGGING OBJECTIVES**

Define exactly what debug information the AI must output to enable systematic MEASURE → ANALYZE → OPTIMIZE cycles during 5-year test runs.

**Critical Goal**: Every log entry must be machine-readable for automated performance analysis.

---

## **📊 REQUIRED LOG CATEGORIES**

### **1. STARTUP & INITIALIZATION LOGS**

#### **Financial Baseline (Must Log Once at Start):**
```
[UMAI-INIT] === ULTIMATE MONEY AI v1.0 STARTING ===
[UMAI-INIT] Start Date: [GAME_DATE]
[UMAI-INIT] Starting Money: €[AMOUNT]
[UMAI-INIT] Taking Maximum Loan: €[LOAN_AMOUNT]
[UMAI-INIT] Total Available Capital: €[TOTAL_CAPITAL]
[UMAI-INIT] Investment Budget: €[BUDGET_AMOUNT]
[UMAI-INIT] === INITIALIZATION COMPLETE ===
```

#### **Game Environment Info:**
```
[UMAI-ENV] Map Size: [WIDTH]x[HEIGHT]
[UMAI-ENV] Climate: [CLIMATE_TYPE]
[UMAI-ENV] Competitors: [COMPETITOR_COUNT]
[UMAI-ENV] Difficulty: [DIFFICULTY_LEVEL]
```

---

### **2. ROUTE ANALYSIS & SELECTION LOGS**

#### **Industry Scanning Results (Log Each Candidate):**
```
[UMAI-SCAN] === INDUSTRY SCAN RESULTS ===
[UMAI-SCAN] Coal Mines Found: [COUNT]
[UMAI-SCAN] Ore Mines Found: [COUNT]  
[UMAI-SCAN] Gold Mines Found: [COUNT]
[UMAI-SCAN] Total Candidates: [TOTAL_COUNT]
```

#### **Route Evaluation Details (Log Each Route Analyzed):**
```
[UMAI-ROUTE] Evaluating: Industry_[ID] ([INDUSTRY_NAME])
[UMAI-ROUTE] Location: [TILE_X],[TILE_Y]
[UMAI-ROUTE] Cargo: [CARGO_TYPE]
[UMAI-ROUTE] Production: [AMOUNT] tons/month
[UMAI-ROUTE] Nearest Destination: [DEST_NAME] at [DEST_X],[DEST_Y]
[UMAI-ROUTE] Distance: [DISTANCE] tiles
[UMAI-ROUTE] Terrain Difficulty: [DIFFICULTY_SCORE]
[UMAI-ROUTE] Estimated Construction Cost: €[COST]
[UMAI-ROUTE] Expected Annual Revenue: €[REVENUE]
[UMAI-ROUTE] Calculated ROI: [ROI]%
[UMAI-ROUTE] Route Decision: [ACCEPT/REJECT] - [REASON]
```

#### **Final Route Selection:**
```
[UMAI-SELECT] === ROUTE SELECTION COMPLETE ===
[UMAI-SELECT] Best Route: Industry_[ID] -> [DESTINATION]
[UMAI-SELECT] ROI: [ROI]% (Target: >150%)
[UMAI-SELECT] Investment Required: €[AMOUNT]
[UMAI-SELECT] Expected Payback: [MONTHS] months
[UMAI-SELECT] === CONSTRUCTION STARTING ===
```

---

### **3. CONSTRUCTION PROGRESS LOGS**

#### **Construction Milestones:**
```
[UMAI-BUILD] === CONSTRUCTION PHASE ===
[UMAI-BUILD] Money Before Construction: €[AMOUNT]
[UMAI-BUILD] Building Source Station at [X],[Y]: [SUCCESS/FAILED]
[UMAI-BUILD] Building Rail Track [DISTANCE] tiles: [SUCCESS/FAILED]
[UMAI-BUILD] Building Destination Station at [X],[Y]: [SUCCESS/FAILED]
[UMAI-BUILD] Building Depot at [X],[Y]: [SUCCESS/FAILED]
[UMAI-BUILD] Total Construction Cost: €[ACTUAL_COST]
[UMAI-BUILD] Money After Construction: €[AMOUNT]
[UMAI-BUILD] === CONSTRUCTION COMPLETE ===
```

#### **Vehicle Deployment:**
```
[UMAI-VEHICLE] Purchasing Train: [ENGINE_NAME] for €[COST]
[UMAI-VEHICLE] Train ID: [VEHICLE_ID]
[UMAI-VEHICLE] Capacity: [CAPACITY] tons
[UMAI-VEHICLE] Orders Set: [SOURCE] -> [DESTINATION] -> [DEPOT]
[UMAI-VEHICLE] Vehicle Started: [SUCCESS/FAILED]
```

---

### **4. MONTHLY PERFORMANCE LOGS**

#### **Financial Summary (Every Game Month):**
```
[UMAI-MONTHLY] === MONTH [YEAR]-[MONTH] REPORT ===
[UMAI-MONTHLY] Company Value: €[VALUE]
[UMAI-MONTHLY] Bank Balance: €[BALANCE]
[UMAI-MONTHLY] Current Loan: €[LOAN]
[UMAI-MONTHLY] Monthly Income: €[INCOME]
[UMAI-MONTHLY] Monthly Expenses: €[EXPENSES]
[UMAI-MONTHLY] Net Profit: €[PROFIT]
[UMAI-MONTHLY] Running Vehicles: [COUNT]
```

#### **Route Performance (Each Route, Monthly):**
```
[UMAI-ROUTE-PERF] Route_[ID]: [SOURCE] -> [DESTINATION]
[UMAI-ROUTE-PERF] Cargo Transported: [AMOUNT] tons
[UMAI-ROUTE-PERF] Route Revenue: €[REVENUE]
[UMAI-ROUTE-PERF] Route Costs: €[COSTS]
[UMAI-ROUTE-PERF] Route Profit: €[PROFIT]
[UMAI-ROUTE-PERF] Vehicle Utilization: [PERCENTAGE]%
[UMAI-ROUTE-PERF] Current ROI: [ROI]%
```

---

### **5. ANNUAL PERFORMANCE LOGS**

#### **Yearly Summary (End of Each Game Year):**
```
[UMAI-ANNUAL] === YEAR [YEAR] SUMMARY ===
[UMAI-ANNUAL] Starting Company Value: €[START_VALUE]
[UMAI-ANNUAL] Ending Company Value: €[END_VALUE]
[UMAI-ANNUAL] Annual Growth: €[GROWTH] ([PERCENTAGE]%)
[UMAI-ANNUAL] Total Routes Built: [COUNT]
[UMAI-ANNUAL] Profitable Routes: [PROFIT_COUNT]/[TOTAL_COUNT]
[UMAI-ANNUAL] Best Route ROI: [BEST_ROI]%
[UMAI-ANNUAL] Fleet Size: [VEHICLE_COUNT] vehicles
[UMAI-ANNUAL] Total Cargo Transported: [AMOUNT] tons
[UMAI-ANNUAL] Company Ranking: #[RANK] of [TOTAL_COMPANIES]
```

#### **Competitive Analysis (Yearly):**
```
[UMAI-COMPETITIVE] === COMPETITIVE POSITION YEAR [YEAR] ===
[UMAI-COMPETITIVE] Our Company Value: €[OUR_VALUE]
[UMAI-COMPETITIVE] Best Competitor: €[BEST_COMPETITOR_VALUE]
[UMAI-COMPETITIVE] Performance Gap: [PERCENTAGE]% [AHEAD/BEHIND]
[UMAI-COMPETITIVE] Market Share: [PERCENTAGE]%
[UMAI-COMPETITIVE] Growth Rate vs Best: [PERCENTAGE]% [FASTER/SLOWER]
```

---

### **6. CRITICAL EVENT LOGS**

#### **Financial Alerts:**
```
[UMAI-ALERT] LOW CASH WARNING: €[AMOUNT] (Threshold: €50,000)
[UMAI-ALERT] BANKRUPTCY RISK: Immediate action required
[UMAI-ALERT] LOAN CAPACITY: €[AVAILABLE] additional loan available
[UMAI-ALERT] INVESTMENT OPPORTUNITY: Route ROI>[THRESHOLD]% available
```

#### **Route Performance Alerts:**
```
[UMAI-ALERT] ROUTE UNDERPERFORMING: Route_[ID] ROI=[CURRENT]% (Target: [TARGET]%)
[UMAI-ALERT] ROUTE FAILURE: Route_[ID] operating at loss for [MONTHS] months
[UMAI-ALERT] VEHICLE BREAKDOWN: Train_[ID] requires depot service
[UMAI-ALERT] PRODUCTION CHANGE: Industry_[ID] production changed to [NEW_AMOUNT]
```

---

### **7. FINAL TEST SUMMARY (After 5 Years)**

#### **Complete Performance Summary:**
```
[UMAI-FINAL] === 5-YEAR TEST COMPLETE ===
[UMAI-FINAL] Test Duration: [START_DATE] to [END_DATE]
[UMAI-FINAL] AI Version: [VERSION]
[UMAI-FINAL] Starting Money: €[START_MONEY]
[UMAI-FINAL] Final Company Value: €[FINAL_VALUE]
[UMAI-FINAL] Total Growth: €[TOTAL_GROWTH] ([PERCENTAGE]%)
[UMAI-FINAL] Average Annual Growth: [AVG_GROWTH]%
[UMAI-FINAL] Best Year Performance: Year [YEAR] (+[GROWTH]%)
[UMAI-FINAL] Worst Year Performance: Year [YEAR] (+[GROWTH]%)
[UMAI-FINAL] Total Routes Built: [COUNT]
[UMAI-FINAL] Success Rate: [PROFITABLE]/[TOTAL] ([PERCENTAGE]%)
[UMAI-FINAL] Best Route ROI Achieved: [BEST_ROI]%
[UMAI-FINAL] Average Route ROI: [AVG_ROI]%
[UMAI-FINAL] Total Vehicles Operated: [COUNT]
[UMAI-FINAL] Total Cargo Transported: [AMOUNT] tons
[UMAI-FINAL] Final Competitive Ranking: #[RANK] of [TOTAL]
[UMAI-FINAL] === TEST ANALYSIS READY ===
```

---

## **💻 SQUIRREL IMPLEMENTATION FRAMEWORK**

### **Logging Class Structure:**
```squirrel
class PerformanceLogger {
    // Financial tracking
    static start_money = 0;
    static monthly_data = [];
    static annual_data = [];
    
    // Route tracking
    static routes = {};
    static route_performance = {};
    
    // Initialization logging
    static function LogStartup() {
        start_money = AICompany.GetBankBalance();
        local loan = AICompany.GetLoanAmount();
        
        AILog.Info("[UMAI-INIT] === ULTIMATE MONEY AI v1.0 STARTING ===");
        AILog.Info("[UMAI-INIT] Start Date: " + AIDate.GetCurrentDate());
        AILog.Info("[UMAI-INIT] Starting Money: €" + start_money);
        AILog.Info("[UMAI-INIT] Taking Maximum Loan: €" + loan);
        AILog.Info("[UMAI-INIT] Total Available Capital: €" + (start_money + loan));
        AILog.Info("[UMAI-INIT] Investment Budget: €400000");
        AILog.Info("[UMAI-INIT] === INITIALIZATION COMPLETE ===");
    }
    
    // Route evaluation logging
    static function LogRouteEvaluation(industry_id, cargo_type, production, 
                                     destination, distance, cost, revenue, roi, decision) {
        AILog.Info("[UMAI-ROUTE] Evaluating: Industry_" + industry_id);
        AILog.Info("[UMAI-ROUTE] Cargo: " + cargo_type);
        AILog.Info("[UMAI-ROUTE] Production: " + production + " tons/month");
        AILog.Info("[UMAI-ROUTE] Distance: " + distance + " tiles");
        AILog.Info("[UMAI-ROUTE] Estimated Construction Cost: €" + cost);
        AILog.Info("[UMAI-ROUTE] Expected Annual Revenue: €" + revenue);
        AILog.Info("[UMAI-ROUTE] Calculated ROI: " + roi + "%");
        AILog.Info("[UMAI-ROUTE] Route Decision: " + decision);
    }
    
    // Monthly performance logging
    static function LogMonthlyPerformance() {
        local date = AIDate.GetCurrentDate();
        local year = AIDate.GetYear(date);
        local month = AIDate.GetMonth(date);
        local value = AICompany.GetCompanyValue(AICompany.COMPANY_SELF);
        local balance = AICompany.GetBankBalance();
        local loan = AICompany.GetLoanAmount();
        
        AILog.Info("[UMAI-MONTHLY] === MONTH " + year + "-" + month + " REPORT ===");
        AILog.Info("[UMAI-MONTHLY] Company Value: €" + value);
        AILog.Info("[UMAI-MONTHLY] Bank Balance: €" + balance);
        AILog.Info("[UMAI-MONTHLY] Current Loan: €" + loan);
        
        // Store for analysis
        monthly_data.append({
            date = date,
            value = value,
            balance = balance,
            loan = loan
        });
    }
    
    // Annual summary logging
    static function LogAnnualSummary() {
        local current_year = AIDate.GetYear(AIDate.GetCurrentDate());
        local current_value = AICompany.GetCompanyValue(AICompany.COMPANY_SELF);
        
        if (annual_data.len() > 0) {
            local last_year_value = annual_data.top().value;
            local growth = current_value - last_year_value;
            local growth_percent = (growth * 100) / last_year_value;
            
            AILog.Info("[UMAI-ANNUAL] === YEAR " + current_year + " SUMMARY ===");
            AILog.Info("[UMAI-ANNUAL] Ending Company Value: €" + current_value);
            AILog.Info("[UMAI-ANNUAL] Annual Growth: €" + growth + " (" + growth_percent + "%)");
        }
        
        annual_data.append({
            year = current_year,
            value = current_value
        });
    }
}
```

---

## **📋 LOGGING IMPLEMENTATION CHECKLIST**

### **Integration into AI Code:**
- [ ] **Startup Logging**: Call `PerformanceLogger.LogStartup()` in `Start()` method
- [ ] **Route Logging**: Log every route evaluation with all parameters
- [ ] **Monthly Logging**: Call monthly logging every 30 game days
- [ ] **Annual Logging**: Call yearly summary every January 1st
- [ ] **Event Logging**: Log all construction, financial, and performance events

### **Data Collection Automation:**
- [ ] **Log File Parsing**: Create script to extract performance data from logs
- [ ] **Metric Calculation**: Automated ROI, growth rate, ranking calculations
- [ ] **Comparison Tools**: Scripts to compare different AI versions
- [ ] **Visualization**: Charts showing performance trends over 5 years

---

## **🎯 MEASUREMENT SUCCESS CRITERIA**

### **After 5-Year Test Run, We Must Be Able to Answer:**
1. **Financial Performance**: What was the exact company value growth?
2. **Route Success Rate**: How many routes were profitable vs total built?
3. **ROI Achievement**: Did we achieve target >150% ROI on routes?
4. **Competitive Position**: How did we rank against other AIs?
5. **Growth Consistency**: Was growth steady or volatile?
6. **Best Decisions**: Which routes/strategies drove best performance?
7. **Failure Points**: Which decisions cost us money or growth?

### **Log Analysis Automation:**
```bash
# Extract key metrics from AI log
grep "\[UMAI-ANNUAL\]" openttd.log | tail -5
grep "\[UMAI-FINAL\]" openttd.log
grep "\[UMAI-ROUTE\] Route Decision: ACCEPT" openttd.log | wc -l
```

---

## **🚀 READY FOR SYSTEMATIC MEASUREMENT**

With this logging specification, every 5-year test run will generate complete performance data for systematic ANALYZE and OPTIMIZE phases.

**Next Steps:**
1. **Implement Logging**: Integrate `PerformanceLogger` into your AI code
2. **Test Logging**: Run short test to verify all log outputs work
3. **Run 5-Year Test**: Complete test with full performance logging
4. **Analyze Data**: Use logs to measure against success criteria
5. **Optimize Strategy**: Use findings to improve AI for next iteration

**🎯 Goal**: Every log entry enables data-driven optimization of your ultimate money-making AI!

---

*This logging specification ensures you can systematically measure, analyze, and optimize your AI's performance with concrete data rather than guesswork.*