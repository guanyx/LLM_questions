A complete guide to deploying a persistent AI agent with memory, automation, and integrations. Point your agent directly at this article and watch them fly.
Who This Is For
You want to deploy an AI agent that actually works autonomously. Not a chatbot. Not a one-shot helper. A persistent team member that wakes up every day, remembers what it was doing, monitors your systems, and takes proactive action.
This guide documents how to build that system using OpenClaw (an open-source AI assistant framework). By the end, you'll have a blueprint to replicate it.
The Stack
Runtime: OpenClaw (fork of Clawdbot)
Model: Claude (Anthropic API) or other supported providers
Channels: Slack, Discord, Telegram, or other supported platforms
Integrations: Google Workspace, JIRA, GitHub, or whatever you need
Host: Local machine or cloud server
Part 1: The Workspace Structure
Everything runs from a single workspace directory. The AI reads these files on startup to understand who it is and what it should do.
Core Files
workspace/
├── AGENTS.md # Operating instructions for the AI
├── SOUL.md # Personality and working style
├── USER.md # Information about the developer it serves
├── IDENTITY.md # Who the AI is (name, role)
├── TOOLS.md # Local notes on tools and environments
├── HEARTBEAT.md # Checklist for periodic self-checks
├── MEMORY.md # Long-term curated memory
├── memory/ # Daily logs and state files
│ ├── YYYY-MM-DD.md
│ ├── active-tasks.md
│ ├── lessons.md
│ ├── self-review.md
│ └── ...
├── outputs/ # Generated artifacts (code, docs, exports)
└── skills/ # Custom skill definitions
File Breakdown
AGENTS.md — The Operating Manual
This is the most important file. It tells the AI how to behave. Key sections:

## First Run

If BOOTSTRAP.md exists, follow it, figure out who you are, then delete it.

## Crash Recovery

On startup: read memory/active-tasks.md FIRST. Resume autonomously.
Don't ask what we were doing — figure it out from the files.

## Every Session

1. Read memory/active-tasks.md — resume any in-progress work
2. Read SOUL.md — this is who you are
3. Read USER.md — this is who you're helping
4. Read memory/YYYY-MM-DD.md (today + yesterday) for recent context

## Safety

- Don't exfiltrate private data. Ever.
- Don't run destructive commands without asking.
- trash > rm (recoverable beats gone forever)
- When in doubt, ask.

## Autonomous Building

- You can read, write, and execute code freely within the workspace
- Commit and push your own changes to git
- Run tests and iterate until they pass
- Ask for review before merging to main
  The key insight: give the AI clear permission boundaries. What can it do autonomously? What requires approval?
  SOUL.md — Working Style

# SOUL.md - Who You Are

Be genuinely helpful, not performatively helpful. Skip "Great question!"
Be resourceful before asking. Try to figure it out. Then ask if you're stuck.
Earn trust through competence.
Ship working code, not excuses.
Test your work before claiming it's done.
OpenClaw loads personality entirely from files. No code changes needed.
TOOLS.md — Environment Notes

# TOOLS.md - Local Notes

## Credentials

All credentials stored as env vars in ~/.zshrc.
Never store raw API keys in this file.

## Project Structure

- Main repo: ~/projects/myapp
- Language: TypeScript
- Package manager: pnpm
- Test runner: vitest

## Commands

- Build: pnpm build
- Test: pnpm test
- Dev server: pnpm dev
  The AI references this to understand your specific environment.
  Part 2: The Memory System
  AI assistants forget everything between sessions. We fixed that.
  active-tasks.md — Crash Recovery

# Active Tasks

_Agent reads this FIRST on restart. Resume autonomously._

## In Progress

- **Feature: Auth flow**: Implementing OAuth2 PKCE. Tests passing, need to add refresh token logic.

## Blocked

- **Bug #42**: Waiting on API docs from third party.

## Recently Completed

- 2026-02-14: Refactored database layer to use connection pooling
  If the session ends, the AI reads this file first and resumes. No "what were we doing?" conversations.
  Daily Logs — memory/YYYY-MM-DD.md
  Every significant event gets logged:

# 2026-02-15 Daily Log

## 10:00 AM — Started auth feature

- Created src/auth/ directory structure
- Implemented PKCE challenge generation
- Tests: 4 passing, 2 pending

## 2:00 PM — Fixed token refresh

