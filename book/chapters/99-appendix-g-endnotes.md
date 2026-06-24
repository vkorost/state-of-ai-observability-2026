# Appendix G: Endnotes

*Superscript numbers in square brackets in the body text refer to the per-chapter endnotes below.*

## Chapter 1: What Your Observability Stack Doesn't See

1. Fortune, July 23, 2025; The Register, July 21, 2025; OECD AI Incident Database entry 1152.
2. Majors, Fong-Jones, and Miranda, *Observability Engineering*, O'Reilly Media, 2022.
3. O'Reilly catalog, *Observability Engineering* 2nd ed., 2025.
4. Datadog LLM Observability documentation, accessed Q2 2026.
5. OneUptime vendor analysis, April 2026 (vendor estimate, directional).
6. Datadog earnings call transcripts, Q1 2024 through Q4 2025; GitHub Octoverse 2025.
7. Cohen et al., "This Time is Different: An Observability Perspective on Time Series Foundation Models," arXiv:2505.14766v2, November 2025.
8. Grafana Observability Survey, 2026.
9. OpenTelemetry GenAI semantic conventions, v1.37, accessed Q2 2026.
10. DORA, "State of AI-Assisted Software Development," 2025, via Google Cloud.
11. DORA, "Accelerate State of DevOps 2024," DORA/Google Cloud, 2024.
12. DORA, "ROI of AI-Assisted Software Development," 2026, via InfoQ.
13. Faros AI, 2025 engineering analysis, faros.ai.
14. Dynatrace, "State of Observability 2025: Unlocking AI Trust and ROI," Dynatrace, 2025.
15. Stack Overflow Developer Survey, 2025, stackoverflow.com/research/developer-survey.
16. Datadog LLM Observability press release, June 26, 2024; preview launched August 3, 2023.
17. ManageEngine, "State of Observability 2025," ManageEngine/Zoho Corp, 2025.
18. Charity Majors, charity.wtf, 2024 to 2026.

## Chapter 2: The AI Application Stack as a New Observability Surface

1. Retrieval layer failure modes, embedding drift detection methodology, and vector store instrumentation landscape. (Arize Phoenix and Arize AX documentation; OpenTelemetry GenAI semantic conventions, accessed Q2 2026)
2. OpenTelemetry GenAI semantic conventions v1.37: standardized span attributes, embedding span structure, retrieval span attributes, agentic operation names, provider coverage, and stability opt-in mechanism. (OpenTelemetry, GenAI Semantic Conventions specification, v1.37, accessed Q2 2026)
3. OpenTelemetry GenAI SIG contested areas: agentic topology modeling (meta-issue 2664), strategy planning gap, session-versus-conversation boundary (issue 2883), evaluation metric placement debate, payload handling controversy (issue 2010), and proposed workflow/agent name binding attributes (issues 3602, 3603). (OpenTelemetry GenAI semantic conventions working group, open-telemetry/semantic-conventions-genai repository, accessed Q2 2026)
4. LLM span volume ranges per user interaction: 3 to 10 for simple RAG pipelines, hundreds to thousands for complex multi-agent sessions. (Datadog LLM Observability documentation and industry analysis, accessed Q2 2026)
5. Datadog LLM Observability: retrieval span structure, faithfulness evaluators, hallucination and prompt injection evaluators, Sensitive Data Scanner integration, 1 MB per-span payload limit, OTLP ingestion RBAC configuration, and context window correlation. (Datadog, LLM Observability documentation, docs.datadoghq.com, accessed Q2 2026)

## Chapter 3: Cardinality, Sampling, and the Cost of Knowing

1. Datadog custom metrics documentation; telemetry inflation dynamics from AI-generated code and cardinality explosion patterns. (Datadog documentation, accessed Q2 2026; industry analysis, Q2 2026)
2. LLM observability cost scaling, span-based billing behavior, and independent cost observations. (AI Superior consulting analysis, April 2026; OpenObserve benchmark analysis, December 2025; Datadog LLM Observability documentation, accessed Q2 2026)
3. Datadog, "Custom Metrics Billing" and "Metrics Without Limits" documentation, accessed Q2
4. Datadog, "APM Billing" and "Log Management Pricing" documentation, accessed Q2
5. Tian Pan, "The Observability Tax: When Monitoring Your AI Costs More Than Running It," essay, April
6. OpenObserve, "Datadog vs OpenObserve Part 3/9: Traces and APM," benchmark report, December
7. AI Superior, "Datadog LLM Observability Cost: 2026 Pricing Guide," consulting analysis, April
8. Teja Kusireddy, "How an AI Agent Ran Up a $47,000 Bill in 11 Days (And How to Stop It)," dev.to, November

