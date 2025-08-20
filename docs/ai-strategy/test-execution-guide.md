# TEST EXECUTION & LOG COLLECTION GUIDE

*How to Run AI Tests and Collect Performance Data*
*Version 1.0 - For Iteration Testing*
*Last Updated: 2025-01-28*

---

## **🎯 TEST EXECUTION OVERVIEW**

After completing your AI development, follow this exact process to run standardized tests and collect performance data for the MEASURE → ANALYZE → OPTIMIZE phases.

---

## **🚀 RUNNING THE AI TEST**

### **Test Command:**
```bash
./build/openttd -d script=5 -g TestAI.sav
```

**Command Breakdown:**
- `./build/openttd` - Start OpenTTD from build directory
- `-d script=5` - Enable maximum debug logging for AI scripts
- `-g TestAI.sav` - Load your standardized test scenario save game

### **Debug Log Output:**
- **Terminal Output**: All AI debug logs display in real-time on terminal
- **Log Format**: Matches your [Performance Logging Spec](./performance-logging-spec.md)
- **Test Duration**: Run for 5 game years minimum (or full test scenario)

---

## **📁 LOG COLLECTION SYSTEM**

### **Automated Log Capture:**
```bash
# Capture all debug output to timestamped log file
./build/openttd -d script=5 -g TestAI.sav 2>&1 | tee docs/iteration_logs/iteration-01-$(date +%Y%m%d-%H%M%S).log
```

**This command:**
- ✅ Runs the test with full debug logging
- ✅ Shows output in terminal (real-time monitoring)  
- ✅ Saves complete log to timestamped file
- ✅ Stores in organized iteration logs folder

### **Log File Naming Convention:**
```
docs/iteration_logs/
├── iteration-01-20250128-143022.log    # Iteration 1, timestamp
├── iteration-02-20250130-091544.log    # Iteration 2, timestamp
├── iteration-03-20250201-164833.log    # Iteration 3, timestamp
└── README.md                           # Log collection guide
```

---

## **📊 LOG COLLECTION SETUP**

### **Pre-Test Setup Commands:**
```bash
# Create iteration logs directory
mkdir -p docs/iteration_logs

# Create log collection helper script
cat > run-ai-test.sh << 'EOF'
#!/bin/bash
# AI Test Runner with Automatic Log Collection

# Check if save game exists
if [ ! -f "TestAI.sav" ]; then
    echo "❌ Error: TestAI.sav not found!"
    echo "Create a test save game first with appropriate settings:"
    echo "  - 256x256 temperate map"
    echo "  - Easy difficulty"
    echo "  - 2-3 competitor AIs"
    echo "  - Starting year 1950"
    exit 1
fi

# Get iteration number from user
read -p "Enter iteration number (e.g., 01, 02): " ITERATION
TIMESTAMP=$(date +%Y%m%d-%H%M%S)
LOGFILE="docs/iteration_logs/iteration-${ITERATION}-${TIMESTAMP}.log"

# Create logs directory if it doesn't exist
mkdir -p docs/iteration_logs

echo "🚀 Starting AI Test - Iteration ${ITERATION}"
echo "📝 Log file: ${LOGFILE}"
echo "⏱️  Start time: $(date)"
echo "🎮 Press Ctrl+C to stop test and analyze logs"
echo ""

# Run test with log collection
./build/openttd -d script=5 -g TestAI.sav 2>&1 | tee "${LOGFILE}"

echo ""
echo "✅ Test completed!"
echo "📊 Log saved to: ${LOGFILE}"
echo "📈 Ready for MEASURE phase analysis"
EOF

# Make script executable
chmod +x run-ai-test.sh
```

### **Quick Test Execution:**
```bash
# Simple one-command test run
./run-ai-test.sh
```

---

## **🔍 LOG ANALYSIS PREPARATION**

### **Essential Log Extraction Commands:**
```bash
# Extract key performance metrics from log file
LOGFILE="docs/iteration_logs/iteration-01-20250128-143022.log"

# Financial Performance Summary
echo "=== FINANCIAL PERFORMANCE ==="
grep "\[UMAI-ANNUAL\]" "$LOGFILE"
grep "\[UMAI-FINAL\]" "$LOGFILE"

# Route Success Analysis  
echo -e "\n=== ROUTE ANALYSIS ==="
grep "\[UMAI-ROUTE\] Route Decision: ACCEPT" "$LOGFILE" | wc -l
grep "\[UMAI-ROUTE\] Calculated ROI:" "$LOGFILE"

# Monthly Growth Tracking
echo -e "\n=== MONTHLY GROWTH ==="
grep "\[UMAI-MONTHLY\] Company Value:" "$LOGFILE" | tail -10

# Critical Events
echo -e "\n=== ALERTS & ISSUES ==="
grep "\[UMAI-ALERT\]" "$LOGFILE"
```

