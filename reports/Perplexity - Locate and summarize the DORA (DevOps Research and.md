<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" style="height:64px;margin-right:32px"/>

# Locate and summarize the DORA (DevOps Research and Assessment)

2025 State of DevOps Report findings specifically related to AI
integration in software delivery. If the 2025 report is not yet
published, use the most recent available edition plus any
supplementary DORA research published in 2025.

Provide:

1. The report's key findings on AI tool adoption (coding
assistants, AI-assisted testing, AI in CI/CD)
2. Any findings on how AI tool adoption correlates with DORA
metrics (deployment frequency, lead time for changes,
change failure rate, time to restore service)
3. Any findings on production incident rates in organizations
with high AI tool adoption vs. low adoption
4. Any findings specific to observability practices in
AI-adopting organizations
5. Whether the report addresses AI-generated code quality
or production reliability

Also identify any other credible industry surveys or research
reports from 2024-2026 that contain quantitative data on AI
production reliability, incident rates, or observability
maturity specifically in the context of AI system deployment.
Include the Pragmatic Engineer, Honeycomb, or similar practitioner
surveys if they contain relevant quantitative findings.

DORA has not yet published a 2025 “Accelerate State of DevOps” report, but it has released a dedicated 2025 **State of AI‑Assisted Software Development** report plus the 2024 **Accelerate State of DevOps** report and a 2026 **ROI of AI‑Assisted Software Development** paper; together these cover AI integration and its impact on DORA metrics and reliability.[^1][^2][^3][^4]

Below I’ll summarize what these DORA sources say, then list other 2024–2026 industry surveys with quantitative findings on AI reliability and observability.

***

## DORA reports and scope

- The **2024 Accelerate State of DevOps report** introduces AI as a major theme and explicitly analyzes how AI adoption affects software delivery performance (throughput and stability, i.e., the DORA metrics).[^5][^2]
- The **2025 State of AI‑Assisted Software Development** report focuses entirely on AI tools (coding assistants, AI in IDEs, etc.) and treats AI as an “amplifier” of existing strengths or weaknesses rather than a standalone performance booster.[^3][^6][^1]
- The **2026 “ROI of AI‑Assisted Software Development”** follow‑up uses the 2025 findings plus financial modeling to estimate how AI affects DORA metrics and downtime cost (the “instability tax”).[^4]

Publicly available material is mostly narrative and high‑level; the detailed regression tables and raw metrics sit behind download forms, so what follows is based on official summaries plus practitioner analyses that quote the reports.[^7][^8][^9][^10][^6][^5][^4]

***

## 1. DORA findings on AI tool adoption

### Adoption level and use cases

- DORA’s 2025 AI report and Scrum.org’s summary say **about 90% of developers now use AI daily**, primarily via autocomplete, chat‑based problem solving, and code suggestions.[^6]
- The 2024 AI preview notes a **majority of respondents rely on AI** for tasks such as code explanation, documentation, writing code, and code optimization, confirming steady adoption growth over the prior year.[^11]
- A 2025 blog summarizing the 2024 DORA data reports that **over 75% of respondents rely on AI for at least one daily professional task**, again with writing code, summarizing information, and explaining code as the dominant use cases.[^7]


### Where AI shows up in the toolchain

- DORA finds AI is most prevalent **inside IDEs and internal web interfaces**, suggesting organizations are embedding AI where developers already work rather than as separate pipeline steps.[^11]
- Common uses include **writing and modifying code, debugging, explaining code, and generating tests**, while more “up‑stream” uses (requirements analysis, planning, architecture insights) remain less common.[^6]
- Roughly **half of respondents report they do not yet interact with AI as an automated part of their toolchain** (e.g., fully integrated CI/CD or automated code review), implying that AI in CI/CD is emerging but not yet universal.[^11]

Overall, DORA’s 2024–2025 work portrays AI primarily as **developer‑centric tooling (coding assistants, AI test generation, code review help)** with early but uneven integration into CI/CD and release automation.[^8][^7][^6][^11]

***

## 2. Correlation between AI adoption and DORA metrics

