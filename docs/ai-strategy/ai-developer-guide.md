# AI DEVELOPER GUIDE - Iteration #1

*Role: AI Programming & Test Execution Only*
*Version 1.0*
*Last Updated: 2025-01-28*

---

## **👨‍💻 YOUR ROLE: AI DEVELOPER**

**You are responsible for:**
- ✅ **AI Programming**: Write Squirrel code for the AI
- ✅ **Logging Implementation**: Add comprehensive debug logging
- ✅ **Test Execution**: Run the AI and collect log files
- ✅ **Handoff**: Deliver complete log files to Analytics Developer

**You are NOT responsible for:**
- ❌ **Performance Analysis**: Analytics Developer handles this
- ❌ **Optimization Decisions**: Analytics Developer determines improvements  
- ❌ **Next Iteration Planning**: Analytics Developer creates next prompts

---

## **📚 REQUIRED READING**

Before coding, review these documents:

### **Essential for AI Development:**
- **[Development Environment](./development-environment.md)** - Squirrel 2.2.5 setup & optimization
- **[Performance Logging Spec](./performance-logging-spec.md)** - **CRITICAL** - Exact logging format
- **[AI Master Analysis](../AI_MASTER_ANALYSIS.md)** - OpenTTD API reference (Parts 2 & 4)

