# Task Completion Checklist for OpenTTD

## Code Quality Checks
Since no automated linting/formatting tools were found in the project configuration, manual verification is required:

### 1. Code Style Compliance
- [ ] Follow CamelCase for function names
- [ ] Use lowercase with underscores for variables
- [ ] Proper brace placement (opening brace on next line)
- [ ] Align variable declarations by spaces
- [ ] Use `this->` for class members
- [ ] Follow enum naming conventions

### 2. Documentation Requirements
- [ ] All new functions are documented
- [ ] Complex code sections have explanatory comments
- [ ] Comments explain WHY, not just WHAT
- [ ] Documentation is clear and helpful for reviewers

### 3. Build Verification
```bash
# Verify build succeeds
cmake --build .

# Verify tests pass
./openttd_test
# OR
ctest
```

### 4. Code Integration
- [ ] New code follows existing patterns in the codebase
- [ ] Dependencies are properly declared if new libraries used
- [ ] Headers are included appropriately
- [ ] No compilation warnings introduced

### 5. Testing
- [ ] Unit tests written for new functionality (if applicable)
- [ ] Manual testing performed
- [ ] Regression tests pass (if applicable)

### 6. Git Workflow
- [ ] Changes committed with descriptive messages
- [ ] No sensitive data or credentials committed
- [ ] Proper branch management if using feature branches

## Common Issues to Check
- Memory leaks (C++ manual memory management)
- Null pointer dereferences
- Array bounds checking
- Proper resource cleanup
- Thread safety (if applicable)

## Platform Considerations
- Test on target platforms if possible
- Consider endianness issues
- Verify cross-platform compatibility

## Performance Considerations
- Profile performance-critical code
- Avoid unnecessary allocations in hot paths
- Consider cache-friendly data structures
- Optimize for the common case