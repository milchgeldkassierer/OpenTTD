# Coding Standards

These standards are **MANDATORY** for AI development and will directly control code generation behavior.

## General Principles

### Memory Efficiency First
- Squirrel 2.2.5 has 128MB memory limit - every allocation counts
- Prefer local variables over class members
- Clear large data structures immediately after use
- Avoid deep object nesting and circular references

### Performance Within Limits
- Maximum 10,000 operations per execution cycle
- Use early returns to minimize unnecessary computation
- Cache expensive OpenTTD API calls when possible
- Prefer integer arithmetic over floating point

### Logging Integration
- Every decision point must be logged for analysis
- Use standardized PerformanceLogger format consistently
- Include context data (route_id, industry_id, etc.) in all logs

## Naming Conventions

### Classes
```squirrel
// PascalCase - Clear, descriptive names
class FinanceManager { }
class RouteEvaluator { }
class PerformanceLogger { }
```

### Functions and Methods
```squirrel
// camelCase - Verb-based names describing action
function calculateROI(route_candidate) { }
function buildRailTrack(start_tile, end_tile) { }
function logRouteEvaluation(candidate, decision) { }
```

### Variables
```squirrel
// snake_case - Descriptive, avoid abbreviations
local route_candidate = null;
local roi_percentage_x100 = 0;  // Use _x100 suffix for scaled integers
local construction_cost = 0;
local max_loan_amount = AICompany.GetMaxLoanAmount();
```

### Constants
```squirrel
// UPPER_SNAKE_CASE - Group related constants
const MIN_ROI_THRESHOLD = 15000;  // 150.00% as integer
const MAX_ROUTE_DISTANCE = 50;
const SAFETY_CASH_RESERVE = 50000;
const LOG_PREFIX_FINANCE = "FIN";
const LOG_PREFIX_ROUTE = "ROUTE";
```

### Files
```squirrel
// kebab-case with .nut extension
main.nut
finance.nut
route-evaluator.nut
performance-logger.nut
```

## Code Structure

### File Organization
```squirrel
// 1. Constants at top
const MIN_ROI_THRESHOLD = 15000;

// 2. Class definition
class FinanceManager {
    // 3. Member variables (minimize these)
    safety_reserve = SAFETY_CASH_RESERVE;
    
    // 4. Constructor
    constructor() {
        // Initialize only essential state
    }
    
    // 5. Public methods first
    function initializeCapital() { }
    
    // 6. Private methods last (prefix with _)
    function _validateCashReserves() { }
}
```

### Function Structure
```squirrel
function calculateROI(route_candidate) {
    // 1. Input validation first
    if (route_candidate == null) {
        PerformanceLogger.logError("ROUTE-001", "Null route candidate");
        return -1;
    }
    
    // 2. Early returns for invalid cases
    if (route_candidate.construction_cost <= 0) {
        return -1;
    }
    
    // 3. Main logic with clear variable names
    local annual_revenue = route_candidate.expected_annual_revenue;
    local operating_costs = _calculateOperatingCosts(route_candidate);
    local net_profit = annual_revenue - operating_costs;
    
    // 4. Result calculation
    local roi_percentage_x100 = (net_profit * 10000) / route_candidate.construction_cost;
    
    // 5. Logging before return
    PerformanceLogger.logRouteEvaluation(route_candidate, roi_percentage_x100);
    
    return roi_percentage_x100;
}
```

## Memory Management

### Variable Scope
```squirrel
// GOOD - Local variables auto-cleaned
function processRoutes() {
    local route_list = [];  // Will be garbage collected
    // ... process routes
    return result;  // route_list automatically freed
}

// BAD - Class member grows indefinitely
class RouteManager {
    all_routes = [];  // Grows forever, memory leak
}
```

### Data Structure Cleanup
```squirrel
// GOOD - Clear large structures immediately
function analyzeIndustries() {
    local industry_list = AIIndustryList();
    local candidates = [];
    
    // Process data
    foreach (industry_id, _ in industry_list) {
        // ... analysis
    }
    
    // Clear immediately after use
    industry_list.Clear();
    candidates.clear();
    
    return selected_candidate;
}
```

### OpenTTD API Efficiency
```squirrel
// GOOD - Cache expensive calls
local max_loan = AICompany.GetMaxLoanAmount();  // Call once
local current_loan = AICompany.GetLoanAmount();

// BAD - Repeated expensive calls
if (AICompany.GetLoanAmount() < AICompany.GetMaxLoanAmount()) {
    AICompany.SetLoanAmount(AICompany.GetMaxLoanAmount());
}
```

## Error Handling