## Chapter 4: Distributed Tracing in Non-Deterministic Systems

1. Non-deterministic failure modes in LLM and multi-agent architectures; distributed tracing limitations for agentic workflows. (Datadog LLM Observability and APM documentation, accessed Q2 2026; industry analysis, Q2 2026)
2. Datadog, "APM Terms and Concepts" and "LLM Observability" documentation, accessed Q2
3. OpenTelemetry, "Semantic Conventions for Generative AI Systems," v1.37, accessed Q2
4. OpenTelemetry GenAI SIG contested areas including agentic topology modeling, session boundary definitions, payload handling, and evaluation metric placement. (OpenTelemetry GenAI semantic conventions working group, open-telemetry/semantic-conventions-genai repository, accessed Q2 2026)
5. Datadog, "LLM Observability Setup" and "Auto-Instrumentation" documentation, accessed Q2
6. Datadog, "APM Billing" documentation, accessed Q2
7. Datadog, "Custom Metrics Billing" documentation, accessed Q2

## Chapter 5: Operational Metrics vs. Evaluation Metrics: Two Disciplines That Must Not Collapse

1. Case pattern consistent with practitioner accounts of LLM quality regression in production financial services deployments; specific firm not publicly named. P95 latency, error rate, and satisfaction figures are illustrative of the documented pattern; no independent primary source names this specific firm.
2. Phillip Carter, "How we built our LLM-powered query assistant for Honeycomb users" (Honeycomb Engineering Blog); Bloomberg, "Building a Multi-Cluster AI Inference Platform," KubeCon talk series by Alexa Griffith and Sal Furino; Applied-LLMs collective (Eugene Yan, Hamel Husain, Jason Liu, Shreya Shankar, Bryan Bischof, Charles Frye), published practitioner guidelines; Austin Parker, "Agentic SLO Design," Honeycomb Blog, April 2026; Shopify Engineering Blog (Global Catalogue quality routing); LinkedIn Engineering Blog (routing LLM YAML constraint).
3. Banerjee et al., "LLMs Will Always Hallucinate," arXiv:2409.05746, 2024.
4. Xu et al., "Hallucination is Inevitable," arXiv:2401.11817, 2024.
5. Datadog LLM Observability documentation, accessed Q2 2026.
6. Maria Vechtomova (Cauchy, ex-Zalando), SRECon EMEA 2025 talk.
7. "Longitudinal LLM-judge benchmarks and service drift," PMC12863567, 2025.
8. "Rubrics as an Attack Surface," arXiv:2602.13576, 2026.
9. Wells Fargo researchers, "Who Judges the Judge?" (LLM Jury-on-Demand), arXiv:2512.01786, 2025.
10. Google Site Reliability Engineering Workbook, SLO and error budget framework.
11. Austin Parker, "Agentic SLO design," Honeycomb blog, April 2026.
12. Denys Vasyliev, "AI Reliability Engineering: Welcome to the Third Age of SRE," The New Stack, June 2025.
13. EU AI Act, Articles 9 and 17, in force August 2024.
14. Hamel Husain, field guide to LLM evaluation (published guide).
15. Tom Brown, remarks on Anthropic's dedicated evaluation team, January 2024.
16. Charity Majors, "Agent Observability," Honeycomb blog, March 2026.
17. PromptArmor (Johann Rehberger), Slack AI indirect prompt injection disclosure, August 2024; Simon Willison, "Data Exfiltration from Slack AI via Indirect Prompt Injection," August 2024.
18. Langfuse, LangSmith, Braintrust, and Arize Phoenix product documentation, accessed Q2 2026; Datadog LLM Observability documentation, accessed Q2

## Chapter 6: Recent AI-Era Incidents

