## Glossary of Named Patterns

The following entries catalog every named pattern introduced in this book, in alphabetical order. Each entry gives the canonical definition, drawn from the chapter that introduces the pattern, and the chapter number where the full treatment appears.

---

**The 1 MB Payload Ceiling.** The hard per-span payload size limit enforced by Datadog LLM Observability, which truncates prompt and response payloads that exceed one megabyte, creating a structural tension between capturing full conversational context and staying within the trace storage budget. Chapter 7.

**The AI Application Surface.** The complete set of new components that generative AI systems introduce as observable entities, including LLM calls, RAG pipelines, vector stores, agentic orchestration loops, and multi-model chains, each emitting telemetry primitives that did not exist in the pre-AI APM taxonomy. Chapter 2.

**Auto-Instrumentation Coverage.** The set of AI frameworks and providers for which Datadog's ddtrace library and the OpenTelemetry GenAI semantic conventions provide zero-code or low-code span capture, as distinct from the set that requires manual instrumentation. Chapter 8.

**The Autonomous Monitoring Loop.** The recursive condition that emerges when the system doing anomaly detection and remediation is itself an AI system whose behavior requires monitoring, so the observability platform must observe the observer. Chapter 11.

**The Cardinality Cliff.** The point at which one new high-entropy tag dimension causes observability storage cost to compound superlinearly, a threshold that AI workloads reach faster than traditional APM because prompt and response text naturally inhabits tag positions that APM was designed to keep low-cardinality. Chapter 3.

**Cardinality Control.** The engineering practice of deliberately limiting the number of indexed tag dimensions in Datadog to prevent superlinear cost growth, including techniques for choosing which span attributes to index, which to store unindexed, and which to discard entirely. Chapter 9.

**The Datadog AI Surface.** The full set of AI-related product capabilities Datadog has shipped between August 2023 and Q2 2026, organized across three successive waves: LLM Observability, the agentic platform layer, and the autonomous-operations layer (Bits AI). Chapter 7.

**The Decision Framework.** The three-way fork that production AI teams navigate when choosing their observability toolchain: Datadog alone, Datadog plus one specialized evaluation tool, or Datadog plus an OTel-native open-source stack, each carrying distinct trade-offs in coverage, cost, and organizational complexity. Chapter 10.

**The Eval/Ops Split.** The principled separation between production observability (is the system healthy?) and LLM evaluation (is the model performing well?), two disciplines that answer different questions, require different methods, and must not be conflated in toolchain design or team ownership. Chapter 5.

**The Lindy Filter.** A durability heuristic that assesses how likely a piece of technical knowledge is to remain valid over a multi-year horizon, based on how long it has already survived: concepts that have persisted through multiple tool generations are more likely to persist through the next one than claims that depend on a specific product version or vendor roadmap announcement. Chapter 12.

**The Observability Gap.** The collective set of AI-era blindspots where current observability tooling cannot see: token-level cost attribution, non-deterministic latency, prompt payloads too large for spans, agentic execution topology, and the confusion between evaluation and operational signals. Chapter 1.

**The Platform Stack vs The Specialized Stack.** The architectural choice between using a single unified observability platform (Datadog) that covers operational monitoring and has partial evaluation capabilities, versus pairing a platform tool with one or more specialized LLM evaluation tools (Langfuse, LangSmith, Braintrust, Arize Phoenix). Chapter 10.

**The Retrieval Layer.** The subsystem within a RAG pipeline that fetches document chunks from a vector store and injects them into the prompt context, introducing its own class of failure modes including embedding drift, index staleness, relevance degradation, and context window poisoning. Chapter 2.

**The Retention Tier.** The Datadog storage architecture that separates log and trace data into cost tiers by freshness and access frequency, enabling teams to retain large telemetry volumes at low cost while keeping recent, high-value data in fast-query indexed storage. Chapter 9.

**The Runaway Cost Loop.** An agentic failure pattern in which a tool-calling loop or multi-agent cycle consumes LLM tokens and incurs API charges at an accelerating rate without triggering any automated intervention, because observability tools record the loop but cannot halt it and provider spend caps enforce with hours of lag. Chapter 6.

**The Sampling Trilemma.** The three-way tension between coverage completeness, cost control, and diagnostic fidelity when choosing a sampling strategy for AI workloads, where each of the three desiderata can only be maximized at the expense of at least one other. Chapter 3.

**The Shadow Agent Problem.** The governance gap that arises when autonomous remediation agents (such as Bits AI SRE) can open production PRs or execute infrastructure changes with inherited operator permissions and no out-of-band trust-verification step, making the agent's actions hard to audit or reverse. Chapter 11.

**The Six Incident Categories.** The taxonomy of AI-era production failure modes documented in the corpus: PII leaks into LLM contexts, runaway agent cost loops, behavioral drift in deployed AI systems, prompt injection attacks, AI-authored bugs reaching production, and agent scope creep. Chapter 6.

**The Span Taxonomy.** Datadog's structured classification of LLM Observability spans by kind (llm, tool, retrieval, embedding, workflow, agent, task), which maps the steps of an AI pipeline onto the trace hierarchy in a way that preserves correlation with standard APM spans. Chapter 7.

**The Span Topology Problem.** The structural difficulty of representing agentic execution as a parent-child span hierarchy when agent loops, orphaned spans, async callbacks, and multi-model routing produce trace shapes that span visualization tools cannot render coherently. Chapter 4.