### Standard Error Pattern
```squirrel
function buildRailStation(tile_location, width, height) {
    // 1. Input validation
    if (!AITile.IsValidTile(tile_location)) {
        PerformanceLogger.logError("BUILD-001", "Invalid tile: " + tile_location);
        return false;
    }
    
    // 2. Pre-condition checks
    if (!AITile.IsBuildable(tile_location)) {
        PerformanceLogger.logError("BUILD-002", "Tile not buildable: " + tile_location);
        return false;
    }
    
    // 3. Attempt operation with error handling
    if (!AIRail.BuildRailStation(tile_location, width, height, AIRail.RAILTRACK_NE_SW)) {
        local error_msg = "Station construction failed: " + AIError.GetLastErrorString();
        PerformanceLogger.logError("BUILD-003", error_msg);
        return false;
    }
    
    // 4. Success logging
    PerformanceLogger.logConstructionSuccess("station", tile_location, _getConstructionCost());
    return true;
}
```

### Error Code Standards
```squirrel
// Format: COMPONENT-NNN
const ERROR_FIN_INSUFFICIENT_FUNDS = "FIN-001";
const ERROR_ROUTE_INVALID_CANDIDATE = "ROUTE-001";
const ERROR_BUILD_CONSTRUCTION_FAILED = "BUILD-001";
const ERROR_LOG_INVALID_FORMAT = "LOG-001";
```

## Logging Requirements

### Mandatory Logging Points
```squirrel
// 1. All financial operations
AICompany.SetLoanAmount(600000);
PerformanceLogger.logFinancialTransaction("loan_acquired", 600000);

// 2. All route evaluations
local roi = calculateROI(candidate);
PerformanceLogger.logRouteEvaluation(candidate, roi, roi >= MIN_ROI_THRESHOLD);

// 3. All construction operations
if (buildRailStation(tile, 1, 4)) {
    PerformanceLogger.logConstructionSuccess("station", tile, cost);
} else {
    PerformanceLogger.logConstructionFailure("station", tile, error_code);
}

// 4. Performance milestones
PerformanceLogger.logMonthlyPerformance(current_month, company_value, profit);
```

### Log Format Consistency
```squirrel
// Use standardized format from PerformanceLogger spec
PerformanceLogger.logRouteEvaluation(
    candidate.source_industry,      // Industry ID
    candidate.destination,          // Tile index
    candidate.cargo_type,          // Cargo type integer
    candidate.construction_cost,    // Cost in euros
    candidate.expected_annual_revenue,  // Revenue projection
    roi_percentage_x100,           // ROI as percentage * 100
    decision_approved              // Boolean approval
);
```

## Performance Optimization

### Integer Arithmetic
```squirrel
// GOOD - Integer math for precision and speed
local roi_percentage_x100 = (annual_profit * 10000) / construction_cost;
local distance_squared = dx * dx + dy * dy;  // Avoid sqrt when possible

// BAD - Floating point (slower, precision issues)
local roi_percentage = annual_profit.tofloat() / construction_cost.tofloat() * 100.0;
```

### Loop Optimization
```squirrel
// GOOD - Early termination, minimal work per iteration
function findBestRoute(candidate_list) {
    local best_roi = 0;
    local best_candidate = null;
    
    foreach (candidate in candidate_list) {
        // Skip obviously bad candidates early
        if (candidate.construction_cost > available_budget) continue;
        if (candidate.distance_tiles > MAX_ROUTE_DISTANCE) continue;
        
        local roi = calculateROI(candidate);  // Expensive operation last
        if (roi > best_roi) {
            best_roi = roi;
            best_candidate = candidate;
        }
    }
    
    return best_candidate;
}
```

### API Call Minimization
```squirrel
// GOOD - Batch API queries
local industry_list = AIIndustryList();
foreach (industry_id, _ in industry_list) {
    if (AIIndustry.GetIndustryType(industry_id) == coal_type) {
        // Process coal industry
    }
}

// BAD - Repeated list creation
for (local i = 0; i < 100; i++) {
    local industry_list = AIIndustryList();  // Expensive repeated call
    // ...
}
```

## Comments and Documentation

### Function Documentation
```squirrel
/**
 * Berechnet ROI für eine Routenkandidaten in Basispunkten
 * 
 * @param route_candidate RouteCandidate Objekt mit allen erforderlichen Daten
 * @return Integer ROI als Prozentsatz * 100 (z.B. 15000 = 150.00%)
 *         Gibt -1 zurück bei ungültigen Eingaben
 */
function calculateROI(route_candidate) {
    // Implementierung...
}
```

