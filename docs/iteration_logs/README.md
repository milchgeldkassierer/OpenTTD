# ITERATION LOGS FOLDER

This folder contains test execution logs from AI Developer test runs.

## File Naming Convention:
```
iteration-XX-YYYYMMDD-HHMMSS.log
```

Example:
- `iteration-01-20250128-143022.log` - Iteration 1, ran on Jan 28, 2025 at 14:30:22

## Log Content:
Each log file contains complete debug output from AI test runs following the [Performance Logging Specification](../ai-strategy/performance-logging-spec.md).

## Usage:
- **AI Developer**: Generates these files during test execution
- **Analytics Developer**: Analyzes these files for performance measurement
- **Both**: Reference for tracking progress across iterations