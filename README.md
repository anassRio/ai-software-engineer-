# AI-Native Software Engineer Learning Path

**Status**: Personal learning journey in progress  
**Objective**: Transform from experienced Software Engineer to AI-Native / Agentic Software Engineer  
**Repository**: Active lab for building AI-augmented systems

---

## 🎯 Vision: What Does "AI-Native" Mean?

You're not trying to become a **Data Scientist** or **ML Researcher**.

You're learning to design, build, and industrialize **production software systems** where LLMs and AI agents are core components, not afterthoughts.

### The Spectrum

```
AI User
  ↓
  Uses ChatGPT, Claude for specific tasks
  
AI-Assisted Developer
  ↓
  Uses Copilot, code completion in IDE
  Writes some prompts, uses LLM APIs
  
AI-Native Software Engineer ← YOU ARE HERE
  ↓
  Designs systems where agents are first-class components
  Builds custom agents, skills, tools
  Orchestrates multi-agent workflows
  Knows how to give autonomy to agents
  Understands when to keep humans in the loop
  Creates evaluation frameworks for agent quality
  
AI Systems Architect / Agentic Engineer
  ↓
  Builds production-grade agentic platforms
  Designs agent orchestration at scale
  Handles observability, monitoring, safety
```

---

## 🏗️ What You'll Learn to Build

By the end of this path, you'll be able to:

✅ Give **responsibilities** to agents (not just "run this prompt")  
✅ Create **tools** that agents reliably use  
✅ Design **skills** (specialized agent capabilities)  
✅ Build **specialized agents** for specific domains  
✅ **Orchestrate** multiple agents working together  
✅ **Connect systems** via MCP (Model Context Protocol)  
✅ **Evaluate agents** rigorously before production  
✅ Create **reliable workflows** with proper error handling  
✅ Keep **humans in the loop** when necessary  
✅ **Industrialize** software development with AI assistance  

---

## 📚 The 10-Module Learning Path

Each module builds on the previous. **Don't skip ahead.**

| # | Module | Focus | You'll Build | Key Skill |
|---|--------|-------|--------------|----------|
| **00** | **AI Fundamentals** | Core ML/AI concepts (for SWE perspective) | Simple neural network | Understand how learning works |
| **01** | **LLM Fundamentals** | How transformers work, tokens, inference | LLM-based application | Understand LLM capabilities & limits |
| **02** | **Context Engineering** | Structure context for optimal agent behavior | Dynamic context system | Craft reliable prompts for agents |
| **03** | **Tools / Function Calling** | Give LLMs access to external capabilities | Multi-tool agent system | Design tools agents use reliably |
| **04** | **Agents** | Build autonomous decision-making systems | Minimal agent runtime | Understand agent loop architecture |
| **05** | **Skills** | Specialized, reusable agent capabilities | Domain-specific skills library | Encapsulate expertise in skills |
| **06** | **Multi-Agent** | Coordinate multiple agents | Software dev team agents | Scale from 1 agent → N agents |
| **07** | **MCP** | Standard protocol for agent integration | MCP server for tools | Connect systems at scale |
| **08** | **Evals** | Measure & improve agent quality | Evaluation framework | Ensure agents work reliably |
| **09** | **AI Software Factory** | Capstone: Full automated development pipeline | End-to-end system | Synthesize everything |

---

## 🧠 The Mental Model

### From Traditional Software

```
User Request
  ↓
Code (deterministic, logic-based)
  ↓
Output
```

### To Agentic Software

```
User Request / Story
  ↓
LLM + Instructions + Context + Tools + State
  ↓
Agent Loop (Think → Act → Observe → Repeat)
  ↓
Output (+ human validation)
```

**Key difference**: Code is replaced by agents making decisions. You need to:
- Craft instructions (prompts)
- Design tools agents use
- Build skills for specialized knowledge
- Create evaluation loops
- Handle failure gracefully

---

