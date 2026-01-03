<p align="center">
  <svg viewBox="0 0 800 200" xmlns="http://www.w3.org/2000/svg" width="100%">
    <defs>
      <pattern id="paperTexture" patternUnits="userSpaceOnUse" width="100" height="100">
        <rect width="100" height="100" fill="#FAF7F2"/>
        <circle cx="25" cy="25" r="0.5" fill="#E8DFD0" opacity="0.4"/>
        <circle cx="75" cy="75" r="0.3" fill="#E8DFD0" opacity="0.3"/>
        <circle cx="50" cy="10" r="0.4" fill="#E8DFD0" opacity="0.35"/>
        <circle cx="10" cy="60" r="0.35" fill="#E8DFD0" opacity="0.3"/>
        <circle cx="90" cy="40" r="0.45" fill="#E8DFD0" opacity="0.25"/>
      </pattern>
      <linearGradient id="goldAccent" x1="0%" y1="0%" x2="100%" y2="0%">
        <stop offset="0%" stop-color="#D97706" stop-opacity="0"/>
        <stop offset="15%" stop-color="#D97706" stop-opacity="1"/>
        <stop offset="85%" stop-color="#D97706" stop-opacity="1"/>
        <stop offset="100%" stop-color="#D97706" stop-opacity="0"/>
      </linearGradient>
    </defs>
    <rect width="800" height="200" fill="url(#paperTexture)" rx="8"/>
    <rect x="1" y="1" width="798" height="198" fill="none" stroke="#EDE6D6" stroke-width="2" rx="7"/>
    <line x1="60" y1="30" x2="60" y2="170" stroke="#B91C1C" stroke-width="1" opacity="0.2"/>
    <text x="400" y="95" text-anchor="middle" font-family="Georgia, 'Times New Roman', serif" font-size="64" font-weight="300" letter-spacing="-1">
      <tspan fill="#78716C">Open</tspan><tspan fill="#1C1917" dx="8"> Prose</tspan>
    </text>
    <rect x="250" y="110" width="300" height="2" fill="url(#goldAccent)" rx="1"/>
    <text x="400" y="150" text-anchor="middle" font-family="Georgia, 'Times New Roman', serif" font-size="18" fill="#78716C" font-style="italic" letter-spacing="0.5">
      A new kind of language for a new kind of computer
    </text>
    <path d="M 30 30 L 30 50 M 30 30 L 50 30" stroke="#A8A29E" stroke-width="1.5" fill="none" stroke-linecap="round"/>
    <path d="M 770 30 L 770 50 M 770 30 L 750 30" stroke="#A8A29E" stroke-width="1.5" fill="none" stroke-linecap="round"/>
    <path d="M 30 170 L 30 150 M 30 170 L 50 170" stroke="#A8A29E" stroke-width="1.5" fill="none" stroke-linecap="round"/>
    <path d="M 770 170 L 770 150 M 770 170 L 750 170" stroke="#A8A29E" stroke-width="1.5" fill="none" stroke-linecap="round"/>
  </svg>
</p>

<p align="center">
  <em>A long-running AI session is a Turing-complete computer. OpenProse is a programming language for it.</em>
</p>

<p align="center">
  <a href="https://prose.md">Website</a> •
  <a href="skills/open-prose/prose.md">Language Spec</a> •
  <a href="examples/">Examples</a>
</p>

---

```prose
# Research and write workflow
agent researcher:
  model: sonnet
  skills: ["web-search"]

agent writer:
  model: opus

parallel:
  research = session: researcher
    prompt: "Research quantum computing breakthroughs"
  competitive = session: researcher
    prompt: "Analyze competitor landscape"

loop until **the draft meets publication standards** (max: 3):
  session: writer
    prompt: "Write and refine the article"
    context: { research, competitive }
```

## The Intelligent Inversion of Control

Traditional orchestration requires explicit coordination code. OpenProse inverts this—you declare agents and control flow, and an AI session wires them up. **The session is the IoC container.**

### 1. The Session as Runtime

