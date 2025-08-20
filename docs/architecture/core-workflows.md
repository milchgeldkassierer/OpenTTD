# Core Workflows

## AI Initialization and Capital Deployment

```mermaid
sequenceDiagram
    participant OpenTTD
    participant UltimateMoneyAI
    participant FinanceManager
    participant PerformanceLogger
    
    OpenTTD->>UltimateMoneyAI: Start()
    UltimateMoneyAI->>PerformanceLogger: LogStartup()
    UltimateMoneyAI->>FinanceManager: InitializeCapital()
    FinanceManager->>OpenTTD: GetMaxLoanAmount()
    OpenTTD-->>FinanceManager: €600,000
    FinanceManager->>OpenTTD: SetLoanAmount(600000)
    FinanceManager->>PerformanceLogger: LogFinancialState(loan_taken)
    FinanceManager-->>UltimateMoneyAI: Capital ready: €600k
    UltimateMoneyAI->>UltimateMoneyAI: Begin route discovery
```

## Route Discovery and ROI-Based Selection

```mermaid
sequenceDiagram
    participant UltimateMoneyAI
    participant IndustryScanner
    participant RouteEvaluator
    participant PerformanceLogger
    participant FinanceManager
    
    UltimateMoneyAI->>IndustryScanner: ScanAllIndustries()
    IndustryScanner->>OpenTTD: GetIndustryList(COAL|ORE|GOLD)
    OpenTTD-->>IndustryScanner: Industry list
    
    loop For each viable industry
        IndustryScanner->>IndustryScanner: EvaluateProduction(industry)
        IndustryScanner->>IndustryScanner: FindNearestDestination(industry)
        IndustryScanner->>IndustryScanner: CreateRouteCandidate(industry)
        IndustryScanner->>RouteEvaluator: CalculateROI(candidate)
        RouteEvaluator->>RouteEvaluator: EstimateConstructionCost()
        RouteEvaluator->>RouteEvaluator: EstimateRevenue()
        RouteEvaluator-->>IndustryScanner: ROI percentage
        IndustryScanner->>PerformanceLogger: LogRouteEvaluation(candidate, decision)
    end
    
    IndustryScanner->>RouteEvaluator: MeetsROIThreshold(best_candidate)
    RouteEvaluator-->>IndustryScanner: ACCEPT/REJECT
    IndustryScanner-->>UltimateMoneyAI: Best route candidate
    UltimateMoneyAI->>FinanceManager: CheckFinancialSafety()
    FinanceManager-->>UltimateMoneyAI: Investment approved
```

## Route Construction and Vehicle Deployment

```mermaid
sequenceDiagram
    participant UltimateMoneyAI
    participant RouteBuilder
    participant PerformanceLogger
    participant FinanceManager
    participant OpenTTD
    
    UltimateMoneyAI->>RouteBuilder: BuildRoute(approved_candidate)
    RouteBuilder->>FinanceManager: GetFinancialSnapshot()
    FinanceManager-->>RouteBuilder: Pre-build finances
    
    RouteBuilder->>OpenTTD: BuildStations(source, destination)
    OpenTTD-->>RouteBuilder: Station construction result
    RouteBuilder->>PerformanceLogger: LogConstructionProgress(stations)
    
    RouteBuilder->>OpenTTD: BuildTrack(path)
    OpenTTD-->>RouteBuilder: Track construction result
    RouteBuilder->>PerformanceLogger: LogConstructionProgress(track)
    
    alt Construction successful
        RouteBuilder->>OpenTTD: DeployVehicles(route)
        RouteBuilder->>OpenTTD: SetupOrders(vehicles)
        RouteBuilder->>PerformanceLogger: LogConstructionComplete(success, costs)
    else Construction failed
        RouteBuilder->>RouteBuilder: RetryFailedConstruction()
        alt Retry failed
            RouteBuilder->>RouteBuilder: RecoverFromConstructionFailure()
            RouteBuilder->>PerformanceLogger: LogConstructionComplete(failed, costs)
        end
    end
    
    RouteBuilder-->>UltimateMoneyAI: Route operational status
```

## Monthly Performance Monitoring and Analysis

```mermaid
sequenceDiagram
    participant OpenTTD
    participant UltimateMoneyAI
    participant RouteManager
    participant FinanceManager
    participant PerformanceLogger
    
    OpenTTD->>UltimateMoneyAI: ManageTick() [Monthly trigger]
    UltimateMoneyAI->>RouteManager: MonitorRoutePerformance()
    
    loop For each active route
        RouteManager->>OpenTTD: GetVehiclePerformance(route_vehicles)
        RouteManager->>RouteManager: CalculateRouteProfitability()
        
        alt Route underperforming
            RouteManager->>RouteManager: ShutdownUnprofitableRoute(route_id)
            RouteManager->>PerformanceLogger: LogRouteShutdown(route_id, reason)
        else Route profitable
            RouteManager->>PerformanceLogger: LogRoutePerformance(route_id, metrics)
        end
    end
    
    UltimateMoneyAI->>FinanceManager: GetFinancialSnapshot()
    FinanceManager->>OpenTTD: GetCompanyFinancials()
    FinanceManager-->>UltimateMoneyAI: Current financial state
    UltimateMoneyAI->>PerformanceLogger: LogMonthlyPerformance()
    
    Note over PerformanceLogger: Machine-readable logs exported for<br/>external bash analysis and Serena MCP
```

---