### **Automated Analysis Script:**
```bash
# Create log analysis helper
cat > analyze-logs.sh << 'EOF'
#!/bin/bash
# AI Log Analysis Tool

if [ $# -eq 0 ]; then
    echo "Usage: ./analyze-logs.sh <log-file>"
    echo "Example: ./analyze-logs.sh docs/iteration_logs/iteration-01-20250128-143022.log"
    exit 1
fi

LOGFILE="$1"
if [ ! -f "$LOGFILE" ]; then
    echo "❌ Error: Log file not found: $LOGFILE"
    exit 1
fi

echo "📊 ANALYZING LOG: $LOGFILE"
echo "================================"

# Extract key metrics
START_VALUE=$(grep "\[UMAI-INIT\] Starting Money:" "$LOGFILE" | tail -1 | grep -o "€[0-9,]*" | tr -d '€,')
FINAL_VALUE=$(grep "\[UMAI-FINAL\] Final Company Value:" "$LOGFILE" | tail -1 | grep -o "€[0-9,]*" | tr -d '€,')
ROUTES_BUILT=$(grep "\[UMAI-ROUTE\] Route Decision: ACCEPT" "$LOGFILE" | wc -l)
BEST_ROI=$(grep "\[UMAI-ROUTE\] Calculated ROI:" "$LOGFILE" | grep -o "[0-9]*%" | sort -nr | head -1)

echo "💰 Starting Money: €$START_VALUE"
echo "💰 Final Value: €$FINAL_VALUE"
if [ -n "$START_VALUE" ] && [ -n "$FINAL_VALUE" ]; then
    GROWTH=$((FINAL_VALUE - START_VALUE))
    GROWTH_PERCENT=$((GROWTH * 100 / START_VALUE))
    echo "📈 Total Growth: €$GROWTH ($GROWTH_PERCENT%)"
fi
echo "🛤️  Routes Built: $ROUTES_BUILT"
echo "🎯 Best ROI Achieved: $BEST_ROI"

echo -e "\n📋 DETAILED ANALYSIS:"
echo "=== Route Decisions ==="
grep "\[UMAI-ROUTE\] Route Decision:" "$LOGFILE"

echo -e "\n=== Annual Summaries ==="
grep "\[UMAI-ANNUAL\]" "$LOGFILE"

echo -e "\n=== Critical Alerts ==="
grep "\[UMAI-ALERT\]" "$LOGFILE"

echo -e "\n✅ Analysis complete! Use this data for ANALYZE → OPTIMIZE phases."
EOF

chmod +x analyze-logs.sh
```

---

## **📋 TEST EXECUTION CHECKLIST**

### **Pre-Test Preparation:**
- [ ] **AI Implementation Complete**: All code written and tested
- [ ] **Logging Integration**: PerformanceLogger class implemented per spec
- [ ] **Test Scenario Ready**: TestAI.sav created with standard settings
- [ ] **Log Collection Setup**: Run log collection setup commands above
- [ ] **Directory Structure**: `docs/iteration_logs/` folder created

### **During Test Execution:**
- [ ] **Monitor Console Output**: Watch for errors or unexpected behavior
- [ ] **Verify Logging**: Confirm log entries match [Performance Logging Spec](./performance-logging-spec.md)
- [ ] **Note Issues**: Document any crashes, errors, or anomalies
- [ ] **Test Duration**: Run for full 5 game years minimum

### **Post-Test Data Collection:**
- [ ] **Log File Saved**: Timestamped log file in `docs/iteration_logs/`
- [ ] **Quick Analysis**: Run `analyze-logs.sh` for immediate insights
- [ ] **Performance Summary**: Extract key metrics for MEASURE phase
- [ ] **Issue Documentation**: Note any problems for ANALYZE phase

---

## **🎯 SUCCESS CRITERIA VERIFICATION**

### **Minimum Test Success:**
- ✅ AI runs for full test duration without crashes
- ✅ Complete log file generated with all required entries
- ✅ Financial performance data captured (startup → monthly → annual → final)
- ✅ Route analysis data shows decision making process

### **Quality Test Success:**
- 🎯 All log entries match Performance Logging Spec format
- 🎯 No critical alerts or bankruptcy warnings
- 🎯 Route success rate > 50% (at least half of attempts successful)
- 🎯 Positive company growth over 5-year period

---

## **⚠️ COMMON TESTING ISSUES**

### **Test Setup Problems:**
- **Missing TestAI.sav**: Create standardized test save game first
- **Wrong OpenTTD Path**: Verify `./build/openttd` exists and is executable
- **Permission Issues**: Ensure write access to `docs/iteration_logs/` folder

### **AI Runtime Issues:**
- **Early Crash**: Check AI syntax and API usage
- **No Log Output**: Verify PerformanceLogger implementation
- **Bankruptcy**: Review financial strategy and safety checks

### **Log Collection Issues:**
- **Missing Logs**: Verify redirect command `2>&1 | tee` working properly
- **Incomplete Data**: Ensure test runs for full duration
- **Format Problems**: Check log entries match specification exactly

---

## **🔄 INTEGRATION WITH ITERATIVE WORKFLOW**

### **After Test Completion:**
1. **MEASURE Phase**: Use `analyze-logs.sh` to extract performance data
2. **ANALYZE Phase**: Compare results to success criteria and previous iterations
3. **OPTIMIZE Phase**: Identify improvements based on log analysis
4. **REPEAT Phase**: Run next iteration with updated AI

### **Version Comparison:**
```bash
# Compare multiple iteration logs
./analyze-logs.sh docs/iteration_logs/iteration-01-*.log
./analyze-logs.sh docs/iteration_logs/iteration-02-*.log

# Track improvement over iterations
grep "Total Growth:" docs/iteration_logs/*.log
```

---

## **📚 INTEGRATION WITH BUILD PROMPT**

Add this section to your [iteration-01-build-prompt.md](./iteration-01-build-prompt.md) checklist:

### **Post-Development Testing:**
- [ ] **Setup Test Environment**: Follow [test-execution-guide.md](./test-execution-guide.md)
- [ ] **Create TestAI.sav**: Generate standardized test scenario
- [ ] **Run AI Test**: Execute `./run-ai-test.sh` for 5-year performance test
- [ ] **Collect Logs**: Verify complete log file in `docs/iteration_logs/`
- [ ] **Analyze Results**: Run `analyze-logs.sh` for performance summary
- [ ] **Document Findings**: Prepare for ANALYZE → OPTIMIZE phases

---

**🎯 Goal: Systematic, repeatable testing with complete performance data collection for data-driven AI optimization!**

---

*This guide ensures every AI iteration generates complete, analyzable performance data for systematic improvement.*