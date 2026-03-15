# AI Personal Assistant — Multi-Agent System (v1 & v2)

A personal AI assistant built with n8n that manages daily tasks through specialized sub-agents, accessible via WhatsApp (v1) and Telegram (v2 with MCP).

---

## Overview

Two iterations of the same core idea: a central orchestrator agent that receives requests, decides which specialized agent should handle them, and returns a response — all through a messaging app.

---

## System Architecture

![Architecture](./architecture.png)

---

## Version 1 — WhatsApp Multi-Agent

![V1 Overview](./screenshots/v1_overview.png)

### How It Works

```
User sends message on WhatsApp
(text, voice, or image)
              ↓
       Input Processing
       /      |       \
      ↓       ↓        ↓
    Text    Voice     Image
             ↓         ↓
         Transcribe  Analyze
              ↓
      Orchestrator Agent
      (Ollama — decides routing)
      /      |      |      \
     ↓       ↓      ↓       ↓
  Search   Email  Calendar  Social
  Agent    Agent   Agent    Agent
              ↓
      Response to user
      (text or audio)
```

### Input Types

The system handles three input types:
- **Text** — standard chat messages
- **Voice** — transcribed automatically before processing
- **Image** — analyzed for content before processing

### Sub-Agents

**Search Agent**
Searches Wikipedia and Hacker News for accurate, current information.

**Email Agent**
Reads, summarizes, sends, and deletes emails via Gmail API.

**Calendar Agent**
Creates, updates, and deletes events on Google Calendar.

**Social Agent**
Drafts and posts content to X (Twitter).

### Output

Responds via WhatsApp as text or as a voice message (Text-to-Speech) depending on context.

---

## Version 2 — Telegram + MCP

![V2 Overview](./screenshots/v2_overview.png)

### What Changed

v2 replaces direct API integrations with Model Context Protocol (MCP). Instead of each agent connecting to tools individually, all agents communicate through a unified MCP layer.

```
v1: Agent → direct API call → Tool
v2: Agent → MCP Client → MCP Server → Tool
```

This makes adding new tools faster and keeps the system more organized as it scales.

### Same agents, better architecture:

- Search Agent (MCP)
- Email Agent (MCP)
- Calendar Agent (MCP)
- Social Agent (MCP)

### Input

Telegram handles the same three input types: text, voice (transcribed), and image (analyzed).

### Output

Responds as text or as an audio file sent directly in Telegram.

---

## Tech Stack

| Category | Tools |
|----------|-------|
| Automation | n8n (Self-Hosted) |
| AI Models | Ollama, Gemini, GPT-OSS |
| Protocol | MCP (Model Context Protocol) |
| Messaging | WhatsApp API (v1), Telegram API (v2) |
| Integrations | Gmail API, Google Calendar API, X API, Wikipedia |
| Infrastructure | Docker, VPS, SSL |

---

## Repository Structure

```
ai-personal-assistant/
├── screenshots/
│   ├── v1_overview.png
│   ├── v1_input_processing.png
│   ├── v1_search_agent.png
│   ├── v1_email_agent.png
│   ├── v1_calendar_agent.png
│   ├── v2_overview.png
│   └── v2_mcp_architecture.png
├── architecture.png
└── README.md
```

---

## Note

Workflow logic, AI prompts, and credentials are kept private. This repository covers architecture and design decisions only.

---

## Contact

- fares.amr@gmail.com
- linkedin.com/in/fares-amr
- github.com/fares-amr