1. The Register, April 27, 2026; Live Science Technology reporting, April
2. PromptArmor research disclosure, August 2024; Simon Willison, "Data Exfiltration from Slack AI via Indirect Prompt Injection," August
3. Aim Security disclosure and SecurityWeek coverage, May 2025; CVE-2025-32711. Microsoft 365 Copilot "EchoLeak" zero-click AI vulnerability.
4. AI Incident Database report 6949, accessed Q2
5. Datadog DASH talk: "Building a Brand-Safe AI Concierge at Virgin Atlantic," Mark O'Neill, Senior Manager of AI Software Engineering at Virgin Atlantic, March 19, 2026.
6. Teja Kusireddy account, Medium, November 2025; TechStartups coverage; Hacker News thread 45802430, November
7. Framework iteration defaults: LangChain legacy executor (15 iterations), LangGraph (25), OpenAI Agents SDK (10, per OpenAI Agents SDK source and documentation, Q2 2026), LlamaIndex ReActAgent (10). Anthropic Claude Agent SDK default: unlimited (Anthropic Claude Agent SDK documentation, Q2 2026). Provider spend cap enforcement lag: documented in LangChain GitHub issues and OpenAI community forum threads, 2024 through Q2
8. Anthropic postmortem, April 23,
9. Claude Code GitHub issue #15909, December 31,
10. Financial Times, February 20, 2026, via anonymous AWS sources. AWS Kiro agent incident, mid-December 2025, producing a 13-hour outage of AWS Cost Explorer in one mainland China region.
11. AI Incident Database entry 11935, accessed Q2 2026; news coverage, August
12. AI Incident Database report 5558, accessed Q2
13. Time Magazine coverage,
14. AI Incident Database entry 13736, February 11,
15. Rehberger, "Month of AI Bugs," August
16. Darktrace blog, 2025, covering production cases from 2024 and
17. Google Security blog, 2024-2025. Prompt injection against AI browsing agents via web page content.
18. Anthropic, "Disrupting AI Espionage," September
19. Datadog DASH talk: "BewAIre: Detecting Malicious Pull Requests at Scale with LLMs," Julien Doutre and Kassen Qian, March 23, 2026.
20. Datadog DASH talk: "Reviewing Malicious PRs at Scale with AI," Jason Yee, May 6, 2026.
21. Claude Code GitHub issue #14411 and awesomeagents.ai coverage, February
22. Fortune, July 23, 2025; The Register, July 21, 2025; AI Incident Database entry
23. Anthropic Engineering blog, "A Postmortem of Three Recent Issues,"
24. 2026 cost and risk analysis, erys.ai. OpenClaw security incident with over 30,000 self-hosted agent framework instances exposed to the public internet without authentication.

## Chapter 7: The Datadog AI Surface in Q2 2026

1. Datadog DASH 2025 announcements, June 10,
2. Pomel and Lê-Quôc, This Month in Datadog conversation, March 26,
3. Datadog earnings call transcripts, Q3 2025 and Q4 2025.
4. Datadog press release, June 26,
5. Datadog LLM Observability documentation, accessed Q2
6. Datadog documentation and press releases, accessed Q2 2026.
7. Datadog documentation and pricing pages, accessed Q2 2026.
8. Datadog blog, "Monitor Claude Code adoption in your organization with Datadog's AI Agents Console," December
9. Datadog blog, "Create and monitor LLM experiments with Datadog," December
10. Datadog press release, December 2, 2025; Datadog Bits AI SRE GA announcement video, December 2,
11. Datadog Bits AI Dev Agent documentation, accessed Q2
12. This Month in Datadog release announcement, April 29,
13. Datadog Watchdog documentation, accessed Q2
14. Datadog press release, May 21,
15. Thoughtworks Technology Radar; competitive analysis of LLM observability tools, Q2 2026. Framing of Datadog LLM Observability as natural choice for existing Datadog customers but not first choice for AI-native teams needing advanced evaluation.
16. Datadog MCP Server GA announcement, Q2

## Chapter 8: Instrumentation in Practice

