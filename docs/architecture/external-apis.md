# External APIs

Based on the PRD requirements and component design, this project operates entirely within the OpenTTD game environment using the built-in Script API. The system does not require external web service integrations.

**No External APIs Required**

The Ultimate OpenTTD AI system is completely self-contained within the OpenTTD game engine. All necessary functionality is provided by:

- **OpenTTD Script API** - Complete game integration for AI operations
- **Serena MCP** - Knowledge base management (local system integration)
- **Local File System** - Log file storage and bash script analysis

**Internal API Dependencies:**

The AI relies exclusively on OpenTTD's comprehensive Script API which provides all necessary capabilities:
- Company management (finances, loans, vehicles)
- Industry scanning and cargo handling
- Rail construction and infrastructure management
- Tile analysis and pathfinding
- Vehicle orders and automation
- Competitive analysis and market data

---