## 📖 Learning Progression Logic

Why this specific order?

```
00: AI Fundamentals
  └─ Why do neural networks work?
     ↓
01: LLM Fundamentals  
  └─ How do language models specifically work?
     ↓
02: Context Engineering
  └─ How do I structure inputs for good outputs?
     ↓
03: Tools / Function Calling
  └─ How do I give agents external capabilities?
     ↓
04: Agents
  └─ How do agents make decisions using LLMs + tools?
     ↓
05: Skills
  └─ How do I package expertise for reuse?
     ↓
06: Multi-Agent
  └─ How do I make multiple agents work together?
     ↓
07: MCP
  └─ How do I scale agent integration?
     ↓
08: Evals
  └─ How do I know if agents actually work?
     ↓
09: AI Software Factory
  └─ How do I build real systems with all of this?
```

---

## 🎓 Philosophy: 70% Practice / 30% Theory

**Not**: Read papers → Watch lectures → Maybe build something

**Instead**: Read concept → Build immediately → Break it → Measure → Explain to someone else

Each module follows:

```
Concept Explanation
  ↓
Worked Example
  ↓
Lab Exercise (hands-on)
  ↓
Mini Project
  ↓
Validation Checkpoint
  ↓
Next module
```

---

## 🏆 The Capstone: AI Software Factory

Your final project transforms a software requirement into a pull request using multiple specialized agents.

### Progressive Versions

**Factory v0** (Simple)
```
Requirement → Planner → Developer → Human Review → PR
```

**Factory v1** (Quality)
```
Requirement → Planner → Developer → Tester → Human Review → PR
```

**Factory v2** (Architecture)
```
Requirement → Planner → Architect → Developer → Tester → Reviewer → Human Review → PR
```

**Factory v3** (Complete)
```
Requirement → SDD / Spec → Planner → Architect → Developer → Tester → Reviewer → Security → Evals → Human Review → PR
```

**Factory v4** (Production)
```
Requirement → Spec → Plan → Architect → Dev → Test → Review → Security → Evals
           ↓ (with Skills, MCP, Memory, Observability, Parallel Agents)
           → Human Approval → PR → GitHub Integration
```

This demonstrates:
- Multi-agent orchestration
- Specialized skills and tools
- Prompt engineering at scale
- Agent evaluation and quality gates
- Production-ready architecture patterns

---

## 🛠️ Tech Stack

### Core
- **Language**: Python (for AI labs), Java/Spring Boot (for real systems)
- **LLM APIs**: OpenAI, Anthropic Claude
- **Frameworks**: OpenAI Agents SDK, Hugging Face libraries
- **Agent Testing**: Custom evaluation framework

### Software Engineering
- Git & GitHub (version control, PRs)
- Docker & Kubernetes (containerization, orchestration)
- Kafka (event streaming)
- CI/CD pipelines
- Testing frameworks (pytest, JUnit)

### Why This Stack?
- **Bridges** your existing SE knowledge to AI engineering
- **Practical** - tools you'll use in production
- **Clear progression** from lab to real systems

---

## 📋 Progress Tracker

Check off each module as you complete theory, labs, projects, and validation:

- [ ] **00** — AI Fundamentals
  - [ ] Theory
  - [ ] Labs (2-3 practice exercises)
  - [ ] Validation checkpoint

- [ ] **01** — LLM Fundamentals
  - [ ] Theory
  - [ ] Labs (5 progressive exercises)
  - [ ] Validation checkpoint

- [ ] **02** — Context Engineering
  - [ ] Theory
  - [ ] Labs (prompt/context comparison)
  - [ ] Mini project (dynamic context system)
  - [ ] Validation checkpoint

- [ ] **03** — Tools / Function Calling
  - [ ] Theory
  - [ ] Labs (build 3+ tools)
  - [ ] Mini project (multi-tool agent)
  - [ ] Validation checkpoint

