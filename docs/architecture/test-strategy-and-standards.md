# Test Strategy and Standards

## Testing Philosophy
- **Approach:** In-game testing only - no unit tests possible for Squirrel scripts
- **Coverage Goals:** Functional validation through live AI behavior observation  
- **Test Method:** Manual execution in OpenTTD with comprehensive logging

## Test Reality for Squirrel Scripts
**No Traditional Testing Possible:**
- Squirrel 2.2.5 has no unit testing frameworks
- OpenTTD's embedded environment doesn't support automated testing
- No way to mock OpenTTD APIs or game state
- Only validation method: Run AI in actual game and observe behavior

## In-Game Testing Strategy

### Manual Observation Testing
- **Method:** Load AI in OpenTTD and watch behavior
- **Duration:** 5-year game runs minimum for performance data
- **Validation:** Monitor debug console for correct logging output
- **Success Criteria:** AI doesn't crash, builds routes, avoids bankruptcy

### Performance Testing  
- **Scope:** Complete AI operation in standardized game scenarios
- **Environment:** Consistent map settings and starting conditions
- **Data Collection:** Performance logs captured via debug output
- **Analysis:** Bash scripts extract metrics from log files

### Debugging Approach
- **Primary Method:** AILog.Info() debug statements throughout code
- **Error Detection:** Watch for exceptions in debug console
- **Behavioral Validation:** Observe AI construction and financial decisions
- **Performance Tracking:** Monitor company growth vs. competitors

## Test Scenarios
- **Basic Test:** Simple map, no competitors, verify basic functionality
- **Competition Test:** Multiple AIs, measure relative performance
- **Stress Test:** Complex map with difficult terrain and high competition

**Key Point:** Testing = Running the AI in-game and measuring results. No other testing method exists for embedded Squirrel scripts.

---
