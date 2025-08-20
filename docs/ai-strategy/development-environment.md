# AI DEVELOPMENT ENVIRONMENT SETUP

*Development Environment for Ultimate Money-Making AI*
*Last Updated: 2025-01-28*

---

## **🐿️ SQUIRREL 2.2.5 SCRIPTING ENVIRONMENT**

### **Core Language Specifications:**
- **Language**: Squirrel 2.2.5 stable with OpenTTD modifications
- **VM Type**: Register-based virtual machine with bytecode compilation
- **Documentation**: `docs/ai-strategy/squirrel225.chm` (Complete language reference)
- **Wiki Reference**: https://wiki.openttd.org/en/Development/Script/Squirrel

### **OpenTTD Integration:**
- **Memory Limit**: 128MB default (configurable)
- **Operation Limit**: 10,000 operations per execution cycle
- **Execution Model**: Frame-based with automatic suspension/resume
- **API Access**: Full OpenTTD Script API available

---

## **🔧 DEVELOPMENT SETUP CHECKLIST**

### **Required Files & Documentation:**
- [ ] **Squirrel Reference**: `docs/ai-strategy/squirrel225.chm`
- [ ] **OpenTTD Wiki**: https://wiki.openttd.org/en/Development/Script/Squirrel
- [ ] **AI Master Analysis**: `AI_MASTER_ANALYSIS.md` (API reference)
- [ ] **Development Strategy**: All docs in `docs/ai-strategy/`

### **Development Environment:**
- [ ] **OpenTTD Installation**: Latest stable version
- [ ] **AI Development Folder**: `ai/ultimate-money-ai/`
- [ ] **Text Editor**: With syntax highlighting for Squirrel
- [ ] **Testing Setup**: Standardized test scenarios ready

---

## **📁 AI PROJECT STRUCTURE**

### **Recommended File Organization:**
```
ai/ultimate-money-ai/
├── info.nut           # AI metadata and information
├── main.nut           # Main AI logic and control flow
├── finance.nut        # Financial management system
├── route.nut          # Route evaluation and construction
├── industry.nut       # Industry scanning and analysis
├── utils.nut          # Utility functions and helpers
└── README.txt         # AI description and version info
```

### **Essential Files for Iteration #1:**
```squirrel
// info.nut - AI Metadata
class UltimateMoneyAI extends AIInfo {
    function GetAuthor()      { return "AI Developer"; }
    function GetName()        { return "Ultimate Money AI"; }
    function GetDescription() { return "Aggressive money-making AI v1.0"; }
    function GetVersion()     { return 1; }
    function GetDate()        { return "2025-01-28"; }
    function CreateInstance() { return "UltimateMoneyAI"; }
    function GetShortName()   { return "UMAI"; }
}

RegisterAI(UltimateMoneyAI());
```

---

## **⚡ SQUIRREL OPTIMIZATION GUIDELINES**

### **Performance Best Practices:**
Based on OpenTTD Wiki optimizations and your AI_MASTER_ANALYSIS.md:

#### **1. Memory Management:**
```squirrel
// Efficient object creation and cleanup
local industry_list = AIIndustryList();
// Use local variables, avoid global state
// Clean up large objects when done

// Good: Local scope
function EvaluateRoute() {
    local candidates = [];
    // ... processing
    return best_candidate; // candidates auto-cleaned
}

// Avoid: Global arrays that grow indefinitely
```

#### **2. API Call Optimization:**
```squirrel
// Batch API calls efficiently
local tile_list = AITileList();
for (local tile = tile_list.Begin(); !tile_list.IsEnd(); tile = tile_list.Next()) {
    // Process multiple tiles in one loop
    local slope = AITile.GetSlope(tile);
    local accepts_coal = AITile.AcceptsCargo(tile, coal_cargo);
    // ... batch multiple checks
}

// Avoid: Repeated API calls in separate loops
```

#### **3. Efficient Data Structures:**
```squirrel
// Use arrays and tables efficiently
local route_cache = {}; // Cache expensive calculations
local industry_data = []; // Use arrays for sequential data

// Cache expensive pathfinding results
function GetCachedDistance(from, to) {
    local key = from + "_" + to;
    if (!(key in route_cache)) {
        route_cache[key] = AITile.GetDistanceManhattanToTile(from, to);
    }
    return route_cache[key];
}
```

#### **4. Operation Count Management:**
```squirrel
// Monitor operation usage to avoid suspension
local operation_count = 0;
for (local industry in AIIndustryList()) {
    // Do work
    operation_count++;
    
    // Yield control if approaching limit
    if (operation_count > 8000) {
        AIController.Sleep(1); // Yield and reset counter
        operation_count = 0;
    }
}
```

---

## **🧪 TESTING ENVIRONMENT SETUP**