- [ ] **04** — Agents
  - [ ] Theory
  - [ ] Labs (build minimal runtime)
  - [ ] Mini project (single-domain agent)
  - [ ] Validation checkpoint

- [ ] **05** — Skills
  - [ ] Theory
  - [ ] Labs (design & test skills)
  - [ ] Mini project (skill library for your domain)
  - [ ] Validation checkpoint

- [ ] **06** — Multi-Agent
  - [ ] Theory
  - [ ] Labs (routing, parallel execution)
  - [ ] Mini project (dev team simulation)
  - [ ] Validation checkpoint

- [ ] **07** — MCP
  - [ ] Theory
  - [ ] Labs (MCP server implementation)
  - [ ] Mini project (software eng MCP server)
  - [ ] Validation checkpoint

- [ ] **08** — Evals
  - [ ] Theory
  - [ ] Labs (eval framework)
  - [ ] Mini project (comprehensive evals)
  - [ ] Validation checkpoint

- [ ] **09** — AI Software Factory
  - [ ] Factory v0 (Planner + Developer)
  - [ ] Factory v1 (+ Tester)
  - [ ] Factory v2 (+ Architect + Reviewer)
  - [ ] Factory v3 (+ Security + Evals)
  - [ ] Factory v4 (Production-ready)
  - [ ] Portfolio demo & documentation

---

## 🚀 How to Use This Repository

1. **Start with Module 00** - Don't skip foundations, even if concepts seem familiar
2. **Read the module README** - Understand objectives and concepts
3. **Follow the labs** - Complete hands-on exercises in order
4. **Build the mini project** - Apply what you learned
5. **Validate your understanding** - Can you explain it without looking?
6. **Take notes** - Fill the "Notes" section in each module
7. **Move to the next module** - Only when checkpoint is complete

---

## 📁 Repository Structure

```
ai-software-engineer-/
├── README.md (this file - your learning map)
│
├── 00-fundamentals/
│   ├── README.md (module guide)
│   ├── labs/
│   │   ├── lab-01-simple-network.md
│   │   ├── lab-02-training-vs-inference.md
│   │   └── ...
│   ├── project/
│   └── validation/
│
├── 01-llm/
│   ├── README.md
│   ├── labs/
│   ├── project/
│   └── validation/
│
├── ... (modules 02-09, similar structure)
│
└── 09-ai-software-factory/
    ├── README.md
    ├── factory-v0/
    ├── factory-v1/
    ├── factory-v2/
    ├── factory-v3/
    └── factory-v4/
```

Structure will grow as you add labs, code, and projects.

---

## 🎯 Success Criteria

You've completed this journey when you can:

✅ **Explain** each core concept without documentation  
✅ **Build** agents for real problems  
✅ **Design** tools and skills for specific domains  
✅ **Orchestrate** multiple agents working together  
✅ **Evaluate** whether your agents actually work  
✅ **Identify** when agents are the right tool vs. when they're not  
✅ **Discuss** tradeoffs: latency, cost, complexity, reliability  
✅ **Show** portfolio-quality projects demonstrating competence  

---

## 🔗 Quick Navigation

- [00 — AI Fundamentals](./00-fundamentals/README.md)
- [01 — LLM Fundamentals](./01-llm/README.md)
- [02 — Context Engineering](./02-context-engineering/README.md)
- [03 — Tools / Function Calling](./03-tools/README.md)
- [04 — Agents](./04-agents/README.md)
- [05 — Skills](./05-skills/README.md)
- [06 — Multi-Agent / Subagents](./06-multi-agent/README.md)
- [07 — MCP](./07-mcp/README.md)
- [08 — Evals & Testing](./08-evals/README.md)
- [09 — AI Software Factory](./09-ai-software-factory/README.md)

---

## 📝 Notes

*Use this section to track overall progress, decisions, and learnings across modules.*

---

**Last Updated**: 2026-09-04  
**Current Focus**: Getting started with Module 00
