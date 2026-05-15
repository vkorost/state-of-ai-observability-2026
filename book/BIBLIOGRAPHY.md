## Further Reading
This list is organized by the rate of change of the knowledge it contains, following the three-tier structure introduced in Chapter 12. Reading at the pace appropriate to each tier avoids the twin failure modes of treating fast-moving claims as permanent and discarding durable principles because they feel less current.

---

### Stable Tier: Primary Sources

These works have persisted across multiple major technology transitions without requiring structural revision to their core arguments. They are worth reading once in depth and revisiting as reference.

**Martin Kleppmann.** *Designing Data-Intensive Applications.* O'Reilly Media, 2017. The foundational text for understanding the structural properties of distributed storage systems. The arguments about consistency tradeoffs, storage architecture, write throughput, and read latency underlie every cardinality, retention, and sampling argument in this book. Not specific to AI systems, which is precisely why it is stable-tier: the storage principles it describes apply to any system that must store, index, and retrieve data at scale.

**Betsy Beyer, Chris Jones, Jennifer Petoff, and Niall Richard Murphy.** *Site Reliability Engineering: How Google Runs Production Systems.* O'Reilly Media, 2016. The foundational text for error budget mechanics, toil reduction, and service level objective design. Chapter 5's treatment of SLO discipline for non-deterministic AI systems rests directly on the error budget framework established here. The framework has survived the transition from monolithic services to microservices to serverless to AI-augmented services without structural revision.

**Charity Majors, Liz Fong-Jones, and George Miranda.** *Observability Engineering: Achieving Production Excellence.* O'Reilly Media, first edition 2022; second edition 2025 (with additional chapters on AI agents and AI-workload observability). The foundational text for the three-pillar model and its extension requirements. The first-edition core chapters establishing high-cardinality event-driven observability are stable-tier. The second-edition AI chapters are medium-tier: they address a rapidly evolving product and practice landscape that will continue to evolve after their publication date.

**Nassim Nicholas Taleb.** *Antifragile: Things That Gain from Disorder.* Random House, 2012. The conceptual grounding for the Lindy filter introduced in Chapter 12. The argument that knowledge surviving multiple cycles of falsification is more likely to survive the next cycle than knowledge that is merely novel applies to observability engineering without modification.

---

### Medium-Cadence Tier: Practitioner Sources

These sources require quarterly re-engagement. The knowledge they contain is valid across a multi-year horizon but is refined regularly as the field evolves.

**OpenTelemetry GenAI Semantic Conventions.** Repository: github.com/open-telemetry/semantic-conventions-genai. The changelog tracks which span attributes are stable, experimental, or deprecated as of each release. Following the changelog on a quarterly basis is the minimum required reading for any team implementing instrumentation against the OTel GenAI specification. Chapter 8 treats v1.37 as the Q2 2026 baseline; the reader should verify the current version before implementing.

**Datadog DASH recordings.** Available at datadoghq.com, released approximately quarterly. The DASH talks cited in this book, from the December 2025 Bits AI SRE GA announcement through the May 2026 sessions on agent execution and reliability, are available on demand. Subsequent DASH announcements supersede the product-state descriptions in Part IV of this book; following DASH recordings quarterly provides the most current product-state picture.

**Honeycomb Engineering Blog.** blog.honeycomb.io. Charity Majors and the Honeycomb team publish practitioner-validated accounts of observability engineering decisions, including the Query Assistant SLO design documented by Phillip Carter and cited in Chapter 5. The blog provides the practitioner-community layer that bridges principle-level research and fast-tier product implementation.

**Applied-LLMs Collective Publications.** The practitioner-validated accounts published by Eugene Yan, Hamel Husain, Jason Liu, Shreya Shankar, Bryan Bischof, and Charles Frye provide the operational ground-truth for what LLM evaluation practices look like in production. These publications are specifically useful for the evaluation-tooling decisions that Chapter 5 and Chapter 10 address at the principle level.

**Austin Parker, Honeycomb.** Parker's published framework for trust-ramp governance of agentic systems, referenced in Chapter 10 (April 2026), and his broader writing on OpenTelemetry and agentic instrumentation provide practitioner-level guidance on the governance questions Chapter 11 identifies as unresolved at Q2 2026.

---

### Fast-Moving Tier: Changelog Sources

These sources require monthly monitoring. The specific claims from Part IV of this book that are most likely to be superseded are best tracked here.

**Datadog Documentation Changelog.** docs.datadoghq.com (changelog section). Records when features move from preview to general availability, when billing models change, and when new frameworks are added to auto-instrumentation coverage. The LLM Observability documentation changelog specifically will record the transitions that Part IV describes as in-progress at Q2 2026: the AI Agents Console from preview, the Bits AI agent handoff workflow developments, and the evaluation tooling layer evolution.

**Langfuse Release Notes.** langfuse.com/changelog. The evaluation tooling category moves faster than the operational monitoring category. Langfuse's changelog tracks annotation queue improvements, prompt management lifecycle changes, and OTel integration updates at a cadence of weeks.

**LangSmith Release Notes.** docs.smith.langchain.com/changelog. LangSmith's annotation queue, CI/CD gating features, and LangGraph-specific debugging capabilities are in active development. Release notes track which capabilities move from beta to stable and what new capabilities ship.

**Braintrust Release Notes.** braintrust.dev/docs/changelog. Braintrust's CI/CD blocking gates, production-to-eval conversion pipeline, and Loop AI features are the primary competitive differentiators documented in Chapter 10. Release notes track their evolution.

**Arize Phoenix Release Notes.** docs.arize.com/phoenix (changelog). Phoenix's RAG evaluators and agentic path analysis capabilities, assessed in Chapter 10's competitive treatment, evolve with each release. The Arize AX Enterprise Kubernetes deployment path and its data residency characteristics are tracked here.

**OpenTelemetry GenAI Semantic Conventions Working Group.** github.com/open-telemetry/semantic-conventions-genai/issues. The working group's active issue queue tracks which attribute names are under active debate, which are approaching stable status, and which have been proposed but not yet accepted. Following this queue is necessary for teams implementing instrumentation that they expect to remain convention-compatible across releases.

---

### The Postmortem Layer

Published incident retrospectives from companies with transparent postmortem cultures provide the practitioner-validated account of what production AI system failures actually look like from inside the engineering organization. The incidents cited in this book, including the Replit Agent database destruction (July 2025), the PocketOS database destruction (April 2026), the $47,000 A2A loop (November 2025), and the Virgin Atlantic AI concierge development account, are examples of this category. Following the engineering blogs, postmortem repositories, and incident disclosure databases of teams doing serious AI production work, including the OECD AI Incident Database (oecd.ai/en/incidents), the AI Incident Database (incidentdatabase.ai), and the engineering blogs of companies that have published accounts of their AI system failures, is the most direct way to track what production AI observability looks like in practice. These accounts are not available from vendor documentation or academic research, and they provide the bridge between the principles in Part II and the implementation decisions in Part IV.

The reading list is not a bibliography. It is a maintenance schedule for the knowledge this book deploys.