### Inline Comments
```squirrel
// Verwende Integer-Arithmetik für Präzision (vermeidet Float-Rundungsfehler)
local roi_percentage_x100 = (net_annual_profit * 10000) / construction_cost;

// Prüfe ROI-Schwellwert (15000 = 150.00% Mindest-ROI)
if (roi_percentage_x100 >= MIN_ROI_THRESHOLD) {
    // Route genehmigt für Konstruktion
    return true;
}
```

### Complex Logic Explanation
```squirrel
// Terrain-Kostenfaktor: Berücksichtigt Steigungen, Wasser und Hindernisse
// Formel: Basiskost * (1 + steigung_faktor + wasser_faktor + hindernis_faktor)
local terrain_multiplier = 1000 + slope_penalty + water_crossing_penalty;
local adjusted_cost = base_construction_cost * terrain_multiplier / 1000;
```

## Security and Safety

### Input Validation
```squirrel
function transferCargo(source_tile, dest_tile, cargo_amount) {
    // Validiere alle OpenTTD API Eingaben
    if (!AITile.IsValidTile(source_tile) || !AITile.IsValidTile(dest_tile)) {
        return false;
    }
    
    // Validiere Geschäftslogik
    if (cargo_amount <= 0 || cargo_amount > MAX_CARGO_CAPACITY) {
        return false;
    }
    
    // Prüfe Finanzsicherheit vor teuren Operationen
    if (AICompany.GetBankBalance(AICompany.COMPANY_SELF) < SAFETY_CASH_RESERVE) {
        PerformanceLogger.logError("FIN-001", "Insufficient cash reserves");
        return false;
    }
    
    // Sichere Operation durchführen
    return _executeCargoTransfer(source_tile, dest_tile, cargo_amount);
}
```

### Financial Safety
```squirrel
// Immer Sicherheitsreserven vor großen Ausgaben prüfen
function attemptConstruction(estimated_cost) {
    local current_cash = AICompany.GetBankBalance(AICompany.COMPANY_SELF);
    local post_construction_cash = current_cash - estimated_cost;
    
    if (post_construction_cash < SAFETY_CASH_RESERVE) {
        PerformanceLogger.logError("FIN-002", "Construction would violate safety reserves");
        return false;
    }
    
    return true;  // Safe to proceed
}
```

## Testing Patterns

### Validation Functions
```squirrel
// Erstelle Validierungsfunktionen für kritische Datenstrukturen
function validateRouteCandidate(candidate) {
    if (candidate == null) return false;
    if (candidate.source_industry <= 0) return false;
    if (candidate.destination <= 0) return false;
    if (candidate.construction_cost <= 0) return false;
    if (candidate.expected_annual_revenue <= 0) return false;
    return true;
}

// Verwende Validierung vor kritischen Operationen
function processRoute(candidate) {
    if (!validateRouteCandidate(candidate)) {
        PerformanceLogger.logError("ROUTE-001", "Invalid route candidate");
        return false;
    }
    
    // Sichere Verarbeitung...
}
```

### State Verification
```squirrel
// Überprüfe Systemzustand vor kritischen Operationen
function ensureOperationalReadiness() {
    // Finanzielle Bereitschaft
    assert(AICompany.GetBankBalance(AICompany.COMPANY_SELF) >= SAFETY_CASH_RESERVE);
    
    // Systemzustand
    assert(AICompany.ResolveCompanyID(AICompany.COMPANY_SELF) != AICompany.COMPANY_INVALID);
    
    // Logging-System
    assert(PerformanceLogger != null);
    
    return true;
}
```

## File Organization Best Practices

### Directory Structure
```
ai/ultimate-money-ai/
├── main.nut              // UltimateMoneyAI Hauptcontroller
├── finance.nut           // FinanceManager
├── industry.nut          // IndustryScanner  
├── route.nut             // RouteEvaluator
├── builder.nut           // RouteBuilder
├── manager.nut           // RouteManager
├── logger.nut            // PerformanceLogger
├── utils.nut             // Hilfsfunktionen
└── info.nut              // AI-Metadaten
```

### Import Organization
```squirrel
// main.nut - Zentrale Importe in logischer Reihenfolge
require("logger.nut");     // Logging zuerst (wird überall verwendet)
require("utils.nut");      // Hilfsfunktionen als nächstes
require("finance.nut");    // Kernkomponenten
require("industry.nut");
require("route.nut");
require("builder.nut");
require("manager.nut");
```

## Standards Enforcement

These standards are **verpflichtend** for all Squirrel code development. They ensure:

- **Speicher-Effizienz** within the 128MB limit
- **Performance** within the 10k operations limit  
- **Wartbarkeit** for iterative development cycles
- **Konsistente Protokollierung** for analysis pipeline
- **Fehlerbehandlung** for robust AI operation

Every code review must validate these standards. Deviations are only allowed with documented justification.

---