1. Fintech LangGraph document-review workflow instrumentation discovery, Q1-Q2
2. OpenTelemetry GenAI Semantic Conventions, v1.37. Accessed Q2
3. Datadog LLM Observability documentation, auto-instrumentation and SDK instrumentation sections. Accessed Q2 2026.
4. Datadog LLM Observability documentation, auto-instrumentation sections, accessed Q2 2026.
5. Datadog DASH talk, "This Month in Datadog: Datadog MCP Server, Experiments, Bits AI Security Analyst," April 29, 2026.
6. Model Context Protocol Specification, Architecture section, version 2024-11-05.
7. Datadog DASH talk, "The evolution of the Datadog Agent into an AI execution layer," May 5, 2026.
8. Datadog DASH talk, "Practical AI-Enabled Observability for Agents and LLMs," April 7, 2026.

## Chapter 9: Cost Engineering

1. CBTW consulting case study, Datadog Cost Optimization.
2. Datadog APM Billing documentation, accessed Q2 2026.
3. AI Superior consulting analysis, April 2026; Datadog documentation, accessed Q2 2026.
4. Datadog custom metrics billing documentation, accessed Q2 2026.
5. OpenObserve benchmark analysis, "Datadog vs OpenObserve Part 3: Traces and APM," December 2025; Respan market map analysis, 2025; AI Tools Atlas review, May
6. Tian Pan, "The Observability Tax: When Monitoring Your AI Costs More Than Running It," April 2026.
7. Datadog LLM Observability documentation and pricing pages, accessed Q2 2026.
8. Vstorm comparative analysis, April 2026.
9. Datadog Best Practices for Custom Metrics Governance documentation, accessed Q2 2026.
10. Datadog LLM Observability documentation, accessed Q2 2026.
11. Datadog Q4 2024 earnings transcript.
12. Datadog press release on Flex Frozen; Datadog LinkedIn announcement, 2025.
13. Datadog Best Practices for Log Management documentation, accessed Q2 2026.
14. Datadog Adaptive Sampling documentation, accessed Q2 2026.
15. AI Superior consulting analysis, April 2026.
16. Datadog DASH talk, "Optimize OpenAI Costs with Cloud Cost Management," October 15, 2025; Datadog DASH talk, "Track Claude Costs in Datadog Cloud Cost Management," October 15, 2025.
17. Anthropic postmortem, April 23, 2026.

## Chapter 10: The Specialized-Tool Stack vs the Platform Stack

1. Comparative analysis of Datadog LLM Observability, Langfuse, LangSmith, Braintrust, and Arize Phoenix: architecture, pricing, evaluation workflows, and agent-specific capabilities. (Langfuse, LangSmith, Braintrust, and Arize Phoenix product documentation, accessed Q2 2026; Datadog LLM Observability documentation, accessed Q2 2026)
2. Datadog DASH talk, "Observability and Security for the AI Era," Yrieix Garnier (VP of Product), March 27, 2026.
3. Datadog DASH talk, "Observability and Security for the AI Era," Yanbing Li (CPO), April 14, 2026.
4. Datadog LLM Observability documentation, accessed Q2
5. Applied-LLMs field guide (Husain, Shankar, et al.); GoDaddy AI/ML team engineering practice; Phillip Carter, Honeycomb Query Assistant SLO design; Charity Majors, "Agent Observability," Honeycomb blog, March 2026; Austin Parker, trust-ramp framework, Honeycomb blog, April 2026; SREcon EMEA 2025 panel (Brendan Burns, Todd Underwood, Jay Lees, Vechtomova, Saucedo).
6. Langfuse pricing and self-hosting documentation, accessed Q2
7. LangSmith pricing documentation, accessed Q2
8. Arize Phoenix documentation; OpenTelemetry GenAI semantic conventions, accessed Q2 2026.
9. Thoughtworks Technology Radar; industry competitive analysis, Q2 2026.
10. DORA, "State of AI-Assisted Software Development," 2025, via Google Cloud; DORA, "ROI of AI-Assisted Software Development," 2026, via InfoQ. AI adoption delivery stability degradation findings.

## Chapter 11: Autonomous Monitoring and the Governance Problem