Other frameworks orchestrate agents from outside. OpenProse runs *inside* the agent session—the session itself is both interpreter and runtime. It doesn't just match names; it understands context and intent.

### 2. The Fourth Wall (`**...**`)

When you need AI judgment instead of strict execution, break out of structure:

```prose
loop until **the code is production ready**:
  session "Review and improve"
```

The `**...**` syntax lets you speak directly to the OpenProse VM. It evaluates this semantically—deciding what "production ready" means based on context.

### 3. Open Standard, Zero Lock-in

OpenProse is a skill you import into Claude Code, OpenCode, Codex, Amp, or any compatible AI assistant. It's not a library you're locked into—it's a language specification.

Switch platforms anytime. Your `.prose` files work everywhere.

### 4. Structure + Flexibility

**Why not just plain English?** You can—that's what `**...**` is for. But complex workflows need unambiguous structure for control flow. The AI shouldn't have to guess whether you want sequential or parallel execution.

**Why not rigid frameworks?** They're inflexible. OpenProse gives you structure where it matters (control flow, agent definitions) and natural language where you want flexibility (conditions, context passing).

## Install (Claude Code)

```bash
/plugin marketplace add git@github.com:openprose/prose.git
/plugin install prose@open-prose
```

Then:

```
"Run the code review example from OpenProse"
"Execute my-workflow.prose"
"Write me an OpenProse workflow for debugging"
```

## Language Features

| Feature | Example |
|---------|---------|
| Agents | `agent researcher: model: sonnet` |
| Sessions | `session "prompt"` or `session: agent` |
| Parallel | `parallel:` blocks with join strategies |
| Variables | `let x = session "..."` |
| Context | `context: [a, b]` or `context: { a, b }` |
| Fixed Loops | `repeat 3:` and `for item in items:` |
| Unbounded Loops | `loop until **condition**:` |
| Error Handling | `try`/`catch`/`finally`, `retry` |
| Pipelines | `items \| map: session "..."` |
| Conditionals | `if **condition**:` / `choice **criteria**:` |

See the [Language Reference](skills/open-prose/prose.md) for complete documentation.

## Examples

The plugin ships with 27 ready-to-use examples:

| Range | Category |
|-------|----------|
| 01-08 | Basics (hello world, research, code review, debugging) |
| 09-12 | Agents and skills |
| 13-15 | Variables and composition |
| 16-19 | Parallel execution |
| 20 | Fixed loops |
| 21 | Pipeline operations |
| 22-23 | Error handling |
| 24-27 | Advanced (choice, conditionals, blocks, interpolation) |

Start with `01-hello-world.prose` or `03-code-review.prose`.

## How It Works

### The OpenProse VM

The OpenProse VM is an AI session that acts as an intelligent runtime:

| Aspect | Behavior |
|--------|----------|
| Execution order | **Strict** — follows program exactly |
| Session creation | **Strict** — creates what program specifies |
| Parallel coordination | **Strict** — executes as specified |
| Context passing | **Intelligent** — summarizes/transforms as needed |
| Condition evaluation | **Intelligent** — interprets `**...**` semantically |
| Completion detection | **Intelligent** — determines when "done" |

### Documentation Files

| File | Purpose | When to Read |
|------|---------|--------------|
| `interpreter.md` | OpenProse VM semantics | Always, for running programs |
| `prose.md` | Full language spec | For compilation, validation, or syntax questions |

## FAQ

**Why not LangChain/CrewAI/AutoGen?**
Those are orchestration libraries—they coordinate agents from outside. OpenProse runs inside the agent session—the session itself is the IoC container. Zero external dependencies, portable across any AI assistant.

**Why not just plain English?**
You can use `**...**` for that. But complex workflows need unambiguous structure for control flow—the AI shouldn't guess whether you want sequential or parallel execution.

**What's "intelligent IoC"?**
Traditional IoC containers (Spring, Guice) wire up dependencies from configuration. OpenProse's container is an AI session that wires up agents using *understanding*. It doesn't just match names—it understands context, intent, and can make intelligent decisions about execution.

## License

MIT
