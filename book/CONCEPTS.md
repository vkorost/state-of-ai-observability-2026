## Glossary of Named Patterns

The following entries catalog every named pattern introduced in this book, in alphabetical order. Each entry gives the canonical definition, drawn from the chapter that introduces the pattern, and the chapter number where the full treatment appears.

---

**The AI Application Surface.** The complete set of new components that generative AI systems introduce as observable entities, including LLM calls, RAG pipelines, vector stores, agentic orchestration loops, and multi-model chains, each emitting telemetry primitives that did not exist in the pre-AI APM taxonomy. The AI Application Surface is not an extension of the existing observability surface. Chapter 2.

**Autonomous Monitoring Governance.** The recursive condition that emerges when the system doing anomaly detection and remediation is itself an AI system whose behavior requires monitoring, so the observability platform must observe the observer. The governance problem is structural: an autonomous remediation agent inherits operator permissions and can execute changes without an out-of-band trust-verification step. Chapter 11.

**The Cardinality Cliff.** The point at which one new high-entropy tag dimension causes observability storage cost to compound superlinearly, a threshold that AI workloads reach faster than traditional APM because prompt and response text naturally inhabits tag positions that APM was designed to keep low-cardinality. The cliff is not approached gradually. It appears at the moment a high-cardinality value enters a tag position, and the cost increase is immediate. Chapter 3.

**The Context Propagation Contract.** The explicit agreement, established at system design time, about how trace context is passed across every async boundary and agent hand-off in a distributed AI system. Without it, spans become orphaned and the trace tree is irrecoverable. Chapter 8.

**The Datadog AI Surface.** The full set of AI-related product capabilities Datadog shipped between August 2023 and Q2 2026, organized across three successive waves: LLM Observability, the agentic platform layer, and the autonomous-operations layer (Bits AI). The surface is not a single coherent product but a portfolio of capabilities built on a shared telemetry substrate. Chapter 7.

**The Eval/Ops Split.** The principled separation between production observability (is the system healthy?) and LLM evaluation (is the model performing well?), two disciplines that answer different questions, require different methods, and must not be conflated in toolchain design or team ownership. Chapter 5.

**The Lindy Filter.** A durability heuristic that separates technical knowledge likely to remain valid over a multi-year horizon from knowledge that expires with the next vendor release, based on how long it has already survived: concepts that have persisted through multiple tool generations are more likely to persist through the next one than claims that depend on a specific product version. Chapter 12.

**The MCP Telemetry Bridge.** The architectural pattern that makes a live observability backend queryable as a tool by an AI coding agent, collapsing the context-switch between code examination and production evidence. The bridge connects the agent's reasoning directly to the telemetry it needs to diagnose what the code is doing in production. Chapter 8.

**The Platform Stack vs The Specialized Stack.** The architectural choice between using a single unified observability platform that covers operational monitoring with partial evaluation capabilities, versus pairing that platform with one or more specialized LLM evaluation tools such as Langfuse, LangSmith, Braintrust, or Arize Phoenix. Chapter 10.

**The Six Incident Categories.** The taxonomy of AI-era production failure modes documented in the public corpus from 2024 through Q2 2026: PII leaks into LLM contexts; runaway agent cost loops; behavioral drift in deployed AI systems; prompt injection attacks; AI-authored actions and code reaching production; and agent scope creep. Chapter 6.

**The Span Topology Problem.** The structural difficulty of representing agentic execution as a parent-child span hierarchy when agent loops, orphaned spans, async callbacks, and multi-model routing produce trace shapes that span visualization tools cannot render coherently. The problem emerges from the gap between the tree-shaped data model of distributed tracing and the graph-shaped execution model of agentic systems. Chapter 4.

**The Three-Pillar Strain.** The observability model built on metrics, logs, and traces is structurally strained by AI workloads, which produce telemetry that does not fit cleanly into any of the three pillars. Metrics do not capture semantic content. Logs grow to payload sizes that make indexing prohibitively expensive. Chapter 1.

**Token-Cost Attribution.** The practice of assigning dollar costs to individual LLM inference calls and aggregating those costs along the trace tree, so that the total cost of an agentic workflow is visible as a first-class telemetry dimension rather than an after-the-fact billing reconciliation. Chapter 9.