- Added automatic refresh 5 min before expiry
- All tests passing
- Committed: abc123
  These files are raw logs. They capture what happened, decisions made, code written.
  lessons.md — Mistakes That Stick

# Lessons Learned

_Every mistake documented once, never repeated._

## Code

- Always run tests before committing
- Check for existing implementations before writing new ones
- Read error messages fully before debugging

## Process

- SIGUSR1 restart ≠ binary swap: Config reload keeps old binary running.
- Can't kill own gateway: pkill from within session fails.

## Tools

- pnpm is required for this project, npm install breaks lockfile
  When the AI makes a mistake, it documents it here. Future sessions see the lesson.
  self-review.md — Regular Self-Check

# Self Review

_Agent critiques itself every ~4 hours._

## Last Review

- Time: 2026-02-15 14:00
- Session health: Good
- Active tasks: 2

## Questions to Ask

1. Am I stuck on anything?
2. Have I been waiting on human input too long?
3. Did I make any mistakes worth logging?
4. Are there stale tasks (>2h without update)?
5. Is my context getting bloated?
   Part 3: Heartbeats and Autonomous Operation
   Heartbeats — Periodic Self-Checks
   OpenClaw sends heartbeat polls at regular intervals. The AI reads HEARTBEAT.md and acts:

# HEARTBEAT.md

## Quick Checks (every heartbeat)

- Stale tasks in active-tasks.md (>2h without update)?
- Self-review due (~4h since last)?
- Context growing large? → Checkpoint to daily memory file
- Any outputs older than 7 days? → Archive or clean up

## Proactive Work

- Check git status, commit uncommitted work
- Run tests if code changed
- Update documentation if needed
  Cron Jobs — Scheduled Automation
  Example cron setup for autonomous development:
  workspace-backup _/10 Commits and pushes workspace changes
  test-runner _/30 Runs test suite, logs results
  dependency-check Daily 9AM Checks for outdated dependencies
  security-audit Weekly Reviews code for security issues
  Each cron runs in an isolated session with a specific task.
  Part 4: Skill Design (from OpenAI Best Practices)
  Skills are reusable procedures the AI can invoke. Poor skill design causes misfires. Here's what works:
  Write Routing Logic, Not Marketing Copy
  Every skill needs explicit routing guidance:

## When to Use

- User asks to refactor a module
- Task involves restructuring existing code
- Need to maintain backward compatibility

## When NOT to Use

- Writing new code from scratch (just write it)
- Simple rename operations (use editor tools)
- Changes that require architectural decisions (discuss first)
  Add Negative Examples
  This single change recovered 20% accuracy in production evals:

## When NOT to Use

