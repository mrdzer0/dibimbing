---
  PERTEMUAN 2: Agentic AI & Model Context Protocol

  Total: 45-50 Slides | Durasi: 90-120 menit

  ---
  PEMBUKAAN & RECAP (10 menit)

  Slide 1: Title Slide

  AGENTIC AI & MODEL CONTEXT PROTOCOL
  Membangun AI yang Bisa Bertindak di Dunia Nyata

  Session 2 of 2
  [Nama Anda]
  [Tanggal]
  Visual: Background dengan konsep koneksi/network, MCP logo
  Speaker Notes: Welcome back, energize audience untuk session teknikal

  ---
  Slide 2: Quick Recap - Pertemuan 1

  📝 Last Session Recap:

  ✅ Evolusi AI: Rule-Based → ML → DL → LLM
  ✅ LLM Limitations: No real-world access
  ✅ Solution: Tool-Using AI
  ✅ Agentic AI: Autonomous, Goal-Oriented, Multi-Step

  Key Insight:
  "LLM alone = Smart but Blind
   LLM + Tools = Smart + Capable"
  Visual: Visual timeline dari pertemuan 1, simplified
  Speaker Notes: Quick 2-minute recap, refresh memory

  ---
  Slide 3: Agenda Hari Ini

  🗺️ Roadmap Pertemuan 2:

  Part 1: Deep Dive - Agentic AI Architecture (25 min)
     └─ Komponen, Patterns, Challenges

  Part 2: Model Context Protocol (MCP) (40 min)
     └─ Apa itu? Kenapa penting? Ekosistem

  Part 3: Hands-On Demos & Labs (45 min)
     └─ Setup MCP, Live demos, Build simple server

  Part 4: Future & Career Opportunities (10 min)
  Visual: Numbered sections dengan icons
  Speaker Notes: Emphasize banyak demo praktikal hari ini

  ---
  Slide 4: Learning Objectives

  🎯 By End of This Session, You Will:

  ✅ Understand arsitektur internal AI agents
  ✅ Know komponen-komponen agentic systems
  ✅ Understand MCP protocol & use cases
  ✅ Setup & configure MCP servers
  ✅ Build simple MCP integration
  ✅ Identify career opportunities in this space

  Bonus: Hands-on code samples & resources! 💻
  Visual: Checklist dengan icons
  Speaker Notes: Set clear expectations

  ---
  BAGIAN 1: DEEP DIVE AGENTIC AI (25 menit)

  Slide 5: Section Divider

  🤖 PART 1
  Anatomy of AI Agents
  Membedah Arsitektur Agentic AI
  Visual: Blueprint/technical drawing aesthetic
  Speaker Notes: Transisi ke bagian teknikal

  ---
  Slide 6: The Agent Loop - Core Concept

  🔄 Fundamental Agent Loop

  ┌─────────────────────────────────┐
  │  1. PERCEIVE (Input)            │
  │     • User request              │
  │     • Environment state         │
  └────────────┬────────────────────┘
               ↓
  ┌─────────────────────────────────┐
  │  2. REASON (Think)              │
  │     • Understand goal           │
  │     • Plan approach             │
  │     • Choose next action        │
  └────────────┬────────────────────┘
               ↓
  ┌─────────────────────────────────┐
  │  3. ACT (Execute)               │
  │     • Use tools                 │
  │     • Generate output           │
  └────────────┬────────────────────┘
               ↓
  ┌─────────────────────────────────┐
  │  4. OBSERVE (Feedback)          │
  │     • Check results             │
  │     • Update understanding      │
  └────────────┬────────────────────┘
               ↓
          [Loop back to step 2 or finish]
  Visual: Circular diagram dengan arrows, animated jika possible
  Speaker Notes: Ini adalah DNA dari semua agent systems

  ---
  Slide 7: Real Example - Agent in Action

  💡 Example: "Book me a restaurant for tonight"

  Step 1 - PERCEIVE:
     Input: User request + context (location, time, preferences)

  Step 2 - REASON:
     💭 "I need to:
         1. Check available restaurants
         2. Filter by user preferences
         3. Check availability
         4. Make reservation"

  Step 3 - ACT:
     🔧 Call tool: search_restaurants(location="Jakarta", cuisine="Italian")

  Step 4 - OBSERVE:
     📊 Result: Found 5 restaurants
     💭 "Good, now check availability..."

  [Loop continues until booking confirmed]
  Visual: Step-by-step flow dengan icons, progress indicator
  Speaker Notes: Make it relatable dengan real-world scenario

  ---
  Slide 8: Agent Components - The Full Stack

  🧩 Core Components of an AI Agent

  1. 🧠 REASONING ENGINE (Brain)
     └─ LLM: GPT-4, Claude, Gemini, etc.
     └─ Prompt engineering & chain-of-thought

  2. 💾 MEMORY SYSTEM
     └─ Short-term: Conversation context
     └─ Long-term: Vector databases, knowledge graphs

  3. 🛠️ TOOL INTERFACE
     └─ Function definitions
     └─ Execution layer
     └─ Error handling

  4. 📋 PLANNING MODULE
     └─ Task decomposition
     └─ Strategy selection

  5. 👁️ PERCEPTION LAYER
     └─ Input parsing
     └─ Context understanding

  6. 🎯 EXECUTION ENGINE
     └─ Action orchestration
     └─ State management
  Visual: Layered architecture diagram, color-coded components
  Speaker Notes: Analogi dengan OS komputer atau robot

  ---
  Slide 9: Memory Systems Explained

  💾 Agent Memory Architecture

  SHORT-TERM MEMORY (Working Memory):
  ┌─────────────────────────────────┐
  │ Current conversation            │
  │ Recent tool outputs             │
  │ Active task context             │
  │                                 │
  │ Limitation: Token window (~200K)│
  └─────────────────────────────────┘

  LONG-TERM MEMORY (Knowledge Base):
  ┌─────────────────────────────────┐
  │ Vector Database (embeddings)    │
  │ • Past conversations            │
  │ • Learned facts                 │
  │ • User preferences              │
  │                                 │
  │ Retrieval: Semantic search      │
  └─────────────────────────────────┘

  Example:
  User: "Remember I'm allergic to peanuts"
  → Stored in long-term memory
  → Retrieved when booking restaurants later
  Visual: Two-tier memory diagram dengan examples
  Speaker Notes: Analogi dengan human memory (RAM vs hard disk)

  ---
  Slide 10: Planning Strategies

  🎯 Agent Planning Approaches

  1. REACT (Reason + Act)
     Thought → Action → Observation → Thought...
     ✅ Simple, effective
     ❌ Can be inefficient

  2. PLAN-AND-EXECUTE
     Plan all steps → Execute sequentially
     ✅ Efficient, organized
     ❌ Less adaptive

  3. REFLEXION (Self-Reflection)
     Try → Fail → Reflect → Retry
     ✅ Learns from mistakes
     ❌ More API calls

  4. TREE OF THOUGHTS
     Explore multiple reasoning paths
     ✅ Better for complex problems
     ❌ Expensive

  5. MULTI-AGENT
     Different agents for different subtasks
     ✅ Specialized, parallel
     ❌ Coordination overhead
  Visual: 5 diagrams showing each approach visually
  Speaker Notes: Tidak ada "best" approach, tergantung use case

  ---
  Slide 11: Demo - Planning Strategy Comparison

  🧪 Live Demo: Different Planning Approaches

  Task: "Plan a trip to Bali"

  REACT Approach:
  💭 "Need destination info" → 🔍 Search Bali
  💭 "Need flights" → ✈️ Search flights
  💭 "Need hotels" → 🏨 Search hotels
  [Iterative, adaptive]

  PLAN-AND-EXECUTE:
  📋 Plan:
     1. Research Bali attractions
     2. Find flights
     3. Book hotel
     4. Create itinerary
  Then execute each step
  [More organized, faster]

  [Show side-by-side execution logs]
  Visual: Split screen comparison atau animation
  Speaker Notes: Bisa pakai LangChain dengan different agent types

  ---
  Slide 12: Tool Integration - How It Works

  🔧 Tool Calling Mechanism

  1. TOOL DEFINITION (What LLM sees):
  {
    "name": "get_weather",
    "description": "Get current weather for a location",
    "parameters": {
      "location": {"type": "string", "required": true},
      "units": {"type": "string", "enum": ["celsius", "fahrenheit"]}
    }
  }

  2. LLM DECISION:
  User: "What's the weather in Tokyo?"
  LLM thinks: "I need weather data"
  LLM outputs:
  {
    "tool": "get_weather",
    "arguments": {"location": "Tokyo", "units": "celsius"}
  }

  3. EXECUTION:
  System calls: get_weather("Tokyo", "celsius")
  Returns: {"temp": 18, "condition": "Cloudy"}

  4. LLM RESPONSE:
  "The weather in Tokyo is 18°C and cloudy."
  Visual: Step-by-step flow dengan JSON highlighting
  Speaker Notes: Ini adalah magic behind tool-using AI

  ---
  Slide 13: Tool Ecosystem - What's Available

  🌐 Common Tool Categories

  DATA ACCESS:
  • Database queries (SQL, MongoDB)
  • File systems (read/write/search)
  • APIs (REST, GraphQL)

  INFORMATION RETRIEVAL:
  • Web search (Google, Bing, DuckDuckGo)
  • Web scraping (Puppeteer, Playwright)
  • Document readers (PDF, DOCX)

  ACTIONS:
  • Email (send, read, filter)
  • Calendar (schedule, check availability)
  • Task management (create, update)

  COMPUTATION:
  • Calculators
  • Data analysis (pandas, numpy)
  • Code execution (Python, JavaScript)

  COMMUNICATION:
  • Slack, Discord, Teams
  • SMS, WhatsApp
  • Social media posting
  Visual: Icon grid, color-coded by category
  Speaker Notes: Agents powerful karena ecosystem tools yang luas

  ---
  Slide 14: Agent Challenges & Solutions

  ⚠️ Real-World Challenges

  CHALLENGE 1: Tool Hell 🔥
  Problem: Every tool has different API, format, auth
  Example:
    • Slack API ≠ Discord API ≠ Teams API
    • Each needs different integration code
    • Maintenance nightmare

  CHALLENGE 2: Context Management 📚
  Problem: Limited context window
  Solution: Smart memory systems, summarization

  CHALLENGE 3: Error Handling 🐛
  Problem: Tools fail, APIs timeout, bad data
  Solution: Retry logic, fallbacks, graceful degradation

  CHALLENGE 4: Security 🔒
  Problem: Agent has too much access
  Solution: Permission systems, sandboxing

  CHALLENGE 5: Cost 💰
  Problem: Many LLM calls = expensive
  Solution: Caching, smaller models for simple tasks

  → Enter: MODEL CONTEXT PROTOCOL (MCP)
  Visual: Problem-solution cards, highlight "Tool Hell" problema
  Speaker Notes: Setup untuk introduce MCP sebagai solusi

  ---
  Slide 15: The Fragmentation Problem

  🔥 The Tool Integration Problem

  Current State:
  ┌─────────────┐     ┌─────────────┐
  │   ChatGPT   │────→│ Custom Code │
  └─────────────┘     └─────────────┘
                            ↓
          ┌─────────────────┼─────────────────┐
          ↓                 ↓                 ↓
      [Slack API]      [Gmail API]      [GitHub API]

  Each integration = custom code, different format

  Problems:
  ❌ No standardization
  ❌ Can't reuse integrations
  ❌ Every AI app reinvents the wheel
  ❌ Maintenance burden
  ❌ Security inconsistencies

  We need: "USB for AI Tools" 🔌
  Visual: Messy spaghetti diagram showing complexity
  Speaker Notes: Paint the pain picture, motivate need for standard

  ---
  BAGIAN 2: PENGENALAN MCP (40 menit)

  Slide 16: Section Divider

  🔌 PART 2
  MODEL CONTEXT PROTOCOL
  The Universal Standard for AI Tools
  Visual: MCP logo, USB-like connector visual
  Speaker Notes: "Ini game-changer untuk AI ecosystem"

  ---
  Slide 17: What is MCP?

  🎯 Model Context Protocol (MCP)

  Definition:
  Open standard protocol untuk menghubungkan
  AI applications dengan external tools & data sources

  Created by: Anthropic (Claude team)
  Released: November 2024
  Status: Open source, community-driven

  Analogy:
  "MCP adalah USB untuk AI Agents"

  Before USB:
  ❌ Every device had different connector
  ❌ Can't share peripherals

  After USB:
  ✅ Universal connector
  ✅ Plug-and-play
  ✅ Works everywhere

  MCP does this for AI tools! 🚀
  Visual: USB evolution analogy diagram, MCP logo
  Speaker Notes: Emphasize "universal standard" concept

  ---
  Slide 18: The MCP Vision

  🌟 The Big Picture

  BEFORE MCP:
  AI App 1 → Custom integration → Tool A
  AI App 2 → Different integration → Tool A (reinvent!)
  AI App 3 → Another integration → Tool A (again!)

  [Everyone building the same thing differently]

  AFTER MCP:
  ┌──────────────────────────────────┐
  │  AI Applications (Hosts)         │
  │  ChatGPT, Claude, Custom Apps    │
  └────────────┬─────────────────────┘
               ↓
        [MCP Protocol] ← Universal Standard
               ↓
  ┌──────────────────────────────────┐
  │  MCP Servers (Once, Works Everywhere)│
  │  Slack, GitHub, Database, etc.   │
  └──────────────────────────────────┘

  Build once → Use everywhere! ✨
  Visual: Before/after architecture comparison
  Speaker Notes: This is why MCP is revolutionary

  ---
  Slide 19: MCP Architecture - The Layers

  🏗️ MCP Architecture

  ┌─────────────────────────────────────────┐
  │  HOST (AI Application)                  │
  │  • Claude Desktop, VS Code, Custom Apps │
  │  • Manages MCP connections              │
  │  • Orchestrates tool calls              │
  └────────────────┬────────────────────────┘
                   ↓
  ┌─────────────────────────────────────────┐
  │  MCP PROTOCOL (Communication Layer)     │
  │  • JSON-RPC based                       │
  │  • Standardized messages                │
  │  • Transport: stdio, HTTP, WebSocket    │
  └────────────────┬────────────────────────┘
                   ↓
  ┌─────────────────────────────────────────┐
  │  MCP SERVER (Tool Provider)             │
  │  • Exposes capabilities                 │
  │  • Implements MCP interface             │
  │  • Handles actual operations            │
  └────────────────┬────────────────────────┘
                   ↓
  ┌─────────────────────────────────────────┐
  │  EXTERNAL SERVICE                       │
  │  • Slack, GitHub, Database, Files, etc. │
  └─────────────────────────────────────────┘
  Visual: Layered architecture diagram dengan examples
  Speaker Notes: Explain each layer's role

  ---
  Slide 20: MCP Core Concepts

  📚 Three Main Primitives

  1. 🛠️ TOOLS (Functions)
     What agents can DO

     Example:
     - create_file(path, content)
     - send_email(to, subject, body)
     - query_database(sql)

  2. 📦 RESOURCES (Data)
     What agents can READ

     Example:
     - file://documents/report.pdf
     - db://users/table
     - api://github/repos/my-repo

  3. 💬 PROMPTS (Templates)
     Reusable prompt templates

     Example:
     - "Analyze code quality"
     - "Summarize meeting notes"
     - "Generate test cases"
  Visual: Three columns dengan icons dan examples
  Speaker Notes: Tools = verbs, Resources = nouns, Prompts = instructions

  ---
  Slide 21: MCP Tools Explained

  🛠️ Tools: The "Actions" Layer

  Structure:
  {
    "name": "create_github_issue",
    "description": "Create a new GitHub issue",
    "inputSchema": {
      "type": "object",
      "properties": {
        "repo": {"type": "string"},
        "title": {"type": "string"},
        "body": {"type": "string"}
      },
      "required": ["repo", "title"]
    }
  }

  Lifecycle:
  1. Host discovers available tools
  2. LLM decides to use a tool
  3. Host calls MCP server
  4. Server executes & returns result
  5. LLM processes result

  Benefits:
  ✅ Strongly typed (JSON Schema)
  ✅ Self-documenting
  ✅ Validation built-in
  Visual: JSON schema example dengan annotations
  Speaker Notes: Tools adalah workhorses dari agents

  ---
  Slide 22: MCP Resources Explained

  📦 Resources: The "Data" Layer

  What are Resources?
  Content that agents can read/access
  Each resource has a unique URI

  Examples:
  ┌─────────────────────────────────────┐
  │ file:///home/user/docs/report.pdf   │
  │ → MCP exposes file contents         │
  ├─────────────────────────────────────┤
  │ db://postgres/users                 │
  │ → MCP provides database access      │
  ├─────────────────────────────────────┤
  │ notion://page/abc123                │
  │ → MCP fetches Notion page           │
  └─────────────────────────────────────┘

  Why Resources?
  ✅ Standardized data access
  ✅ Permission control per resource
  ✅ Dynamic content (files, APIs, etc.)
  ✅ Read-only safety

  Use Case:
  "Summarize all PDFs in my documents folder"
  → Agent lists resources
  → Reads each via MCP
  → Summarizes
  Visual: URI examples dengan resource icons
  Speaker Notes: Resources give agents "eyes" to see data

  ---
  Slide 23: MCP Prompts Explained

  💬 Prompts: The "Templates" Layer

  What are MCP Prompts?
  Reusable, shareable prompt templates
  With variables & context injection

  Example Structure:
  {
    "name": "code_review",
    "description": "Review code for quality",
    "arguments": [
      {"name": "language", "description": "Programming language"},
      {"name": "focus", "description": "Review focus area"}
    ]
  }

  Template:
  "You are an expert {{language}} developer.
  Review the following code for {{focus}}.
  Consider: performance, security, readability.
  Code: {{code_content}}"

  Benefits:
  ✅ Consistency across projects
  ✅ Best practices sharing
  ✅ Community-driven templates
  ✅ Contextual prompts
  Visual: Template example dengan variable highlighting
  Speaker Notes: Prompts make expertise reusable

  ---
  Slide 24: MCP Ecosystem - What's Available

  🌐 MCP Server Ecosystem

  OFFICIAL SERVERS (by Anthropic):
  📁 @modelcontextprotocol/server-filesystem
     → Read/write local files

  🗄️ @modelcontextprotocol/server-postgres
     → Database queries

  🐙 @modelcontextprotocol/server-github
     → GitHub operations

  🌐 @modelcontextprotocol/server-puppeteer
     → Web scraping/automation

  💬 @modelcontextprotocol/server-slack
     → Slack integration

  📊 @modelcontextprotocol/server-gdrive
     → Google Drive access

  COMMUNITY SERVERS (growing daily):
  • Discord, Twitter, Notion
  • AWS, Google Cloud
  • Obsidian, Todoist
  • And 100+ more!

  Browse: https://github.com/modelcontextprotocol/servers
  Visual: Grid of server logos/icons dengan links
  Speaker Notes: Growing ecosystem, show GitHub page

  ---
  Slide 25: How MCP Actually Works

  🔄 MCP Communication Flow

  Example: "Create a file named hello.txt"

  1. USER → HOST:
     "Create a file named hello.txt with 'Hello World'"

  2. HOST → LLM:
     [Available tools: create_file, read_file, delete_file]
     "What should I do?"

  3. LLM → HOST:
     {
       "tool": "create_file",
       "arguments": {
         "path": "hello.txt",
         "content": "Hello World"
       }
     }

  4. HOST → MCP SERVER (via MCP protocol):
     {
       "method": "tools/call",
       "params": {
         "name": "create_file",
         "arguments": {...}
       }
     }

  5. MCP SERVER → FILESYSTEM:
     [Actually creates the file]

  6. MCP SERVER → HOST:
     {"success": true, "message": "File created"}

  7. HOST → LLM → USER:
     "✅ I've created hello.txt with the content!"
  Visual: Sequence diagram dengan numbered steps
  Speaker Notes: Walk through step-by-step, pause di setiap step

  ---
  Slide 26: MCP vs Traditional Integration

  ⚖️ Comparison: Traditional vs MCP

  TRADITIONAL APPROACH:
  ┌─────────────────────────────────┐
  │ Your AI App                     │
  │   ├─ Custom Slack code (500 LOC)│
  │   ├─ Custom GitHub code (400 LOC)│
  │   ├─ Custom DB code (300 LOC)  │
  │   └─ Auth, error handling, etc. │
  └─────────────────────────────────┘

  Problems:
  ❌ Reinvent for each tool
  ❌ Different error patterns
  ❌ Maintenance burden
  ❌ Can't share with others
  ❌ Security inconsistencies

  MCP APPROACH:
  ┌─────────────────────────────────┐
  │ Your AI App                     │
  │   └─ MCP Client (50 LOC)       │
  └──────────┬──────────────────────┘
             ↓ (Uses MCP Protocol)
  ┌──────────────────────────────────┐
  │ MCP Servers (Built Once)         │
  │ @mcp/slack, @mcp/github, @mcp/db │
  └──────────────────────────────────┘

  Benefits:
  ✅ Plug-and-play
  ✅ Community maintained
  ✅ Standardized security
  ✅ 10x less code
  ✅ Works with all MCP hosts
  Visual: Side-by-side architecture + LOC comparison bar chart
  Speaker Notes: Quantify the benefit (10x less code adalah real)

  ---
  Slide 27: Real-World MCP Use Cases

  💼 MCP in Action - Use Cases

  1. 📝 CONTENT CREATION AGENT
     Tools: filesystem, web-search, image-generation
     Workflow: Research → Write → Generate images → Save

  2. 💻 CODING ASSISTANT
     Tools: github, filesystem, terminal
     Workflow: Read code → Understand → Write → Commit

  3. 📊 DATA ANALYST AGENT
     Tools: postgres, sqlite, csv-reader
     Workflow: Query → Analyze → Visualize → Report

  4. 📧 EMAIL AUTOMATION
     Tools: gmail, calendar, contacts
     Workflow: Read → Classify → Draft response → Schedule

  5. 🔍 RESEARCH ASSISTANT
     Tools: web-scrape, pdf-reader, note-taking
     Workflow: Search → Read → Synthesize → Organize

  6. 🏢 BUSINESS OPERATIONS
     Tools: slack, notion, google-sheets
     Workflow: Monitor → Alert → Update → Report
  Visual: 6 cards dengan workflow diagrams
  Speaker Notes: Show video demos kalau ada

  ---
  Slide 28: MCP Security Model

  🔒 Security & Permissions

  PRINCIPLE: Principle of Least Privilege

  Host Control:
  ┌─────────────────────────────────┐
  │ User must explicitly:           │
  │ • Install MCP server            │
  │ • Configure in settings         │
  │ • Grant permissions             │
  └─────────────────────────────────┘

  Permission Levels:
  🟢 READ-ONLY: Resources only
  🟡 LIMITED: Specific tools only
  🔴 FULL: All capabilities

  Example (Claude Desktop config):
  {
    "mcpServers": {
      "filesystem": {
        "command": "mcp-server-filesystem",
        "args": ["--allowed-dirs", "/home/user/safe-folder"],
        "permissions": ["read", "write"]
      }
    }
  }

  Safety Features:
  ✅ Sandboxed execution
  ✅ Path restrictions
  ✅ Rate limiting
  ✅ Audit logging
  Visual: Permission levels diagram, config example
  Speaker Notes: Emphasize user control & transparency

  ---
  Slide 29: Building an MCP Server - Overview

  🛠️ Creating Your Own MCP Server

  Language Options:
  • Python (official SDK)
  • TypeScript/JavaScript (official SDK)
  • Other languages (community SDKs)

  Basic Structure:
  ┌─────────────────────────────────┐
  │ 1. Setup MCP SDK               │
  │ 2. Define tools/resources       │
  │ 3. Implement handlers           │
  │ 4. Add error handling           │
  │ 5. Test & deploy                │
  └─────────────────────────────────┘

  Simple Server (conceptual):
  from mcp import Server, Tool

  server = Server("my-calculator")

  @server.tool()
  def add(a: int, b: int) -> int:
      """Add two numbers"""
      return a + b

  server.run()

  → That's it! Now any MCP host can use it! 🎉
  Visual: Code structure dengan annotations
  Speaker Notes: Show it's not scary, quite simple actually

  ---
  Slide 30: MCP Adoption & Future

  📈 MCP Adoption Status

  CURRENT HOSTS (Supporting MCP):
  ✅ Claude Desktop (native)
  ✅ Zed Editor
  ✅ Sourcegraph Cody
  ✅ Continue (VS Code extension)

  COMING SOON:
  🔜 VS Code official
  🔜 JetBrains IDEs
  🔜 More AI platforms

  ECOSYSTEM STATS (as of Dec 2024):
  • 150+ MCP servers (GitHub)
  • 50+ official servers
  • Growing 10+ servers/week
  • Active community (Discord, GitHub)

  Why It Matters:
  🌟 First universal standard for AI tools
  🌟 Backed by major AI company (Anthropic)
  🌟 Open source → No vendor lock-in
  🌟 Solves real pain point

  Future Vision:
  → MCP becomes the "HTTP for AI tools"
  → Every service offers MCP server
  → App stores for MCP servers
  Visual: Timeline, adoption chart, ecosystem growth graph
  Speaker Notes: Still early, but momentum is strong

  ---
  BAGIAN 3: HANDS-ON DEMOS & LABS (45 menit)

  Slide 31: Section Divider

  🎬 PART 3
  Hands-On Time!
  Let's Get Our Hands Dirty 💻
  Visual: Code editor, terminal imagery
  Speaker Notes: "Most fun part, mari kita praktek!"

  ---
  Slide 32: Demo Environment Setup

  ⚙️ What We'll Use Today

  Platform: Python + MCP Python SDK
  Environment: Google Colab (no install needed!)

  Demos:
  1. ✅ Setup MCP Server (10 min)
  2. ✅ Use Official MCP Servers (15 min)
  3. ✅ Build Custom MCP Server (20 min)

  Requirements:
  • Google account (for Colab)
  • GitHub account (optional, for demos)
  • Enthusiasm! 🚀

  All code will be shared:
  📁 GitHub repo: [your-repo-url]
  📝 Slides: [slides-url]
  Visual: Checklist, tech stack logos
  Speaker Notes: Lower barrier to entry, everything in browser

  ---
  Slide 33: Demo 1 - Installing MCP (Claude Desktop)

  📦 Demo 1: Setup MCP in Claude Desktop

  Step-by-Step:

  1. Install Claude Desktop
     Download: https://claude.ai/download

  2. Locate config file:
     • Mac: ~/Library/Application Support/Claude/claude_desktop_config.json
     • Windows: %APPDATA%/Claude/claude_desktop_config.json

  3. Install MCP server (example: filesystem)

     npm install -g @modelcontextprotocol/server-filesystem

  4. Edit config:
     {
       "mcpServers": {
         "filesystem": {
           "command": "mcp-server-filesystem",
           "args": ["/path/to/allowed/folder"]
         }
       }
     }

  5. Restart Claude Desktop

  6. Test: "List files in my folder"

  [Live demo or video walkthrough]
  Visual: Screenshots for each step, config file example
  Speaker Notes: Do live if possible, have backup video

  ---
  Slide 34: Demo 2 - MCP Filesystem in Action

  🎥 Demo 2: Real MCP Usage

  Task: "Analyze my Python project"

  Watch Claude with MCP Filesystem:

  User: "Read all .py files in /home/user/project
         and give me a summary of what this project does"

  Claude (with MCP):
  1. 🔍 Lists resources: file:///home/user/project/*.py
  2. 📖 Reads: main.py, utils.py, models.py
  3. 🧠 Analyzes code structure
  4. ✍️ Generates summary:
     "This is a web scraping project using BeautifulSoup..."

  WITHOUT MCP:
  ❌ "I cannot access files on your computer"

  WITH MCP:
  ✅ Full file system access (with permissions)
  ✅ Can read, write, search files
  ✅ Multi-file analysis

  [Live demo showing actual interaction]
  Visual: Split screen - Claude interface + file system
  Speaker Notes: Show real interaction, emphasize the difference

  ---
  Slide 35: Demo 3 - Database MCP Server

  🗄️ Demo 3: Database Integration

  Setup: MCP Postgres Server

  Task: "Show me top 5 customers by sales"

  Configuration:
  {
    "mcpServers": {
      "postgres": {
        "command": "mcp-server-postgres",
        "args": ["postgresql://user:pass@localhost/mydb"]
      }
    }
  }

  Interaction:
  User: "What are my top 5 customers by total sales?"

  Claude (via MCP):
  1. 💭 "I need to query the database"
  2. 🛠️ Uses tool: query_database
  3. 📝 Generates SQL:
     SELECT customer_name, SUM(amount) as total
     FROM sales
     GROUP BY customer_name
     ORDER BY total DESC
     LIMIT 5
  4. 📊 Gets results
  5. 💬 Formats nicely: "Your top 5 customers are..."

  → Natural language → SQL → Results! 🎉

  [Demo with sample database]
  Visual: Live query execution, results table
  Speaker Notes: Use SQLite untuk simplicity, pre-populate sample data

  ---
  Slide 36: Coding Time - Build Simple MCP Server

  💻 Let's Build: Weather MCP Server

  Goal: Create MCP server that provides weather data

  Features:
  • get_current_weather(city)
  • get_forecast(city, days)
  • get_temperature(city)

  Tech Stack:
  • Python + MCP SDK
  • Free Weather API (wttr.in atau OpenWeather free tier)

  Time: 20 minutes
  Difficulty: Beginner-friendly

  Follow along! 👨‍💻👩‍💻

  [Open Google Colab notebook]
  Visual: Target code structure preview
  Speaker Notes: "Let's code together, step by step"

  ---
  Slide 37: Code Walkthrough - Part 1 (Setup)

  # Step 1: Install dependencies (Colab)
  !pip install mcp requests

  # Step 2: Imports
  from mcp.server import Server
  from mcp.server.stdio import stdio_server
  from mcp.types import Tool, TextContent
  import requests
  import json

  # Step 3: Initialize server
  server = Server("weather-server")

  print("✅ Setup complete!")

  Instructions:
  1. Copy code to Colab cell
  2. Run cell
  3. Verify installation

  Visual: Code with syntax highlighting, output preview
  Speaker Notes: Walk through each line, explain imports

  ---
  Slide 38: Code Walkthrough - Part 2 (Define Tools)

  # Step 4: Define tool schema
  WEATHER_TOOL = Tool(
      name="get_weather",
      description="Get current weather for a city",
      inputSchema={
          "type": "object",
          "properties": {
              "city": {
                  "type": "string",
                  "description": "City name (e.g., 'Jakarta', 'Tokyo')"
              },
              "units": {
                  "type": "string",
                  "enum": ["metric", "imperial"],
                  "description": "Temperature units",
                  "default": "metric"
              }
          },
          "required": ["city"]
      }
  )

  # Step 5: Register tool with server
  @server.list_tools()
  async def list_tools():
      return [WEATHER_TOOL]

  print("✅ Tool defined!")

  Key Points:
  • JSON Schema for validation
  • Clear descriptions help LLM
  • Type safety built-in

  Visual: Code + schema diagram
  Speaker Notes: Explain importance of good descriptions

  ---
  Slide 39: Code Walkthrough - Part 3 (Implementation)

  # Step 6: Implement tool handler
  @server.call_tool()
  async def call_tool(name: str, arguments: dict):
      if name == "get_weather":
          city = arguments["city"]
          units = arguments.get("units", "metric")

          try:
              # Call free weather API
              url = f"https://wttr.in/{city}?format=j1"
              response = requests.get(url, timeout=5)
              data = response.json()

              # Extract info
              current = data["current_condition"][0]
              temp = current["temp_C"] if units == "metric" else current["temp_F"]
              condition = current["weatherDesc"][0]["value"]
              humidity = current["humidity"]

              # Format result
              result = f"Weather in {city}:\n"
              result += f"Temperature: {temp}°{'C' if units == 'metric' else 'F'}\n"
              result += f"Condition: {condition}\n"
              result += f"Humidity: {humidity}%"

              return [TextContent(type="text", text=result)]

          except Exception as e:
              return [TextContent(
                  type="text",
                  text=f"Error getting weather: {str(e)}"
              )]

      raise ValueError(f"Unknown tool: {name}")

  print("✅ Implementation complete!")

  Visual: Code with error handling highlighted
  Speaker Notes: Emphasize error handling importance

  ---
  Slide 40: Code Walkthrough - Part 4 (Run Server)

  # Step 7: Run the server
  async def main():
      async with stdio_server() as (read_stream, write_stream):
          await server.run(
              read_stream,
              write_stream,
              server.create_initialization_options()
          )

  # For Colab testing, we'll simulate instead
  # In production: python weather_server.py
  print("✅ Server ready to run!")
  print("\nTo use in Claude Desktop:")
  print("1. Save this as weather_server.py")
  print("2. Add to claude_desktop_config.json:")
  print('''
  {
    "mcpServers": {
      "weather": {
        "command": "python",
        "args": ["/path/to/weather_server.py"]
      }
    }
  }
  ''')

  Testing Alternative (for demo):
  # Quick test in Colab
  test_result = await call_tool("get_weather", {"city": "Jakarta"})
  print(test_result[0].text)

  Visual: Full code + output example
  Speaker Notes: Show testing, then explain deployment

  ---
  Slide 41: Testing Our MCP Server

  🧪 Testing the Weather Server

  Method 1: Direct Testing (Colab)
  # Already shown in previous slide

  Method 2: With MCP Inspector (local)
  npx @modelcontextprotocol/inspector python weather_server.py

  Method 3: In Claude Desktop
  [Configure → Restart → Test]

  Test Queries:
  ✅ "What's the weather in Tokyo?"
  ✅ "Get weather for London in Fahrenheit"
  ✅ "Compare weather between Jakarta and Singapore"

  Expected Behavior:
  1. Claude recognizes available tool
  2. Calls get_weather with correct arguments
  3. Displays formatted results
  4. Can handle multiple cities in one query!

  [Live demo of actual usage]

  Visual: Screenshots of testing methods, actual output
  Speaker Notes: Do live test if possible, show multiple queries

  ---
  Slide 42: Extending Your MCP Server

  🚀 Level Up Your Server

  Easy Additions:
  1. Add more tools:
     • get_forecast(city, days)
     • get_air_quality(city)
     • get_uv_index(city)

  2. Add resources:
     weather://historical/{city}
     → Access historical weather data

  3. Add prompts:
     "Weather Report Template"
     → Formatted weather summaries

  4. Add caching:
     → Don't call API for every request
     → Cache for 30 minutes

  5. Add multiple APIs:
     → Fallback if one fails
     → Combine data sources

  Example Extension:
  @server.list_resources()
  async def list_resources():
      return [
          Resource(
              uri="weather://favorites",
              name="Favorite Cities Weather",
              mimeType="application/json"
          )
      ]

  Visual: Code snippets for extensions, architecture diagram
  Speaker Notes: Show how easy it is to extend, encourage creativity

  ---
  Slide 43: Community MCP Servers Showcase

  🌟 Cool Community Servers to Try

  1. 🎵 Spotify MCP Server
     Control Spotify, get recommendations

  2. 📝 Obsidian MCP Server
     Access your knowledge base

  3. 🐦 Twitter/X MCP Server
     Read timeline, post tweets

  4. 🏠 Home Assistant MCP Server
     Control smart home devices

  5. 📊 Google Sheets MCP Server
     Read/write spreadsheets

  6. 🎮 Discord MCP Server
     Bot management, read messages

  7. 📸 Unsplash MCP Server
     Search and download images

  8. 🗺️ Maps MCP Server
     Geocoding, directions

  Installation:
  npm install -g @username/mcp-server-name

  Browse more: https://github.com/modelcontextprotocol/servers

  Visual: Grid with server icons/screenshots
  Speaker Notes: Quick showcase, encourage exploration

  ---
  Slide 44: Hands-On Exercise

  🎯 Your Turn: Mini Challenge

  EXERCISE: Extend the Weather Server

  Choose one (15 minutes):

  BEGINNER:
  Add a "get_forecast" tool that shows 3-day forecast

  INTERMEDIATE:
  Add resource that lists all available cities
  URI: weather://cities/supported

  ADVANCED:
  Create multi-city comparison tool:
  compare_weather(city1, city2, city3)
  Returns side-by-side comparison

  Bonus Challenge:
  Add prompt template for "Daily Weather Briefing"

  [Work time: 15 minutes]
  [Share solutions: 5 minutes]

  Helper code snippets in the notebook! 💡

  Visual: Challenge cards, countdown timer
  Speaker Notes: Walk around (if in-person), answer questions, show solutions after

  ---
  Slide 45: Solutions & Best Practices

  ✨ Exercise Solutions

  SOLUTION 1: Forecast Tool
  @server.call_tool()
  async def call_tool(name, arguments):
      if name == "get_forecast":
          city = arguments["city"]
          days = arguments.get("days", 3)

          # Use API forecast endpoint
          url = f"https://wttr.in/{city}?format=%C+%t\n"
          # [Implementation...]

  BEST PRACTICES:

  1. ✅ Descriptive tool names
     ❌ "tool1", "func"
     ✅ "get_weather_forecast", "search_city"

  2. ✅ Clear descriptions
     Help LLM understand when to use tool

  3. ✅ Robust error handling
     Network issues, invalid input, etc.

  4. ✅ Input validation
     Use JSON Schema properly

  5. ✅ Efficient implementations
     Cache, rate limiting, timeouts

  6. ✅ Good logging
     Debug issues easily

  7. ✅ Security first
     Sanitize inputs, limit access

  Visual: Code solutions side-by-side, best practices checklist
  Speaker Notes: Review solutions quickly, emphasize best practices

  ---
  BAGIAN 4: FUTURE & WRAP-UP (10 menit)

  Slide 46: Section Divider

  🔮 PART 4
  The Future & Your Role
  Visual: Futuristic imagery
  Speaker Notes: Wrap-up, inspire action

  ---
  Slide 47: The Future of Agentic AI

  🚀 What's Coming Next?

  SHORT TERM (2024-2025):
  • More MCP adoption across tools
  • Better multi-modal agents (text + image + audio)
  • Improved reasoning capabilities
  • Lower costs, faster inference

  MEDIUM TERM (2025-2027):
  • AI agents as coworkers (not just tools)
  • Persistent, learning agents
  • Multi-agent collaboration at scale
  • Industry-specific agents

  LONG TERM (2027+):
  • Autonomous AI systems
  • Self-improving agents
  • Human-AI hybrid workflows
  • New interaction paradigms

  Key Trend: From "AI that helps" → "AI that does"

  Visual: Timeline with milestones, concept art
  Speaker Notes: Balance optimism with realism

  ---
  Slide 48: Career Opportunities

  💼 Jobs & Skills in Agentic AI Space

  EMERGING ROLES:

  1. 🛠️ AI Agent Developer
     Build & deploy agent systems
     Skills: Python, LLMs, MCP, APIs

  2. 🔌 Integration Engineer
     Create MCP servers & connections
     Skills: APIs, protocols, system design

  3. 📝 Prompt Engineer
     Craft effective agent instructions
     Skills: LLMs, reasoning patterns, testing

  4. 🎨 Agent UX Designer
     Design human-agent interactions
     Skills: UX, AI capabilities, psychology

  5. 🔒 AI Safety Engineer
     Ensure safe agent behavior
     Skills: Security, ethics, testing

  6. 📊 Agent Performance Analyst
     Optimize agent efficiency & costs
     Skills: Metrics, optimization, ML

  Average Salary (US): $120k - $200k+
  Demand: Growing rapidly 📈

  Visual: Job cards dengan salary ranges, demand chart
  Speaker Notes: Motivate mahasiswa, show concrete opportunities

  ---
  Slide 49: Learning Path - Next Steps

  🎓 Your Learning Journey

  IMMEDIATE (This Week):
  ✅ Setup Claude Desktop + MCP server
  ✅ Try filesystem & github servers
  ✅ Build simple custom server
  ✅ Join MCP community (Discord)

  SHORT TERM (This Month):
  📚 Deep dive: LangChain docs
  📚 Read: MCP specification
  💻 Project: Build useful MCP server for yourself
  🤝 Contribute: Open source MCP servers

  MEDIUM TERM (3-6 Months):
  🏗️ Build: Complete agent application
  📝 Write: Blog about your learnings
  👥 Network: AI/agent communities
  💼 Portfolio: Showcase projects

  RESOURCES:
  • MCP Docs: modelcontextprotocol.io
  • LangChain: python.langchain.com
  • Anthropic: anthropic.com/guides
  • Community: GitHub, Discord, Reddit

  The best time to start: NOW! 🚀

  Visual: Learning roadmap, resource links with QR codes
  Speaker Notes: Give concrete action items, make it achievable

  ---
  Slide 50: Key Takeaways - Summary

  🎯 Key Takeaways from Today

  1. AGENTIC AI = LLM + Tools + Autonomy
     → Can perceive, reason, act, learn

  2. CORE COMPONENTS:
     • Reasoning engine (LLM)
     • Memory systems
     • Tool interfaces
     • Planning modules

  3. MCP = Universal Standard for AI Tools
     → "USB for AI Agents"
     → Solve integration fragmentation

  4. MCP PRIMITIVES:
     • Tools (actions)
     • Resources (data)
     • Prompts (templates)

  5. YOU CAN BUILD THIS!
     → Open source, well-documented
     → Growing community
     → Real career opportunities

  Remember: We're at the beginning of agent era
  → Early movers have huge advantage! 💡

  Visual: Summary cards, key concepts highlighted
  Speaker Notes: Recap main points, energize audience

  ---
  Slide 51: Community & Resources

  🤝 Join the Community

  OFFICIAL CHANNELS:
  🐙 GitHub: github.com/modelcontextprotocol
  💬 Discord: discord.gg/modelcontextprotocol
  📧 Newsletter: modelcontextprotocol.io/newsletter

  LEARNING RESOURCES:
  📚 Documentation: modelcontextprotocol.io/docs
  🎥 YouTube: [channels]
  📝 Blog Posts: anthropic.com/blog
  🧑‍💻 Examples: github.com/modelcontextprotocol/examples

  INDONESIAN COMMUNITY:
  🇮🇩 [Your local Discord/Telegram]
  🇮🇩 [Indonesian AI meetup groups]

  COURSE MATERIALS:
  📦 GitHub: [your-repo]
     • All slides
     • Code examples
     • Exercise solutions
     • Additional resources

  Stay connected! Let's build together! 🚀

  Visual: QR codes for all links, community logos
  Speaker Notes: Encourage participation, give ways to stay in touch

  ---
  Slide 52: Q&A

  ❓ Questions & Discussion

  Open Floor!

  Topics to discuss:
  • Technical questions
  • Project ideas
  • Career advice
  • Troubleshooting
  • Anything AI agents!

  [Interactive Q&A time]

  💡 No question is too basic!
  💡 Share your ideas!
  💡 Let's learn together!

  Visual: Q&A graphic, encouraging imagery
  Speaker Notes: Encourage participation, be welcoming

  ---
  Slide 53: Final Challenge & Homework

  🎯 Final Challenge (Optional)

  BUILD SOMETHING COOL!

  Project Ideas:
  1. 📚 Personal Knowledge Agent
     MCP + Obsidian/Notion → Research assistant

  2. 💻 Dev Workflow Agent
     MCP + GitHub + Terminal → Automation

  3. 📊 Data Analysis Agent
     MCP + Database + Visualization → Reports

  4. 🏠 Home Automation Agent
     MCP + IoT → Smart home control

  5. 🎓 Study Buddy Agent
     MCP + Files + Web → Learning assistant

  BONUS:
  Share on GitHub & get feedback!
  Best project: Featured in next session!

  Deadline: [2 weeks from now]

  Visual: Project cards, GitHub star icon
  Speaker Notes: Inspire action, make it fun

  ---
  Slide 54: Thank You!

  🎉 Thank You!

  You're now equipped to:
  ✅ Understand agentic AI architectures
  ✅ Use MCP in your projects
  ✅ Build custom MCP servers
  ✅ Join the AI agent revolution

  Keep Learning, Keep Building! 🚀

  Contact:
  📧 [your-email]
  🐙 GitHub: [your-github]
  💼 LinkedIn: [your-linkedin]
  💬 [Discord/Telegram]

  Special Thanks:
  • Anthropic for MCP
  • Open source community
  • YOU for participating! 👏

  Let's stay in touch!
  See you in the agent future! 🤖✨

  Visual: Thank you graphic, all contact info
  Speaker Notes: Warm closing, express gratitude

  ---
  BONUS/BACKUP SLIDES

  Slide 55: Backup - Troubleshooting Common Issues

  🔧 Common Issues & Solutions

  ISSUE 1: MCP Server Not Connecting
  ✅ Check config file path
  ✅ Verify JSON syntax (use validator)
  ✅ Check server installation (npm list -g)
  ✅ Look at logs (~/Library/Logs/Claude/)

  ISSUE 2: Tool Not Being Called
  ✅ Improve tool description
  ✅ Check inputSchema
  ✅ Test with explicit request
  ✅ Verify server is running

  ISSUE 3: Permission Errors
  ✅ Check file/folder permissions
  ✅ Review allowed-dirs config
  ✅ Run with appropriate privileges

  ISSUE 4: Slow Response
  ✅ Implement caching
  ✅ Add timeouts
  ✅ Use async/await properly
  ✅ Optimize API calls

  Debug Tips:
  • Enable verbose logging
  • Use MCP Inspector tool
  • Test tools individually
  • Check network connectivity

  Visual: Problem-solution flowchart
  Speaker Notes: Only if questions arise

  ---
  Slide 56: Backup - Advanced MCP Patterns

  🎨 Advanced MCP Patterns

  1. CHAINING TOOLS
     Tool A result → Input for Tool B
     Example: search_web → summarize_results → save_to_file

  2. CONDITIONAL EXECUTION
     If-then logic in tool implementation
     Example: If file exists, read; else create

  3. STREAMING RESPONSES
     Long operations with progress updates
     Use SSE (Server-Sent Events)

  4. BATCH OPERATIONS
     Process multiple items efficiently
     Example: analyze_all_files tool

  5. STATEFUL SERVERS
     Remember previous interactions
     Use session management

  6. MULTI-MODAL TOOLS
     Text + Images + Audio
     Example: transcribe_audio → analyze_sentiment

  7. WEBHOOKS INTEGRATION
     Real-time event handling
     Example: GitHub webhook → process PR

  Visual: Pattern diagrams with code snippets
  Speaker Notes: Advanced users only

  ---
  Slide 57: Backup - MCP vs Other Protocols

  ⚖️ MCP vs Alternatives

  MCP vs Function Calling (OpenAI):
  • MCP: Protocol, reusable across apps
  • Function Calling: API-specific, not portable

  MCP vs LangChain Tools:
  • MCP: Standardized, interoperable
  • LangChain: Framework-specific

  MCP vs APIs:
  • MCP: AI-native, semantic
  • APIs: Human-designed, RESTful

  MCP vs Zapier/IFTTT:
  • MCP: AI-controlled, dynamic
  • Zapier: Pre-configured, static

  UNIQUE MCP ADVANTAGES:
  ✅ Universal standard
  ✅ AI-first design
  ✅ Security model built-in
  ✅ Community ecosystem
  ✅ Works offline (stdio transport)

  WHEN TO USE WHAT:
  → MCP: Agent applications
  → APIs: Traditional apps
  → Zapier: No-code automation
  → All together: Best results!

  Visual: Comparison table with checkmarks
  Speaker Notes: Only if comparison questions come up

  ---
  Slide 58: Backup - Cost Analysis

  💰 Economics of Agentic AI

  COST FACTORS:
  1. LLM API Calls
     • GPT-4: ~$0.03-0.06 per 1K tokens
     • Claude: ~$0.015-0.075 per 1K tokens
     • Open source: Self-hosted costs

  2. Tool API Calls
     • Some free (filesystem)
     • Some paid (external APIs)

  3. Infrastructure
     • MCP servers: Minimal (local)
     • Hosting: If needed

  EXAMPLE: Research Agent Task
  Task: "Research AI trends and write report"

  Without Agent:
  • Human: 2 hours @ $50/hr = $100

  With Agent:
  • 50 LLM calls @ $0.01 = $0.50
  • 20 web searches: Free
  • 5 minutes human review: $4
  • Total: ~$5

  ROI: 20x cost savings! 📈

  Cost Optimization:
  ✅ Use caching
  ✅ Smaller models for simple tasks
  ✅ Batch operations
  ✅ Set budget limits

  Visual: Cost breakdown chart, ROI comparison
  Speaker Notes: If economics questions come up

  ---
  Slide 59: Backup - Ethics & Responsible AI

  ⚖️ Ethical Considerations

  AGENT ACCOUNTABILITY:
  ❓ Who is responsible for agent actions?
  ✅ Clear logging & audit trails
  ✅ Human oversight for critical tasks
  ✅ Rollback capabilities

  BIAS & FAIRNESS:
  ❓ Agent decisions might reflect LLM biases
  ✅ Diverse training data
  ✅ Regular audits
  ✅ Fairness metrics

  PRIVACY:
  ❓ Agents access sensitive data
  ✅ Data minimization
  ✅ Encryption
  ✅ Clear privacy policies

  AUTONOMY LIMITS:
  ❓ How much autonomy is safe?
  ✅ Graduated autonomy levels
  ✅ Confirmation for high-stakes actions
  ✅ Emergency stop mechanisms

  JOB DISPLACEMENT:
  ❓ Will agents replace jobs?
  💭 History: Tools augment, not replace
  💭 New roles emerge
  💭 Focus on human-AI collaboration

  PRINCIPLES:
  1. Transparency
  2. Accountability
  3. User control
  4. Privacy first
  5. Continuous monitoring

  Visual: Ethics framework diagram
  Speaker Notes: Important topic if raised

  ---
  Slide 60: Backup - Research Papers & Deep Dives

  📚 Academic Foundation

  KEY PAPERS:

  ReAct (2022):
  "Synergizing Reasoning and Acting in Language Models"
  → Foundation for modern agents

  AutoGPT (2023):
  Autonomous agents that pursue goals
  → Viral proof-of-concept

  Toolformer (2023):
  "Teaching Language Models to Use Tools"
  → Self-supervised tool learning

  Gorilla (2023):
  "Large Language Model Connected with Massive APIs"
  → API call generation

  AgentBench (2023):
  → Benchmark for evaluating agents

  BOOKS:
  • "Building LLM Apps" - O'Reilly
  • "AI Agents" - Manning (upcoming)

  COURSES:
  • CS 324 - Stanford (Large Language Models)
  • DeepLearning.AI - LangChain courses

  Research Groups:
  • Stanford HAI
  • OpenAI
  • Anthropic Research
  • Google DeepMind

  Visual: Paper titles with links, book covers
  Speaker Notes: For academically curious students

  ---
  REKOMENDASI DELIVERY - PERTEMUAN 2:

  Timing Breakdown:

  - Slides 1-4 (Opening): 10 min
  - Slides 5-15 (Deep Dive Agents): 25 min
  - Slides 16-30 (MCP Deep Dive): 30 min
  - Break: 10 min ☕
  - Slides 31-45 (Hands-On): 45 min
  - Slides 46-54 (Wrap-up): 10 min
  - Buffer: 10-20 min untuk Q&A extra

  Critical Demos to Prepare:

  1. Claude Desktop + MCP Filesystem (MUST HAVE)
    - Pre-configure before session
    - Have backup video
    - Test multiple queries
  2. Weather MCP Server Build (MAIN LAB)
    - Complete Colab notebook
    - Test all code cells
    - Have solutions ready
    - Backup: Pre-built server to download
  3. Community Servers Showcase (NICE TO HAVE)
    - 2-3 pre-installed servers
    - Show variety of use cases
    - Quick demos (2-3 min each)

  Materials to Prepare:

  pertemuan-2-materials/
  ├── slides/
  │   └── pertemuan-2-agentic-ai-mcp.pdf
  ├── code/
  │   ├── weather_server.py (complete)
  │   ├── weather_server_starter.py (template)
  │   └── test_mcp_server.py
  ├── notebooks/
  │   ├── 01-mcp-basics.ipynb
  │   ├── 02-build-weather-server.ipynb
  │   └── 03-advanced-patterns.ipynb
  ├── configs/
  │   ├── claude_desktop_config.json (example)
  │   └── mcp_servers_list.md
  ├── exercises/
  │   ├── exercise-1-extend-weather.md
  │   └── exercise-2-custom-server.md
  └── README.md (setup instructions)

  Pre-Session Checklist:

  1 Week Before:
  - Create GitHub repo dengan all materials
  - Test all demos end-to-end
  - Record backup videos
  - Setup Discord/Telegram community
  - Send pre-reading materials

  1 Day Before:
  - Test Claude Desktop + MCP setup
  - Verify all Colab notebooks run
  - Prepare sample data files
  - Check API keys/rate limits
  - Print handouts (optional)

  Day Of:
  - Arrive early untuk setup
  - Test screen sharing/projector
  - Open all tabs/apps needed
  - Have backup laptop ready
  - Water & energy! ☕

  Engagement Strategies:

  1. Interactive Polls (every 15 min):
    - "Raise hand if you've used [X]"
    - "What use case excites you most?"
    - Quick feedback checks
  2. Pair Programming (during lab):
    - Team up students
    - Peer teaching
    - Share solutions
  3. Live Coding:
    - Type slowly
    - Explain every line
    - Make intentional mistakes & fix
    - Ask "What should we do next?"
  4. Show Failures:
    - Demo agent getting stuck
    - Show how to debug
    - Teach troubleshooting

  Backup Plans:

  Plan B (Network Issues):
  - Use offline recordings for demos
  - Distribute USB drives with materials
  - Focus on code walkthrough vs live execution

  Plan C (Time Running Short):
  - Skip slides 10-11 (planning strategies detail)
  - Skip community showcase (slide 43)
  - Do exercise as homework
  - Share recording for later

  Plan D (Too Fast):
  - Do advanced exercise
  - Live build another server
  - Q&A discussion
  - Code review session

  Post-Session:

  Immediately After:
  - Share GitHub repo link
  - Post slides & recordings
  - Create feedback form
  - Answer lingering questions

  Within 1 Week:
  - Compile Q&A into FAQ
  - Feature student projects
  - Send additional resources
  - Schedule office hours (optional)

  Ongoing:
  - Keep Discord/Telegram active
  - Share news about MCP updates
  - Curate community resources
  - Plan follow-up sessions

  Apakah Anda ingin saya buatkan:
  1. Complete Colab notebook untuk weather server lab?
  2. Claude Desktop setup tutorial step-by-step dengan screenshots?
  3. Video script untuk demo recordings?
  4. Exercise solutions lengkap dengan explanations?
  5. GitHub repo structure siap pakai dengan template README?