DORA clusters the four key metrics into two composites: **throughput** (deployment frequency, lead time for changes) and **stability** (change failure rate, time to restore service).[^5]

### Positive effects: individual productivity and local quality

Across 2024–2025, DORA consistently reports that higher AI adoption is associated with **better individual‑level outcomes**:

- The 2024 report states that AI adoption **“significantly increases individual productivity, flow, and job satisfaction.”**[^2]
- A causal analysis summarized by CUSY (based on the 2024 report) finds that a **25% increase in AI adoption** is associated with approximately:
    - **7.5% increase in documentation quality**
    - **3.4% increase in code quality**
    - **3.1% increase in code review speed**[^7]
- The 2025 AI report summary and analyses echo that AI improves developer effectiveness and “developer experience,” especially when coupled with good internal platforms and clean data.[^1][^3][^4][^6]


### Negative effects: delivery throughput and stability

However, DORA also finds **non‑intuitive or negative correlations with the delivery metrics themselves**:

- The official 2024 report explicitly concludes: **AI adoption increases individual productivity but hurts software delivery performance**, reducing both throughput and stability when fundamentals like small batch sizes and robust testing are not in place.[^9][^2][^5]
- The CUSY causal‑inference write‑up quantifies this as an estimated **1.5% decrease in delivery throughput** and **7.2% decrease in delivery stability** for the same 25% uplift in AI adoption, even as documentation and code quality indicators improve.[^7]
- DORA’s 2024 AI preview notes that AI adoption affects “productivity, flow, documentation quality, job satisfaction, time spent doing creative work, and **delivery stability**,” again implying a trade‑off between local gains and system stability.[^11]
- Practitioner commentary on the 2025 AI report (Scrum.org, LinkedIn) underscores the same point: **AI increases throughput but also increases instability**, especially for teams with weak practices, summarised as “speed without stability is just accelerated chaos.”[^10][^12][^6]


### How this maps to the four DORA metrics

Public DORA materials rarely publish per‑metric coefficients, but they consistently treat:

- **Throughput** as a composite of **deployment frequency and lead time**, and
- **Stability** as a composite of **change failure rate and time to restore service**.[^5]

Given DORA’s statements that AI adoption **reduces throughput and stability**, the direction of effect is:

- **Deployment frequency / lead time**: on average, AI‑heavy teams tend to show **slightly worse throughput** (fewer deploys or longer lead times) unless they have strong platform, CI, and value‑stream practices.[^2][^4][^6][^7]
- **Change failure rate / time to restore**: AI adoption correlates with **higher instability**, i.e., more failed changes and/or slower recovery, again unless mitigated by strong testing, small batches, and automation.[^10][^4][^2][^6][^7]

Crucially, the 2025 AI report frames AI as an **amplifier**: **high‑performing teams see gains, while struggling teams see their problems magnified**, so these negative averages hide significant variance by maturity level.[^3][^4][^1][^6]

***

## 3. Production incident rates with high vs. low AI adoption

DORA has *not* publicly released a simple table of “incident rates by AI adoption quartile,” but several clues connect AI usage to higher failure/incident risk:

- The 2024 Accelerate report explicitly says AI **negatively impacts delivery stability**, which is largely driven by **change failure rate and time to restore**—both proxies for production incidents.[^2][^5]
- The 2026 ROI paper, building on 2025 data, models an **“instability tax”**: in its example, AI adoption is associated with a **rise in change failure rate from 5% to 6%**, producing a modeled **negative downtime impact of about \$344k** in the first year for a 500‑engineer org, even though overall ROI remains positive.[^4]
- Commentaries on the 2025 AI report emphasize that **teams get faster and also break things more often**, and that many organizations “don’t understand why” volatility and instability are rising.[^12][^10][^6]

External (non‑DORA) data point in a similar direction:

- A LinkedIn post summarizing a Uplevel study (cited alongside DORA 2024) notes that teams with GitHub Copilot access saw **no significant improvement in PR cycle time but a 41% increase in bug rate**, suggesting higher defect introduction despite similar throughput.[^9]

