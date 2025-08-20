# Source Tree

```
OpenTTD/
├── ai/ultimate-money-ai/               # Core AI implementation
│   ├── info.nut                        # AI metadata and registration
│   ├── main.nut                        # UltimateMoneyAI main controller
│   ├── finance.nut                     # FinanceManager component
│   ├── industry.nut                    # IndustryScanner component
│   ├── route.nut                       # RouteEvaluator component
│   ├── builder.nut                     # RouteBuilder component
│   ├── manager.nut                     # RouteManager component
│   ├── logger.nut                      # PerformanceLogger component
│   ├── utils.nut                       # Utility functions and helpers
│   └── README.txt                      # AI description and version info
│
├── docs/                               # Complete documentation
│   ├── ultimate-openttd-ai-prd.md     # Product requirements
│   ├── architecture.md                # This architecture document
│   ├── ai-strategy/                   # Implementation guides
│   │   ├── ultimate-ai-development-strategy.md
│   │   ├── iterative-workflow.md
│   │   ├── ai-developer-guide.md
│   │   ├── analytics-developer-guide.md
│   │   ├── performance-logging-spec.md
│   │   ├── test-execution-guide.md
│   │   ├── development-environment.md
│   │   ├── developer-handoff-protocol.md
│   │   ├── brainstorming-session-results.md
│   │   └── squirrel225.chm
│   └── iteration_logs/                # Performance test data
│       ├── iteration-01-YYYYMMDD-HHMMSS.log
│       ├── iteration-02-YYYYMMDD-HHMMSS.log
│       └── analysis-results/          # Bash script outputs
│
├── scripts/                           # Analysis and testing tools
│   ├── run-ai-test.sh                 # Automated test execution
│   ├── analyze-logs.sh                # Performance metric extraction
│   ├── extract-metrics.sh             # Detailed data analysis
│   └── test-scenarios/                # Standardized test save games
│       ├── TestAI.sav                 # Basic profitability test
│       ├── Competition.sav            # Multi-AI competitive test
│       └── Subsidy.sav                # Advanced feature test
│
├── .serena/                           # Serena MCP knowledge base
│   ├── optimization_attempts.md       # Complete attempt history
│   ├── failed_optimizations.md        # Anti-pattern database
│   ├── parameter_experiments.md       # Parameter tuning history
│   ├── strategic_decisions.md         # Decision rationale archive
│   ├── iteration_patterns.md          # Cross-iteration patterns
│   └── competitive_analysis.md        # Market intelligence
│
├── .bmad-core/                        # BMad framework files
│   ├── core-config.yaml              # Project configuration
│   ├── tasks/                         # Workflow definitions
│   ├── templates/                     # Document templates
│   └── data/                          # Reference data
│
├── .git/                              # Version control
├── .gitignore                         # Ignore patterns
├── README.md                          # Project overview
└── CHANGELOG.md                       # Version history
```

---