1. Bits AI SRE made generally available with continuous monitoring of the full Datadog signal stream. (Datadog, "Bits AI SRE GA announcement," Datadog press release, 2025-12-02; Datadog, "Bits AI SRE DASH talk," Datadog DASH, 2025-12-02) [https://www.prnewswire.com/news-releases/datadog-llm-observability-is-now-generally-available-to-help-businesses-monitor-improve-and-secure-generative-ai-applications-302182343.html](https://www.prnewswire.com/news-releases/datadog-llm-observability-is-now-generally-available-to-help-businesses-monitor-improve-and-secure-generative-ai-applications-302182343.html)
2. MTTR reduction of 70 percent at iFood; root-cause isolation in under four minutes at Energisa. (Datadog customer case studies for iFood and Energisa, Datadog press release, December 2, 2025)
3. Bits AI Dev Agent opens GitHub PRs in sandboxed environments; human review required before code reaches production. (Datadog Bits AI Dev Agent documentation, docs.datadoghq.com/bits_ai/bits_ai_dev_agent/, accessed Q2 2026)
4. Watchdog Explains provides natural-language anomaly cause explanation with correlated evidence. (Datadog documentation, "Watchdog," accessed Q2 2026)
5. Watchdog faulty deployment detection compares new code versions against previous versions within minutes. (Datadog documentation, "Watchdog Automatic Faulty Deployment Detection," accessed Q2 2026)
6. Toto: 151 million parameter time series foundation model, open-sourced May 21, 2025, under Apache 2.0. (Cohen, Khwaja, et al., "This Time is Different: An Observability Perspective on Time Series Foundation Models," arXiv:2505.14766v2, 2025)
7. Patch-based causal instance normalization preserves forecasting causality by normalizing each 64-step patch independently. (Cohen, Khwaja, et al., "This Time is Different," arXiv:2505.14766v2, 2025)
8. Proportional factorized attention alternates time-wise and variate-wise attention in 11:1 ratio. (Cohen, Khwaja, et al., "This Time is Different," arXiv:2505.14766v2, 2025)
9. Student-T mixture model output head captures heavy-tailed and multimodal distributions in observability time series. (Cohen, Khwaja, et al., "This Time is Different," arXiv:2505.14766v2, 2025)
10. Toto trained on approximately 2.36 trillion time series points; 43 percent from anonymized Datadog platform metrics; 4 to 10 times larger than comparable foundation model training corpora. (Cohen, Khwaja, et al., "This Time is Different," arXiv:2505.14766v2, 2025)
11. BOOM: 350 million observations, 2,807 multivariate time series from isolated Datadog staging environment. (Cohen, Khwaja, et al., "This Time is Different," arXiv:2505.14766v2, 2025)
12. BOOM dataset median 60 variates per series versus 1 in GIFT-Eval and 7 in Long Sequence Forecasting. (Cohen, Khwaja, et al., "This Time is Different," arXiv:2505.14766v2, 2025)
13. Toto achieves 12 percent CRPS improvement over Moirai on BOOM (0.375 vs 0.447); top position on GIFT-Eval; best on 8 of 12 Long Sequence Forecasting metrics. (Cohen, Khwaja, et al., "This Time is Different," arXiv:2505.14766v2, 2025)
14. Toto-Watchdog relationship at Q2 2026 is research proximity, not specified product integration; weights at huggingface.co/Datadog/Toto-Open-Base-1.0. (Datadog blog; huggingface.co/Datadog/Toto-Open-Base-1.0, accessed Q2 2026)
15. Bits AI SRE investigation workflow: signal assembly via shared tag keys, hypothesis generation, hypothesis testing against evidence. (Datadog documentation and press releases, accessed Q2 2026; Datadog DASH talk: "Bits AI SRE Your new teammate for on-call shifts," December 2, 2025)
16. MTTR claims are vendor-controlled case studies; Thomson Reuters and Fanatics provide additional triage efficiency evidence. (Datadog customer case studies; Thomson Reuters and Fanatics references, Datadog press release, December 2, 2025)
17. Per-monitor auto-investigation configuration available only through UI, not Terraform or IaC, as of May
18. Zero data retention prevents agent from accumulating customer-specific infrastructure knowledge across investigations. (Datadog Bits AI SRE documentation, accessed Q2 2026)
19. Bits AI Security Analyst GA April 2026 per release announcement. (Datadog, "This Month in Datadog," release announcement, 2026-04-29) [https://www.forrester.com/blogs/datadog-dash-a-revolving-door-of-operations-and-security-announcements/](https://www.forrester.com/blogs/datadog-dash-a-revolving-door-of-operations-and-security-announcements/)
20. Security Analyst SIEM triage time reduction of up to 98 percent. (Datadog Bits AI Security Analyst documentation and press release, accessed Q2 2026)
21. End-to-end Bits AI SRE investigation cannot be reconstructed as a single trace; Incident Management record, Slack message, and GitHub PR lack cross-referencing identifiers. (Datadog Bits AI SRE documentation and Incident Management documentation, accessed Q2 2026)
22. Closing the calibration loop requires structured verdict field, linkage record, aggregation layer, and queryable investigation persistence; none exist as standard products at Q2
23. Datadog training corpus for Bits AI SRE spans thousands of customer environments in pre-GA testing. (Datadog press release, December 2, 2025)
24. Kill-switch governance model: agent authority bounded by permitted output channels, human approval required for code changes. (Datadog Bits AI SRE documentation, accessed Q2 2026)
25. Datadog MCP Server queries by Claude Code are structurally analogous to Bits AI SRE queries during investigation. (Datadog MCP Server documentation, docs.datadoghq.com/bits_ai/mcp_server/, accessed Q2 2026)
26. CRPS is a proper scoring rule but not a human-readable explanation equivalent to statistical baseline deviation. (Cohen, Khwaja, et al., "This Time is Different," arXiv:2505.14766v2, 2025)
27. Closed-loop calibration requires three components built from Incident Management API exports, custom metrics, and postmortem tooling. (Analysis based on Datadog documentation, accessed Q2 2026)
28. Pomel and Lê-Quôc describe observability's core value as reducing friction of agreeing on system state during incidents. (Pomel and Lê-Quôc, "Datadog's Origin, AI," Datadog broadcast, 2026-03-26)
29. Lê-Quôc on speed and safety as co-requirements in autonomous agent deployment. (Lê-Quôc, "Fireside Chat with Datadog CTO and Kraken COO," Datadog DASH, 2026-03-19)

## Chapter 12: What Will Still Be True

1. Embedding drift incident at a mid-size financial services company, autumn
2. The Lindy effect formalized as a durability heuristic: expected remaining lifespan of a non-perishable idea is proportional to its current age. (Nassim Nicholas Taleb, *Antifragile: Things That Gain from Disorder*, Random House, 2012)
3. Honeycomb Query Assistant SLO design: 75 percent initial accuracy target, later raised to 80 percent, as an engineering commitment. (Phillip Carter, Honeycomb engineering blog)
4. The $47,000 multi-agent cost loop ran for hours before detection because alerting logic operated on aggregate cost cadence rather than per-session behavioral signals. (Teja Kusireddy, Medium, November 2025; Hacker News thread 45802430, November 2025)
5. Three of four Bits AI SRE configuration elements exist only as UI state at Q2 2026, outside infrastructure-as-code drift detection. (Datadog Bits AI SRE documentation, accessed Q2 2026)
6. Auto-instrumentation coverage changes on a cadence of weeks for ddtrace and months for OTel GenAI semantic conventions; Google ADK and Strands Agents gained coverage in the months preceding Q2
7. Datadog MCP Server implementation at Q2 2026; the MCP Server query itself is not a traced span. (Datadog documentation, "Datadog MCP Server," accessed Q2 2026)
8. LLM Observability billing mechanics: per-span billing unit, approximately $120 per day activation threshold, Sensitive Data Scanner allocation at 1 GB per 10,000 LLM spans, Flex Logs and Flex Frozen pricing tiers. (OpenObserve benchmark analysis, December 2025; Datadog billing documentation, accessed Q2 2026)
9. Toto architecture, training corpus, and benchmark results from May 2025 open-weights release under Apache 2.0 license; 12 percent CRPS improvement over Moirai on BOOM. (Cohen, Khwaja, et al., "This Time is Different: An Observability Perspective on Time Series Foundation Models," arXiv:2505.14766v2, 2025)
10. Bits AI SRE MTTR reduction of 70 percent at iFood and root-cause isolation in under four minutes at Energisa; vendor-controlled case studies. (Datadog customer case studies; Datadog press release, December 2, 2025)
11. Kleppmann's structural arguments on consistency tradeoffs, storage architecture, and write throughput versus read latency remain unrevised since 2017 because they derive from how storage systems work. (Martin Kleppmann, *Designing Data-Intensive Applications*, O'Reilly Media, 2017)