Putting this together: **DORA evidence supports that high AI‑adoption cohorts experience higher change failure and more volatile production outcomes on average than low‑adoption cohorts, unless they invest heavily in testing, CI/CD, and small batch practices.**[^10][^4][^6][^2][^7]
Precise incident‑rate deltas by adoption band are not published in the open summaries.

***

## 4. Observability practices in AI‑adopting organizations (DORA + others)

DORA itself talks more about **foundational practices** than about specific observability tools, but observability shows up implicitly as part of the stability story and is treated as a prerequisite for safe AI adoption:

- The 2024 report warns that AI and platform engineering can hurt stability if fundamentals such as **robust testing and small batch sizes** are missing, which in practice includes adequate CI/CD and observability to detect/regress incidents quickly.[^5][^2][^7]
- The 2026 ROI report recommends counter‑investments in **automated testing, continuous integration, and working in small batches** explicitly to offset the instability tax from faster AI‑driven code production, implying that organizations need sufficient observability to make these investments effective.[^4]
- The 2025 AI Capabilities Model (as summarized by Scrum.org) lists **high‑quality internal platforms, clean/accessible data, and a strong focus on DevEx and feedback loops** as prerequisites for reaping AI benefits; in practice, these capabilities often embed observability for fast feedback and incident learning.[^1][^3][^6]

Other surveys give more direct quantitative links between **observability maturity, AI features, and reliability**:

- **ManageEngine “State of Observability 2025”** (1,240 respondents) reports that:
    - 64.7% of organizations achieved **≥50% reduction in MTTR** after adopting observability.[^13]
    - 81% report **≥100% ROI** from observability tools.[^13]
    - Organizations with more reliable AI/ML features in their observability tools are **4.9× more likely** to achieve a **90% MTTR reduction**, **3.7× higher productivity gains**, and **2.8× more likely** to exceed **150% ROI**, strongly linking AI‑powered observability to incident response performance.[^13]
- **Grafana Observability Survey 2026** (1,363 respondents) finds:
    - Roughly **9 in 10 respondents see value** in AI for forecasting, root cause analysis, onboarding, and generating dashboards/alerts.[^14][^15]
    - **77% see value** in AI taking autonomous actions but with significant skepticism; **95% say AI must “show its work”** (explain reasoning) to be trusted for operations.[^15][^14]
    - **57% report implementing observability for LLM‑based applications** (“LLM app observability”) in at least investigating/POC/production stages.[^14]
    - **77% say centralized observability has saved time or money**, with verbatim examples of MTTR dropping from hours to minutes and major outage costs avoided.[^14]
- **Dynatrace “State of Observability 2025: Unlocking AI Trust and ROI”** reports:
    - **100% of surveyed organizations use AI in some capacity**, with observability increasingly used as the “control plane” for AI transformation.[^16]
    - **70% increased observability budgets this year**, and **75% plan to increase again**, often to manage AI‑related risk.[^16]
    - AI capabilities are now the \#1 criterion (29%) for selecting an observability platform, surpassing cloud compatibility.[^16]
    - Despite this, humans still **verify 69% of AI‑driven decisions**, and **70% of organizations increased budgets for “trust and transparency” initiatives**, underscoring ongoing concerns about AI reliability.[^16]

Together, these paint a picture where **AI‑heavy organizations are rapidly upgrading observability (often with AI‑assisted features) to manage the extra instability that DORA associates with AI‑driven throughput increases.**[^2][^14][^13][^4][^7][^16]

***

## 5. DORA on AI‑generated code quality and production reliability

DORA distinguishes between **local code quality** and **system‑level reliability**:

- As noted earlier, the 2024 causal analysis finds that increased AI adoption is correlated with **higher documentation quality and better self‑reported code quality**, plus faster code review.[^7]
- The 2025 AI report summary (via Scrum.org) says **59% of teams report improved code quality with AI**, 10% say quality worsened, and about 30% are unsure or don’t fully trust AI output, reflecting mixed perceptions.[^6]
- The 2024 AI preview shows **only 24% of developers say they trust AI‑generated code “a lot” or “a great deal”**, indicating substantial skepticism even when quality is perceived as improved.[^11]
- Practitioner commentary stresses that **AI “doesn’t replace code review; it makes code review more critical,”** because AI tends to produce confident but sometimes subtly incorrect code.[^8][^6]

