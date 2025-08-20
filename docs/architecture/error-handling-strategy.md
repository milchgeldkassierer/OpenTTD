# Error Handling Strategy

## General Approach
- **Error Model:** Defensive programming with graceful degradation
- **Exception Hierarchy:** Squirrel native error handling with custom error types via tables
- **Error Propagation:** Local error handling with comprehensive logging for analysis

## Logging Standards
- **Library:** OpenTTD AILog.Info() native logging
- **Format:** Standardized format per Performance Logging Specification
- **Levels:** INFO (standard), ALERT (problems), ERROR (critical failures)
- **Required Context:**
  - Correlation ID: Route ID or operation identifier when applicable
  - Service Context: Component name (FINANCE, ROUTE, BUILD, etc.)
  - User Context: N/A (autonomous AI system)

## Error Handling Patterns

### External API Errors
- **Retry Policy:** 3 attempts with exponential backoff for OpenTTD API failures
- **Circuit Breaker:** Disable problematic routes after 5 consecutive failures
- **Timeout Configuration:** No explicit timeouts (OpenTTD manages execution cycles)
- **Error Translation:** Convert OpenTTD API errors to standard AI decision points

### Business Logic Errors
- **Custom Exceptions:** Error tables with type, message, and recovery action fields
- **User-Facing Errors:** All errors logged to debug output (no direct user interface)
- **Error Codes:** Standardized prefixes: FIN- (financial), ROUTE- (routing), BUILD- (construction)

### Data Consistency
- **Transaction Strategy:** No formal transactions; rebuild state from OpenTTD API on errors
- **Compensation Logic:** Reverse construction operations on failure, liquidate failed routes
- **Idempotency:** All operations check current state before executing

---