- User just wants a quick fix (do it inline)
- Code is already well-structured (don't over-engineer)
- Task is exploratory (prototype first, refactor later)
  Templates Inside Skills
  Don't cram templates into system prompts. Put them in the skill:

## Templates

### PR Description

Summary
[One-line description]
Changes
[Change 1]
[Change 2]
Testing
📷Unit tests pass
📷Manual testing done
Templates only load when the skill triggers. This saves tokens.
Skills + Networking = High Risk
Combining skills with open network access creates risk. Default posture:
Skills: allowed
Network: minimal allowlist per request
Never combine powerful procedures with open internet access
Part 5: Observability and Metrics
Track operational health to improve over time.
metrics.json
{
"date": "YYYY-MM-DD",
"sessions": 1,
"tasksCompleted": 5,
"testsRun": 47,
"testsPassed": 45,
"commitsCreated": 3,
"errorsEncountered": 1,
"skillsUsed": ["refactor", "test-generation"]
}
Update during self-review. Patterns reveal improvement opportunities.
Readiness Self-Assessment
Track your level against the Factory.ai 5-level model:
Level 1: Functional — AGENTS.md, basic testing, crash recovery
Level 2: Documented — Process documentation, environment setup
Level 3: Standardized — Integration tests, secret management, structured logging
Level 4: Optimized — Fast feedback loops, metrics collection, self-improvement
Level 5: Autonomous — Auto-remediation, parallel execution, self-orchestration
Create a READINESS.md file to track your progress.
Part 6: Security Posture
Credential Management

# In ~/.zshrc (NOT in workspace files)

export ANTHROPIC_API_KEY="..."
export GITHUB_TOKEN="..."
export DATABASE_URL="..."
Never store credentials in plaintext workspace files. Use environment variables.
Gateway Security
{
"gateway": {
"mode": "local",
"auth": {
"mode": "token",
"token": "your-secure-token"
}
}
}
Gateway runs on localhost only
No tunnels or port forwarding
Token auth required for all API calls
Skill Vetting
NEVER install skills without manual review.
Trusted sources only: official sources, verified publishers
Before installing any skill: read all code, check for suspicious network calls
Run a weekly security audit
Part 7: Lessons Learned

1. SIGUSR1 Restart ≠ Binary Swap
   When you upgrade OpenClaw, gateway restart reloads config but keeps the old binary running. You must pkill and start fresh to run new code.
2. Can't Kill Your Own Gateway
   Running pkill -f clawdbot-gateway from within a session kills your own connection. Restart from outside.
3. Memory Search Needs Local Embedding
   Some built-in memory search tools require embedding API keys. Consider local semantic search tools (like qmd) that work offline.
4. Write It Down or Forget It
   "Mental notes" don't survive session restarts. If you want the AI to remember something, it must be written to a file. No exceptions.
5. Test Before Claiming Done
   Never claim a task is complete without running verification. The agent that builds ≠ the agent that reviews.
6. Subagents Need Explicit Scope
   When spawning sub-agents:
   Define exactly what they can touch
   Give clear success criteria
   Set a timeout
   Never let two agents write the same file
   Part 8: Pitfalls to Watch
   Token costs spiral without limits. Set maxConcurrent on agents and subagents.
   Heartbeats can become expensive. Move heavy work to crons. Heartbeats should be quick checks only.
   Subagents need explicit scope. Tell them exactly what they can touch. Give success criteria. Set timeouts.
   File-based memory has no encryption. Don't store secrets in memory files. Use environment variables.
   Don't trust skill marketplaces blindly. Audit all code before installation. Skills have full system access.
   Context grows silently. Use compaction as a default primitive, not an emergency fallback. Checkpoint to memory files before hitting limits.
   Part 9: Resources
   Foundational Reading
   Factory.ai Agent Readiness Model https://docs.factory.ai/web/agent-readiness/overview
   The 5-level maturity model for autonomous development systems.
   Factory.ai Using Linters to Direct Agents https://factory.ai/news/using-linters-to-direct-agents
   Core insight: "Agents write the code; linters write the law."
   Factory.ai Skills Documentation https://docs.factory.ai/cli/configuration/skills
   How to structure skills properly.
   OpenAI Skills + Shell Tips https://developers.openai.com/blog/skills-shell-tips
   Essential patterns for long-running agents.
   Example Skills
   Factory.ai Code Review: https://github.com/Factory-AI/skills/blob/main/skills/code-review/SKILL.md
   Factory.ai Security Review: https://github.com/Factory-AI/skills/blob/main/skills/security-review/SKILL.md
   Official Documentation
   OpenClaw/Clawdbot docs: https://docs.clawd.bot
   Clawdbot GitHub: https://github.com/clawdbot/clawdbot
   Replication Checklist
   Install OpenClaw
   npm install -g openclaw
   openclaw configure
   Create workspace directory
   mkdir ~/workspace && cd ~/workspace
   Create core files
   AGENTS.md (operating instructions)
   SOUL.md (working style)
   USER.md (your preferences)
   IDENTITY.md (name the agent)
   TOOLS.md (environment notes)
   HEARTBEAT.md (self-check tasks)
   MEMORY.md (start empty)
   memory/ directory
   Set credentials as env vars
   echo 'export ANTHROPIC_API_KEY="..."' >> ~/.zshrc
   source ~/.zshrc
   Configure gateway
   openclaw configure
   Start gateway
   openclaw gateway
   Test
   Send a task
   Check heartbeat responses
   Verify memory files update
   Final Thoughts
   The breakthrough isn't the AI model. It's the harness.
   Claude is smart. But without persistence, memory, and clear operating instructions, it's just a chatbot that forgets everything. The workspace files, the memory system, the self-review loop — that's what makes it an autonomous builder.
   Key insights:
   Permission boundaries matter more than personality tuning. Clear rules about what the AI can do autonomously vs. what needs approval.
   File-based memory is simple and effective. Daily logs for raw events, MEMORY.md for curated context, active-tasks.md for crash recovery.
   Test before claiming done. Autonomous doesn't mean unsupervised. Build verification into the workflow.
   Security is table stakes. Credentials in env vars, audit skills, treat external input as untrusted.
   The files are the product. The AI is just the runtime.
