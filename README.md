### Hi, I'm Pravesh 👋

I build **AI systems that talk, decide, and stay up** — real-time voice agents, LLM orchestration, and the resilience plumbing underneath them.

Most of my work sits at the boundary where a language model meets production reality: streaming latency budgets measured in hundreds of milliseconds, providers that fall over mid-request, context that has to be *selected* rather than dumped into a prompt, and delivery guarantees that survive a crash. I care more about what happens on the bad day than on the demo.

---

### Featured work

**[langbreaker](https://github.com/pravesh-dholwani/langbreaker)** — *stateful circuit breakers for LangChain fallback chains*
LangChain's `with_fallbacks` is stateless, so every request retries a dead primary first and pays its full timeout. This wraps the chain in per-model circuit breakers backed by Redis and Lua: a known-bad model is skipped instantly, one pod across the cluster issues the recovery probe, and state propagates over pub/sub. One-line API change, plus an `lccb` CLI for inspecting and overriding circuits in production.
`Python` · `LangChain` · `Redis` · `Lua`

**[personalized-context-engine](https://github.com/pravesh-dholwani/personalized-context-engine)** — *the intelligence layer between structured services and an LLM*
Detects intent, pulls only the context that intent actually needs from four upstream services, personalizes tone and length, and returns a grounded, sourced answer. Intent classification is LLM-primary with a keyword fallback; context selection is YAML configuration rather than a wall of `if/else`; a failed upstream lowers confidence instead of erroring. Runs end to end with no API key via a mock provider.
`Python` · `FastAPI` · `OpenAI` · `Docker Compose`

**[real-estate-sales-voice-agent](https://github.com/pravesh-dholwani/real-estate-sales-voice-agent)** — *streaming voice sales agent with real interruption handling*
A cascaded STT → orchestrator → TTS pipeline on Pipecat. The orchestrator runs a reason–act–observe loop, follows a sales script, and keeps a LIFO task stack — so a mid-sentence barge-in gets classified: a backchannel is ignored, a side question parks the primary task and resumes it after answering, a correction invalidates stale work. Tokens stream into per-sentence TTS, so it starts speaking before the reply exists.
`Python` · `Pipecat` · `WebRTC` · `Groq` · `Silero VAD`

**[pulse](https://github.com/pravesh-dholwani/pulse)** — *at-least-once fan-out webhook delivery*
Never skip an event, tolerate duplicates. Postgres is the source of truth and the retry scheduler; Redis Streams carries only work that is due right now. HMAC-signed deliveries, per-endpoint retry policies, and two independent crash-recovery layers — a fast Redis `XAUTOCLAIM` path and a durable Postgres reaper. Five processes that scale independently, plus a dependency-free web console.
`Python` · `FastAPI` · `PostgreSQL` · `Redis Streams` · `Docker`

<sub>Also around: **[todo-with-llm](https://github.com/pravesh-dholwani/todo-with-llm)** (a to-do list you talk to), **[lyrics-explainer](https://github.com/pravesh-dholwani/lyrics-explainer)** (explains song lyrics across languages), **[skillsnapai](https://github.com/pravesh-dholwani/skillsnapai)**, and a trail of older experiments.</sub>

---

### Toolbox

| | |
|---|---|
| **Languages** | Python (primary), JavaScript, SQL |
| **AI / LLM** | LangChain · OpenAI · Anthropic · Groq · prompt & context engineering · RAG · tool-calling agents |
| **Voice** | Pipecat · WebRTC · streaming STT/TTS · VAD & turn-taking · barge-in handling |
| **Backend** | FastAPI · asyncio · REST APIs · event-driven workers · webhooks |
| **Data & infra** | PostgreSQL · Redis (Streams, Lua, pub/sub) · Docker & Compose |
| **Practice** | pytest · graceful degradation · idempotency & retries · design docs before code |

---

### How I work

- **Design doc before code.** Non-trivial repos start with a written design (`langbreaker`'s covers streaming, retries, and split-brain analysis before a line of the library exists).
- **State the assumptions.** If the spec is ambiguous, I write down the call I made and why, instead of leaving it implicit for someone to discover later.
- **Say what's out of scope, on purpose.** Every featured repo has a "what I'd improve with more time" and a "left out of scope" section — cut corners are labeled, not hidden.
- **Tests over confidence.** `personalized-context-engine` ships 35 tests, `pulse` and `langbreaker` ship unit coverage for the parts most likely to be silently wrong (retry/cache logic, backoff, signing).

---

### Currently working on

- Production LLM resilience — circuit breaking, fallback chains, and the failure modes that only show up under real traffic.
- Real-time voice agents: cutting end-to-end latency and making interruptions feel like a conversation rather than a state machine.
- Context engineering — deciding what an LLM *should* see, which is almost always less than what's available.

<sub>Rough edges and half-finished ideas are documented in the repos themselves; most READMEs have a "what I'd improve with more time" section.</sub>

---

### Get in touch

- **LinkedIn** — [linkedin.com/in/pravesh-dholwani-41742421b](https://www.linkedin.com/in/pravesh-dholwani-41742421b/)
- **Email** — dholwanipravesh05@gmail.com
- **Website** — [praveshdholwani.vercel.app/](https://praveshdholwani.vercel.app/)

