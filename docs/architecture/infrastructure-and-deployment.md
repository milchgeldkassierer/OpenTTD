# Infrastructure and Deployment

Since this is a private local development project without cloud infrastructure needs, the deployment architecture focuses on local development workflow and iteration management.

## Infrastructure as Code
- **Tool:** N/A (Local development)
- **Location:** N/A
- **Approach:** Direct file system management and version control

## Deployment Strategy
- **Strategy:** Local manual deployment
- **CI/CD Platform:** N/A (Private project)
- **Pipeline Configuration:** Manual testing workflow via bash scripts

## Environments

- **Development:** Local OpenTTD installation with AI development folder
- **Testing:** Same local environment with standardized test scenarios
- **Production:** Player's OpenTTD game with deployed AI

## Environment Promotion Flow

```
Development → Testing → Production
     ↓           ↓          ↓
Edit .nut → Run tests → Copy to game
   files      Extract     AI folder
              metrics
```

## Rollback Strategy

- **Primary Method:** Git version control with tagged releases
- **Trigger Conditions:** Performance regression, critical bugs, bankruptcy in testing
- **Recovery Time Objective:** Immediate (git checkout previous version)

---