### **Reference Materials:**
- **[Master Strategy](./ultimate-ai-development-strategy.md)** - Overall project goals
- **[Squirrel 2.2.5 Documentation](./squirrel225.chm)** - Language reference
- **[OpenTTD Script Wiki](https://wiki.openttd.org/en/Development/Script/Squirrel)** - Best practices

---

## **🎯 ITERATION #1 BUILD REQUIREMENTS**

### **Build Objective:**
Create the **simplest possible profitable AI** that proves the basic money-making strategy works.

### **Success Criteria:**
- ✅ AI doesn't go bankrupt (maintains >€50,000 cash)
- ✅ Builds at least one profitable coal/ore route
- ✅ Route generates positive profit within 2 game years
- ✅ Complete logging per specification

---

## **💰 FINANCIAL STRATEGY**

### **Immediate Actions:**
```squirrel
function Start() {
    // Take maximum loan for aggressive expansion
    local max_loan = AICompany.GetMaxLoanAmount();
    AICompany.SetLoanAmount(max_loan);
    
    // Log startup (REQUIRED for Analytics)
    PerformanceLogger.LogStartup();
}
```

### **Investment Strategy:**
- **Total Capital**: €600,000 (loan + starting money)
- **Investment Budget**: €400,000 for aggressive route building
- **Safety Threshold**: Keep >€50,000 cash reserve

---

## **🚂 AI IMPLEMENTATION REQUIREMENTS**

### **Route Selection Logic:**
1. **Cargo Focus**: Coal or Iron Ore ONLY
2. **Distance Limit**: Maximum 50 tiles
3. **Terrain**: Flat ground only (no bridges/tunnels)
4. **ROI Target**: Minimum 150% return on investment
5. **Production**: Minimum 100 tons/month

### **Construction Strategy:**
- **Single Route**: Build only ONE route in Iteration #1
- **Simple Stations**: 1-platform, 4-tile length
- **Direct Track**: Point-to-point connection
- **Basic Signals**: Block signals only
- **One Depot**: Near source station

---

## **📊 LOGGING IMPLEMENTATION (MANDATORY)**

### **Required Logging System:**
**⚠️ CRITICAL**: Implement the complete `PerformanceLogger` class from [Performance Logging Spec](./performance-logging-spec.md)

### **Essential Log Categories:**
- **Startup Logs**: Financial baseline, environment info
- **Route Analysis**: Every candidate evaluation with ROI
- **Construction Progress**: Build costs, success/failure
- **Monthly Performance**: Financial summaries
- **Annual Reports**: Growth rates, competitive position

### **Implementation Example:**
```squirrel
// Use exact format from performance-logging-spec.md
PerformanceLogger.LogStartup();
PerformanceLogger.LogRouteEvaluation(industry_id, cargo_type, production, 
                                   destination, distance, cost, revenue, roi, decision);
PerformanceLogger.LogMonthlyPerformance();
PerformanceLogger.LogAnnualSummary();
```

**⚠️ Without proper logging, Analytics Developer cannot measure performance!**

---

## **🔧 IMPLEMENTATION TASKS**

### **Task 1: Financial Foundation**
- [ ] Implement maximum loan acquisition
- [ ] Create financial safety checks
- [ ] Add startup logging

### **Task 2: Route Discovery**
- [ ] Scan for coal/ore mines
- [ ] Check production levels
- [ ] Find accepting destinations
- [ ] Log all candidates found

### **Task 3: Route Evaluation**
- [ ] Calculate construction costs
- [ ] Estimate annual revenue
- [ ] Compute ROI percentage
- [ ] Log evaluation details

### **Task 4: Construction**
- [ ] Build rail track and stations
- [ ] Purchase and deploy train
- [ ] Set up basic orders
- [ ] Log construction progress

### **Task 5: Performance Monitoring**
- [ ] Implement monthly/annual logging
- [ ] Track route profitability
- [ ] Monitor financial health
- [ ] Generate final summary

---

## **🧪 TEST EXECUTION**

### **Test Setup:**
```bash
# Create test scenario save game with:
# - 256x256 temperate map
# - Easy difficulty  
# - 2-3 competitor AIs
# - Starting year 1950
```

### **Test Execution Command:**
```bash
# Run AI test with full logging
./build/openttd -d script=5 -g TestAI.sav 2>&1 | tee docs/iteration_logs/iteration-01-$(date +%Y%m%d-%H%M%S).log
```

### **Test Duration:**
- **Minimum**: 5 game years for performance data
- **Recommended**: 10 game years for trend analysis
- **Monitor**: Watch for crashes, errors, bankruptcy

---

## **📁 PROJECT STRUCTURE**

### **AI Code Organization:**
```
ai/ultimate-money-ai/
├── info.nut          # AI metadata
├── main.nut          # Main AI control flow  
├── finance.nut       # Financial management
├── route.nut         # Route evaluation & construction
├── logger.nut        # PerformanceLogger implementation
└── README.txt        # AI description
```

### **Log File Location:**
```
docs/iteration_logs/
└── iteration-01-YYYYMMDD-HHMMSS.log    # Your test output
```

---

## **✅ COMPLETION CHECKLIST**

### **Pre-Development:**
- [ ] Environment setup complete
- [ ] Documentation reviewed
- [ ] Test scenario (TestAI.sav) created

### **During Development:**
- [ ] PerformanceLogger class implemented
- [ ] All required logging integrated
- [ ] Financial safety checks added
- [ ] Route evaluation logic complete

### **Testing Phase:**
- [ ] AI runs without crashes
- [ ] Complete log file generated
- [ ] Test duration: 5+ game years
- [ ] No bankruptcy or critical errors

### **Handoff to Analytics Developer:**
- [ ] **Log file delivered**: Complete iteration log in `docs/iteration_logs/`
- [ ] **AI code committed**: Version tagged as `v1.0-iteration-01`
- [ ] **Issues documented**: Any problems or anomalies noted
- [ ] **Test summary**: Brief description of AI behavior during test

---

## **🔄 HANDOFF PROCESS**

### **What You Deliver:**
1. **Complete Log File**: Full test run log with all required entries
2. **AI Source Code**: Committed and tagged version
3. **Test Summary**: Brief notes on AI behavior, any issues
4. **Status Report**: Success/failure against basic criteria

### **What Analytics Developer Does:**
1. **Performance Analysis**: Extract metrics from your log
2. **Optimization Planning**: Identify improvements needed
3. **Next Iteration Prompt**: Create requirements for Iteration #2
4. **Handoff Back**: Deliver new build requirements to you

---

## **⚠️ CRITICAL SUCCESS FACTORS**

### **Must Have for Analytics:**
- ✅ **Complete Logging**: Every log entry per specification
- ✅ **Consistent Format**: Exact format from performance-logging-spec.md
- ✅ **Full Test Duration**: Minimum 5 years of game data
- ✅ **No Missing Data**: All startup, monthly, annual, and final logs

### **Quality Indicators:**
- 🎯 **AI Survival**: No bankruptcy during test
- 🎯 **Route Success**: At least one profitable route built
- 🎯 **Positive Growth**: Company value increases over test period
- 🎯 **Clean Logs**: No errors or missing log entries

---

## **🎯 FOCUS ON YOUR ROLE**

**Your Job**: Write the AI code and run the test. Make sure logging is complete and accurate.

**Not Your Job**: Analyzing performance, deciding optimizations, planning next iteration.

**Success Metric**: Analytics Developer can extract all needed data from your log file to measure performance and plan improvements.

---

**🚀 Ready to code the AI! Focus on solid implementation and comprehensive logging.**

*Analytics Developer will handle all performance analysis and optimization planning based on your log data.*