At the same time, DORA and related analyses are clear that **system‑level reliability can deteriorate even when local code quality improves**:

- The 2024 report and 2025 commentary state that AI **“negatively impacts software delivery stability and throughput”**, a finding repeated in 2025 analyses that describe AI as increasing throughput *and* instability.[^10][^6][^5][^2][^7]
- The 2026 ROI report formalizes this as an **“instability tax”**—more failures and downtime cost when pipelines and governance are not upgraded to cope with increased code volume, despite net positive ROI.[^4]

Non‑DORA evidence amplifies this concern:

- The Uplevel Copilot study cited in a 2024 LinkedIn post reports **no improvement in PR cycle time but a 41% increase in bug rate** for teams with Copilot access, suggesting that AI‑generated code can degrade production reliability if verification is not scaled.[^9]

So, DORA’s position is essentially:

> **AI‑generated code can be as good or better at the unit level, but unless you redesign testing, CI/CD, and observability, the net effect on production reliability is often negative.**[^6][^2][^4][^7]

***

## Other 2024–2026 surveys on AI reliability, incidents, and observability

Below are key non‑DORA studies with quantitative findings relevant to AI in production, incident rates, or observability maturity.

### Selected reports (2024–2026)

| Report | Year | Scope \& sample | AI / reliability / observability findings (public) |
| :-- | :-- | :-- | :-- |
| **DZone + Honeycomb “Observability \& Performance Trend Report”** | 2024 | Community survey on observability maturity and production “excellence” | Concludes that advanced observability, SRE practices, and shared ownership correlate with better release cadence, incident response, and resilient systems; framed as “observability enables production excellence,” though AI‑specific stats are limited in the public summary. [^17] |
| **ManageEngine “State of Observability 2025”** | 2025 | 1,240 IT leaders/practitioners across ~75 countries | 64.7% report ≥50% MTTR reduction; 81% report ≥100% ROI from observability; organizations with more reliable AI/ML features in their tools are 4.9× more likely to get 90% MTTR reduction and 2.8× more likely to exceed 150% ROI, tying AI‑powered observability directly to incident performance. [^13] |
| **Grafana “Observability Survey” (4th annual)** | 2026 | 1,363 respondents from 76 countries | ~90% see AI as valuable for forecasting, root‑cause, onboarding, and generating dashboards/alerts; 77% see value in autonomous actions but 95% insist AI must explain its reasoning; 57% are implementing observability for LLM‑based apps; 77% say centralized observability has saved time or money and report examples of dramatic MTTR reduction. [^14][^15] |
| **Dynatrace “State of Observability 2025: Unlocking AI Trust and ROI”** | 2025 | Global exec/tech‑leader survey | 100% of orgs use AI in some capacity; 70% increased observability budgets this year and 75% plan to do so again; AI capabilities are now the \#1 criterion (29%) for observability platform selection; humans verify 69% of AI‑driven decisions and 70% increased budgets for “trust and transparency,” underlining reliability concerns. [^16] |
| **Pragmatic Engineer “AI tooling for software engineers” (2024) \& “2025 Survey”** | 2024–2025 | ≈3,000+ engineers, mostly mid‑senior | 2025 tech‑stack survey: 85% of respondents mention at least one AI tool; only ~4% explicitly say they do not use AI tools, showing near‑universal adoption; however, these surveys focus on **tool usage and sentiment**, not quantitative production reliability or incident‑rate data. [^18][^19] |
| **Honeycomb \& DZone Observability research** | 2020–2024 | Community surveys | Earlier Honeycomb work (often cited in 2024 materials) argues that advanced observability and SRE culture reduce MTTR, improve release cadence, and improve “production excellence,” but public write‑ups don’t yet separate AI vs non‑AI systems quantitatively. [^17] |
| **McKinsey “State of AI Trust in 2026”** | 2026 | Executive survey on AI trust maturity | Finds progress in AI trust maturity but persistent gaps in strategy, governance, and risk management; focuses more on governance and compliance than operations, with limited direct data on production incident rates. [^20] |