### **OpenTTD Configuration:**
```ini
# openttd.cfg settings for AI development
[difficulty]
competitor_speed = 2              # Medium AI speed for testing
max_no_competitors = 3            # Limit competitors for testing

[ai]
ai_in_multiplayer = true         # Enable AI in multiplayer (for testing)
ai_disable_veh_train = false    # Allow trains
ai_disable_veh_roadveh = true   # Disable road vehicles (focus on trains)
ai_disable_veh_aircraft = true  # Disable aircraft
ai_disable_veh_ship = true      # Disable ships

[game_creation]
map_x = 8                       # 256x256 map (2^8)
map_y = 8                       # Good size for testing
```

### **Test Scenario Standards:**
- **Map Size**: 256x256 (small for fast testing)
- **Terrain**: Temperate climate
- **Starting Year**: 1950 (good train availability)
- **Industries**: High industry density
- **Towns**: Medium town density
- **Competitors**: 2-3 weak AIs for baseline

---

## **📊 DEBUGGING & LOGGING SETUP**

### **AI Console Commands:**
```
# Debug AI behavior
debug_level ai=1                 # Enable AI debugging
debug_level script=1             # Enable script debugging

# AI management
start_ai <company_id>            # Start AI manually
stop_ai <company_id>             # Stop AI
reload_ai <company_id>           # Reload AI script
```

### **Logging Framework:**
```squirrel
// Comprehensive logging for MEASURE phase
class Logger {
    static function Info(message) {
        AILog.Info("[UMAI] " + message);
    }
    
    static function Financial(action, before, after) {
        local change = after - before;
        AILog.Info("[FINANCE] " + action + ": €" + before + " -> €" + after + " (" + change + ")");
    }
    
    static function RouteAnalysis(industry, production, distance, roi) {
        AILog.Info("[ROUTE] " + industry + " | Prod:" + production + " | Dist:" + distance + " | ROI:" + roi + "%");
    }
}
```

---

## **🔍 DEVELOPMENT WORKFLOW**

### **Code → Test → Debug Cycle:**
1. **Write Code**: Implement specific functionality
2. **Load AI**: Start OpenTTD with new AI version
3. **Monitor Console**: Watch AI log output
4. **Check Performance**: Observe AI behavior in-game
5. **Debug Issues**: Use console commands and logs
6. **Iterate**: Fix issues and test again

### **Fast Development Tips:**
```squirrel
// Quick development helpers
function DebugTile(tile) {
    Logger.Info("Tile " + tile + ": Slope=" + AITile.GetSlope(tile) + 
                " Type=" + AITile.GetTileType(tile));
}

// Quick financial check
function ShowMoney() {
    local money = AICompany.GetBankBalance();
    local loan = AICompany.GetLoanAmount();
    Logger.Info("Money: €" + money + " | Loan: €" + loan + " | Net: €" + (money - loan));
}
```

---

## **⚠️ COMMON PITFALLS TO AVOID**

### **Squirrel-Specific Issues:**
- **Integer Overflow**: Squirrel uses 32-bit integers, be careful with large money values
- **String Concatenation**: Use `+` operator efficiently, avoid excessive string building
- **Array Bounds**: Always check array limits, no automatic bounds checking
- **Null Checking**: Always validate API results before use

### **OpenTTD AI Constraints:**
- **No DoCommands in Constructor**: Only in Start() and later methods
- **Operation Limits**: AI suspends after 10,000 operations
- **Memory Limits**: 128MB default limit, design accordingly
- **API Validation**: All commands validated, check preconditions

---

## **🎯 ITERATION #1 DEVELOPMENT CHECKLIST**

### **Pre-Development Setup:**
- [ ] **Environment Ready**: OpenTTD installed and configured
- [ ] **Documentation Access**: Squirrel reference and wiki bookmarked
- [ ] **File Structure**: AI folder created with basic files
- [ ] **Testing Scenario**: Standard test map prepared

### **Development Tools Ready:**
- [ ] **Text Editor**: Squirrel syntax highlighting enabled
- [ ] **Console Access**: AI debug commands memorized
- [ ] **Logging System**: Logger class implemented
- [ ] **Quick Test Setup**: Fast load/reload workflow established

### **Reference Materials:**
- [ ] **Squirrel 2.2.5 CHM**: Language reference available
- [ ] **OpenTTD Script API**: AI_MASTER_ANALYSIS.md Part 2 reviewed
- [ ] **Wiki Guide**: OpenTTD Squirrel development guide studied
- [ ] **Build Prompt**: iteration-01-build-prompt.md ready for implementation

---

## **🚀 READY FOR DEVELOPMENT!**

**Your development environment is now fully specified and ready for building the ultimate money-making AI.**

**Next Step**: Follow `iteration-01-build-prompt.md` to implement your first basic profitable AI using this Squirrel 2.2.5 environment.

**Success Criteria**: One profitable coal/ore route + comprehensive logging + no bankruptcy = Foundation for future optimization cycles.

---

*With Squirrel 2.2.5 and OpenTTD's robust API, you have all the tools needed to build the most profitable AI in OpenTTD history.*