So far, **DORA’s AI‑focused research plus observability‑vendor surveys (Grafana, Dynatrace, ManageEngine, Honeycomb)** are the main sources combining AI adoption, reliability concerns, and observability maturity; **Pragmatic Engineer’s surveys** are excellent for understanding practitioner AI adoption and tool choices, but they don’t yet provide quantitative incident‑rate or reliability metrics.[^17][^18][^19][^14][^13][^2][^4][^16][^7]

If you’d like, I can turn this into a short internal briefing or slide deck focused specifically on: (a) what DORA implies for your AI roll‑out, and (b) which observability investments most directly mitigate the instability tax.
<span style="display:none">[^21][^22][^23][^24][^25][^26][^27][^28][^29][^30]</span>

<div align="center">⁂</div>

[^1]: https://research.google/pubs/dora-2025-state-of-ai-assisted-software-development-report/

[^2]: https://dora.dev/research/2024/dora-report/

[^3]: https://dora.dev/research/2025/dora-report/

[^4]: https://www.infoq.com/news/2026/05/dora-roi-ai-assisted-dev-report/

[^5]: https://www.mezmo.com/blog/key-takeaways-from-the-2024-dora-report

[^6]: https://www.scrum.org/resources/blog/dora-report-2025-summary-state-ai-assisted-software-development

[^7]: https://cusy.io/en/blog/dora-report-2024.html

[^8]: https://middlewarehq.com/blog/how-ai-is-reshaping-software-development-insights-from-the-2024-dora-report

[^9]: https://www.linkedin.com/posts/mike-fisher-3317a8_the-ai-trap-activity-7275155392916066305-sdTz

[^10]: https://www.linkedin.com/posts/yyemini_google-clouds-2025-dora-report-just-came-activity-7386451003941785600-3Dt9

[^11]: https://dora.dev/research/2024/ai-preview/

[^12]: https://www.linkedin.com/posts/robertbowley_reflections-on-the-latest-dora-state-of-ai-assisted-activity-7377248227751899136-n3h4

[^13]: https://download.manageengine.com/it-operations-management/pdf/State-of-observability-2025-report.pdf

[^14]: https://grafana.com/observability-survey/

[^15]: https://www.youtube.com/watch?v=oPgL9_9dhl8

[^16]: https://www.dynatrace.com/news/blog/state-of-observability-2025-ai-trust-roi/

[^17]: https://www.honeycomb.io/resources/whitepapers/observability-maturity-findings-2020-thankyou

[^18]: https://newsletter.pragmaticengineer.com/p/the-pragmatic-engineer-2025-survey

[^19]: https://newsletter.pragmaticengineer.com/p/the-pragmatic-engineer-2025-survey-part-3

[^20]: https://www.mckinsey.com/capabilities/tech-and-ai/our-insights/tech-forward/state-of-ai-trust-in-2026-shifting-to-the-agentic-era

[^21]: https://www.artiquare.com/pragmatic-engineer-survey-exposes-failure-of-first-wave-ai/

[^22]: https://finance.yahoo.com/news/honeycomb-advances-observability-ai-powered-130000550.html

[^23]: https://cloud.google.com/resources/content/2025-dora-ai-assisted-software-development-report

[^24]: https://blog.pragmaticengineer.com/ai-coding-tools-explosion/

[^25]: https://www.linkedin.com/posts/jacob-conger-9238444a_observability-is-being-rebuilt-for-the-activity-7374468679373332480-o8pv

[^26]: https://www.reddit.com/r/EngineeringManagers/comments/1t566bq/dora_metrics_are_lying_to_you_and_ai_is_making_it/

[^27]: https://www.linkedin.com/posts/thestevemitchell_the-pragmatic-engineer-released-their-2025-activity-7356345883732373506-0-8B

[^28]: https://itbrief.com.au/story/ai-cost-pressures-reshape-observability-in-new-survey

[^29]: https://www.apmdigest.com/honeycomb-unveils-kubernetes-aware-observability-to-solve-application-performance-mysteries

[^30]: https://www.youtube.com/watch?v=DIBzCc6sE9M

