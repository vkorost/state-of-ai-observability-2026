# In-Depth Analysis of OpenTelemetry Generative AI Semantic Conventions - Current State, Ecosystem Divergence, and Future Projections

## Section 1: What Is Settled

The OpenTelemetry Generative AI Semantic Conventions, as of v1.37 and the contemporary release cycles of Q2 2026, establish a unified infrastructure telemetry framework designed to normalize the operational footprint of Large Language Model transactions, agentic orchestrations, and external tool interactions. This specification provides engineering and platform teams with a standardized vocabulary across diverse AI workloads, enabling predictable collection of traces, metrics, and events. To prevent telemetry breaking changes across legacy environments, the specification relies on an explicit opt-in mechanism via the environment variable `OTEL_SEMCONV_STABILITY_OPT_IN=gen_ai_latest_experimental`, which commands compliant instrumentation libraries to emit the updated convention set while suppressing pre-v1.36.0 layouts.

### Standardized Span Attributes for Model Operations

The core specification enforces structural rigidity for operations directly interacting with foundation model services. These attributes capture the operational parameters of the request, model identifying signatures, execution parameters, performance boundaries, and token logistics.

| **Attribute Key**                          | **Value Type** | **Requirement Level**  | **Functional Description and Constraints**                                                                                            |
| ------------------------------------------ | -------------- | ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| `gen_ai.operation.name`                    | String         | Required               | Identifies the transaction type (e.g., `chat`, `generate_content`, `text_completion`, `embeddings`).                                  |
| `gen_ai.provider.name`                     | String         | Required               | Primary discriminator for the underlying AI infrastructure host or model provider. Replaces the deprecated `gen_ai.system` namespace. |
| `gen_ai.request.model`                     | String         | Conditionally Required | The explicit base or fine-tuned model name targeted by the client request (e.g., `gpt-4`).                                            |
| `gen_ai.response.model`                    | String         | Recommended            | The definitive version of the model that processed and fulfilled the generation request.                                              |
| `gen_ai.conversation.id`                   | String         | Conditionally Required | Unique thread identifier managing dialogue context, conversational state, and multi-turn correlation.                                 |
| `gen_ai.output.type`                       | String         | Conditionally Required | Captures the requested content format requested by the client (e.g., `text`, `json`, `image`).                                        |
| `gen_ai.request.temperature`               | Double         | Recommended            | Controls token selection randomness during generation.                                                                                |
| `gen_ai.request.top_p`                     | Double         | Recommended            | Governs nucleus sampling diversity thresholds.                                                                                        |
| `gen_ai.request.top_k`                     | Double         | Recommended            | Restricts token selection options to the top-k highest probabilities.                                                                 |
| `gen_ai.request.max_tokens`                | Integer        | Recommended            | Imposes upper ceilings on generated token sequences.                                                                                  |
| `gen_ai.request.seed`                      | Integer        | Conditionally Required | Numerical anchor to enforce reproducible deterministic sampling across requests.                                                      |
| `gen_ai.request.stream`                    | Boolean        | Conditionally Required | Tracks whether token generation utilizes server-sent event streams.                                                                   |
| `gen_ai.request.presence_penalty`          | Double         | Recommended            | Penalizes tokens based on their prior emergence in the text stream.                                                                   |
| `gen_ai.request.frequency_penalty`         | Double         | Recommended            | Penalizes tokens on a linear scale based on cumulative repetition.                                                                    |
| `gen_ai.request.stop_sequences`            | String Array   | Recommended            | Explicit literal limits instructing models to halt sequence construction.                                                             |
| `gen_ai.response.id`                       | String         | Recommended            | Server-side completion identifier issued by the executing provider.                                                                   |
| `gen_ai.response.finish_reasons`           | String Array   | Recommended            | Array reflecting token execution termination statuses (e.g., `["stop"]`, `["length"]`).                                               |
| `gen_ai.response.time_to_first_chunk`      | Double         | Recommended            | Captures time to initial token chunk in seconds from request issuance.                                                                |
| `gen_ai.usage.input_tokens`                | Integer        | Recommended            | Tracking input sequences. Replaces `prompt_tokens`.                                                                                   |
| `gen_ai.usage.output_tokens`               | Integer        | Recommended            | Tracking generated sequences. Replaces `completion_tokens`.                                                                           |
| `gen_ai.usage.reasoning.output_tokens`     | Integer        | Recommended            | Tracks output tokens consumed exclusively by internal model reasoning mechanisms.                                                     |
| `gen_ai.usage.cache_read.input_tokens`     | Integer        | Recommended            | Measures cached input tokens evaluated directly out of provider memory arrays.                                                        |
| `gen_ai.usage.cache_creation.input_tokens` | Integer        | Recommended            | Tracks input tokens committed into active provider cache arrays.                                                                      |
| `server.address`                           | String         | Recommended            | FQDN or IP endpoint destination handling the network transaction.                                                                     |
| `server.port`                              | Integer        | Conditionally Required | Target network socket port for the underlying infrastructure service.                                                                 |
| `error.type`                               | String         | Conditionally Required | Unified error class tracking rate limits, timeouts, or exceptions (e.g., `500`, `timeout`).                                           |
| `openai.request.service_tier`              | String         | Conditionally Required | Provider-specific attribute tracking requested service tier parameters.                                                               |
| `openai.response.service_tier`             | String         | Conditionally Required | Provider-specific attribute tracking used response service tier parameters.                                                           |
| `openai.api.type`                          | String         | Recommended            | Provider-specific attribute mapping the targeted endpoint flavor.                                                                     |

### Standardized Event Types

To prevent performance degradation on primary tracing spans from oversized text or multimodal structures, the specification isolates actual text payloads into the OpenTelemetry Event API. This structural decoupling allows high-volume production systems to manage large message arrays through discrete logging or event pipelines rather than overloading the distributed tracing mesh.

| **Standardized Event Type**                 | **Current Stability Status** | **Functional Purpose**                                                              |
| ------------------------------------------- | ---------------------------- | ----------------------------------------------------------------------------------- |
| `gen_ai.client.inference.operation.details` | Development / Experimental   | Captures structural context, chat histories, system instructions, and tool schemas. |
| `gen_ai.evaluation.result`                  | Development / Experimental   | Extracts automated evaluation marks, scores, and natural language explanations.     |

Within the primary inference event schema, specific nested attributes are explicitly standardized to capture raw operational values:

- `gen_ai.input.messages`: A deeply structured JSON array archiving prompt text, role designations, and historical message interactions in exact sequential order.

- `gen_ai.output.messages`: A structured payload detailing the exact text, images, or multimodal content blocks emitted back to client systems by the model.

- `gen_ai.system_instructions`: System prompts or baseline behavioral boundaries passed to the model independently of transactional history.

- `gen_ai.tool.definitions`: Structured schema definitions declaring what system tools were exposed to the model execution runtime.

### Standardized Span Kinds and Functional Contexts

The architectural topology of a Generative AI execution trace relies on standard OpenTelemetry `SpanKind` configurations combined with explicit `gen_ai.operation.name` attributes to classify transaction semantics. This approach ensures that downstream visualization systems can distinguish between network boundaries, agent loops, and programmatic tool execution.

| **Span Kind** | **Operation Name (gen_ai.operation.name)**                        | **Structural Target and Execution Role**                                                                        |
| ------------- | ----------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| `CLIENT`      | `chat` \| `generate_content` \| `text_completion` \| `embeddings` | Represents an external out-of-process RPC boundary to a managed foundation model service.                       |
| `INTERNAL`    | `chat` \| `generate_content`                                      | Applied when model inference is executed directly within the host process, such as via local weights.           |
| `CLIENT`      | `create_agent`                                                    | Describes remote initialization, registration, or creation parameters of a persistent agent instance.           |
| `INTERNAL`    | `invoke_agent`                                                    | Tracks the internal execution steps, localized decision loops, and reasoning blocks inside an active agent.     |
| `INTERNAL`    | `invoke_workflow`                                                 | Grouping container span reported by orchestration systems that direct multiple interconnected agent components. |
| `INTERNAL`    | `execute_tool`                                                    | Captures client-side or tool-side lifecycle boundaries where external systems fulfill calculated actions.       |

### Standardized Telemetry Metrics

Beyond individual traces, high-level operational health requires continuous aggregations via the OpenTelemetry Metrics API. These metrics enable platform teams to define Service Level Objectives around latency, token efficiency, and provider availability.

| **Metric Name**                                 | **Instrument Type** | **Unit**  | **Monitored Dimensions**                                                                                               |
| ----------------------------------------------- | ------------------- | --------- | ---------------------------------------------------------------------------------------------------------------------- |
| `gen_ai.client.token.usage`                     | Counter             | `{token}` | `gen_ai.operation.name`, `gen_ai.provider.name`, `gen_ai.token.type`, `gen_ai.request.model`, `gen_ai.response.model`. |
| `gen_ai.client.operation.duration`              | Histogram           | `s`       | `gen_ai.operation.name`, `gen_ai.provider.name`, `gen_ai.request.model`, `gen_ai.response.model`, `error.type`.        |
| `gen_ai.client.operation.time_to_first_chunk`   | Histogram           | `s`       | `gen_ai.operation.name`, `gen_ai.provider.name`, `gen_ai.request.model`, `gen_ai.response.model`.                      |
| `gen_ai.client.operation.time_per_output_chunk` | Histogram           | `s`       | `gen_ai.operation.name`, `gen_ai.provider.name`, `gen_ai.request.model`, `gen_ai.response.model`.                      |
| `gen_ai.server.request.duration`                | Histogram           | `s`       | `gen_ai.operation.name`, `gen_ai.provider.name`, `gen_ai.request.model`, `gen_ai.response.model`, `error.type`.        |
| `gen_ai.server.time_to_first_token`             | Histogram           | `s`       | `gen_ai.operation.name`, `gen_ai.provider.name`, `gen_ai.request.model`, `gen_ai.response.model`.                      |
| `gen_ai.server.time_per_output_token`           | Histogram           | `s`       | `gen_ai.operation.name`, `gen_ai.provider.name`, `gen_ai.request.model`, `gen_ai.response.model`.                      |

### Covered Providers and Frameworks

The semantic vocabulary incorporates closed-source commercial APIs, cloud-managed model routers, and open-weights execution engines. This is managed primarily via low-cardinality values explicitly supported within the `gen_ai.provider.name` attribute. Covered provider systems directly documented within the technology specs include `openai`, `anthropic`, `aws.bedrock`, `azure.ai.inference`, `azure.ai.openai`, `gcp.vertex_ai`, `gcp.gemini`, `gcp.gen_ai`, `deepseek`, `perplexity`, `cohere`, and `x_ai`.

At the software layer, frameworks like CrewAI natively adopt these semantic specifications directly into their source codebase. Concurrently, the larger ecosystem depends heavily on auto-instrumentation layers and translation SDKs, such as Arize’s OpenInference (supporting over 32 libraries) and Traceloop’s OpenLLMetry (supporting over 34 libraries), which actively map internal tracking structures directly into these standardized schemas.

## Section 2: What Is Still Contested or In Progress

As the specification continues to evolve, significant architectural shifts, operational debates, and legislative requirements have kept several areas highly fluid within the GenAI SIG.

### Standalone Repository Migration and Governance Churn

The most noticeable operational shift is the physical extraction of GenAI semantic conventions from the core OpenTelemetry repository. To bypass the review queues and engineering bandwidth bottlenecks of the primary project, the maintainers instituted a dedicated repository: `open-telemetry/semantic-conventions-genai`. Consequently, an active migration effort is underway to move existing `gen-ai` labeled issues and open Pull Requests from the main repository into this new workspace. This split creates temporary alignment challenges for contributors navigating dual repositories.

### Topology and Hierarchical Conflicts in Agentic Workflows

While basic operations are stable, modeling autonomous, collaborative, or multi-agent environments remains highly contested. Meta-issue `#2664` outlines a broad taxonomy categorizing AI Agent topologies into six relational structures. The underlying debate within the SIG centers on how to mathematically model these structures inside standard distributed tracing limits without generating unbounded span depths or parent-child loop cycles. Key areas of contention include:

- **The Strategy Planning Gap:** Community feedback highlights a critical missing layer between a structural Task (what must be accomplished) and an Action (the execution step). There is no standardized convention to capture "planning strategy blocks"—the phase where an agent algorithmically decides the execution sequence of tool calls and sub-tasks.

- **Session Boundaries vs. Conversational Boundaries:** Issue `#2883` focuses on resolving conflicts between a user dialogue line and a multi-agent boundary. A single user interaction might trigger multiple distinct multi-agent execution tracks. The group is evaluating the introduction of a new `session.id` attribute to sit strictly above `gen_ai.conversation.id`. This approach establishes a clear three-tier semantic hierarchy:

$$\text{session.id} \longrightarrow \text{gen\_ai.conversation.id} \longrightarrow \text{individual span layers}$$

- **The User Perspective Entry Span:** Issue `#3418` proposes adding a user-centric entry span (`gen_ai.operation.name = "enter"`). Proponents argue that existing internal tracking (such as `invoke_workflow` or `chat`) fails to capture performance metrics from an end-user viewpoint. Opponents express concern that introducing abstract, non-code-mapped spans complicates auto-instrumentation rules, requiring manual instrumentation intervention instead.

### Payload Handling, Privacy Controls, and Lifecycle Realignment

The decision to isolate prompt and completion strings into separate OTel Events remains highly controversial. Issue `#2010` outlines a push by several observability backend vendors to re-litigate this choice. Prompts represent input parameters available at initialization, whereas completions are stream-buffered objects received non-deterministically at the end of the transaction lifecycle. Moving content to separate events removes spatial and temporal locality from the primary trace span, which complicates backend processing and inline sampling. Issues `#1621` and `#1964` deal with chunk-level event storms vs block buffering. Privacy scrubbing is entirely outside the standard.

### Evaluation Metrics and Global Safety Overlays

While standard client operational durations and token counters are finalized, logging evaluation parameters remains an ongoing area of design work. A major initiative involves defining standard metrics for model quality, such as hallucination indicators, answer correctness, and groundedness scoring. Disagreements exist regarding whether these derived KPIs should be managed as custom runtime histograms (e.g., `gen_ai.response.quality`) or standardized directly as explicit span metrics.

Furthermore, external legislative changes have accelerated the need for new safety-specific conventions. Issue `#3356` outlines a proposal to introduce provider-side safety telemetry to comply with the enforcement of the EU AI Act. This proposal aims to standardize logging for safety classifier evaluations, response modifications, and abstention actions using specialized fields :

```
gen_ai.safety.evaluation_performed (Boolean)
gen_ai.response.modification_type  (Enum vs. String Debate)
gen_ai.confidence.*                 (Provider-Specific vs. Universal Schema)
```

The core debate centers on whether these compliance metrics belong on operational spans or separate compliance events.

## Section 3: What Datadog Implements vs. The Standard

Datadog’s native ingestion framework allows enterprise teams to route OpenTelemetry GenAI spans directly to Datadog LLM Observability backends via standard OTLP conduits without utilizing the localized `ddtrace` instrumentation libraries. However, achieving full compatibility requires understanding specific schema alignments, proprietary fallbacks, and physical data processing limitations.

### Schema Alignment and Attribute Mapping Matrix

When OpenTelemetry GenAI v1.37+ telemetry hits the Datadog intake endpoint, an automatic mapping layer translates standard fields into native Datadog LLM Observability schema representations.

| **OpenTelemetry OTLP Input Attribute**            | **Datadog Native LLM Observability Target Field** | **Data Processing and Contextual Handling**                     |
| ------------------------------------------------- | ------------------------------------------------- | --------------------------------------------------------------- |
| `gen_ai.provider.name`                            | Model Provider Field                              | Maps the active vendor hosting destination.                     |
| `gen_ai.response.model` \| `gen_ai.request.model` | `meta.model_name`                                 | Resolves target execution model identities.                     |
| `gen_ai.operation.name`                           | `span.kind` / Operation Type                      | Maps the trace role (e.g., chat operations translate to `llm`). |
| `gen_ai.conversation.id`                          | `session_id`                                      | Populates Datadog’s session tracking UI and appends to tags.    |
| `gen_ai.response.finish_reasons`                  | `metadata.finish_reasons`                         | Captures sequence termination codes directly.                   |
| `gen_ai.tool.name`                                | `name`                                            | Overrides the generic span name to identify the specific tool.  |
| `gen_ai.tool.call.id`                             | `metadata.tool_id`                                | Links execution context to unique tool call identifiers.        |
| `gen_ai.tool.description`                         | `metadata.tool_description`                       | Ingests the baseline documentation string of the target tool.   |
| `gen_ai.tool.type`                                | `metadata.tool_type`                              | Resolves execution architecture parameters.                     |
| `gen_ai.tool.definitions`                         | `meta.tool_definitions`                           | Parses the system tool capabilities payload as a JSON array.    |
| `gen_ai.tool.call.arguments`                      | `input.value`                                     | Maps tool input parameters into the functional trace.           |
| `gen_ai.tool.call.result`                         | `output.value`                                    | Captures the output or return string of the tool transaction.   |

### Conversational Payload Extraction Hierarchies

To extract prompt and completion content strings, Datadog implements a clear extraction priority model. The intake engine first checks for direct span attributes, evaluating `gen_ai.input.messages`, `gen_ai.output.messages`, and `gen_ai.system_instructions`. If these are missing, it falls back to parsing associated OTel span events named `gen_ai.client.inference.operation.details`.

For embedding-specific spans, the engine maps `gen_ai.input.messages` to `meta.input.documents`, while hardcoding `meta.output.value` to a static confirmation string: `[N embedding(s) returned]`.

### Operational Fallbacks for Alternative Schemas

To maintain broad compatibility across fragmented ecosystems, Datadog provides legacy fallback processing for alternative instrumentation schemas, such as OpenLLMetry. If an incoming span lacks the standard `gen_ai.operation.name` attribute, the intake parser inspects the legacy `llm.request.type` field to resolve the target backend span type :

$$\text{chat} \parallel \text{completion} \longrightarrow \text{"llm"}$$

$$\text{embedding} \longrightarrow \text{"embedding"}$$

$$\text{rerank} \parallel \text{unknown} \longrightarrow \text{"workflow"}$$

### Practical Limitations of Native OTLP Ingestion

Deploying an architecture that relies on native OTLP ingestion without the `ddtrace` agent presents several design limitations and risks :

- **The 256-Character Tag Truncation Ceiling:** Any non-standard or extended `gen_ai.*` attribute that is not explicitly defined in Datadog's core mapping table falls back to a generic span tag. Datadog enforces a strict **256-character maximum limit per value** on standard tags. Consequently, custom metadata arrays or large unstructured parameters are permanently truncated upon ingestion, destroying JSON formatting or long context blocks.

- **The Custom Attribute Filtration Drop:** The ingestion engine converts basic scalar metadata tags into generic metrics, but filters out certain system namespaces (e.g., `_dd.*`, `llm.*`, `ddtags`). Crucially, **all other non-mapped custom attributes are completely dropped**, preventing the use of arbitrary application context tags unless they precisely match the standard specification.

- **Cross-Pipeline Telemetry Leakage and Access Gaps:** OpenTelemetry traces routed via standard OTLP destinations can simultaneously write records to Datadog's general APM Trace Explorer databases. This dual ingestion presents security risks if the target payloads contain PII or sensitive training data. To prevent unauthorized viewing across teams, administrators must manually configure a separate "Restricted Dataset" policy within the APM interface to align access permissions with LLM Observability constraints.

- **ID Format Mismatches in External Evaluations:** OpenTelemetry manages trace and span identifiers natively as hexadecimal string representations. However, Datadog’s external evaluations HTTP API requires numeric identifiers submitted as decimal strings. Engineers must implement custom mathematical conversion logic within their evaluation applications—such as Python's `int(hex_id, 16)`—to successfully connect external evaluations with ingested OTel spans.

## Section 4: What Is Coming

The OpenTelemetry GenAI instrumentation roadmap focuses on stabilizing core infrastructure telemetry, formalizing multi-agent workflows, and expanding domain-specific protocol integrations.

### SIG Roadmap and Stability Milestones

The primary focus for the GenAI SIG is moving core span and event attributes out of experimental tracking and into a finalized stable release within the new `semantic-conventions-genai` repository. This milestone aims to deprecate the requirement for explicit stability opt-in environment overrides, such as `OTEL_SEMCONV_STABILITY_OPT_IN=gen_ai_latest_experimental`. Stabilizing these definitions ensures that downstream analytics platforms, visual metric backends, and collector processors can assume consistent data structures without risking breaking changes from minor version updates.

### Architectural Progress on Agentic Topologies

Driven by the meta-framework structures introduced in proposal `#2664`, the SIG is actively splitting the broad agentic schema into targeted sub-issues and dedicated pull requests. Work is focused on defining specific attribute sub-families to provide standard out-of-the-box support for recursive tool calls and multi-agent systems :

- `gen_ai.task.*`: Standardizes the structural representation of multi-step task and goal decompositions.

- `gen_ai.action.*`: Manages fine-grained execution metrics around non-deterministic execution paths.

- `gen_ai.agent.skills.*`: Issue `#2686` focuses specifically on standardizing how localized capability arrays and skills are registered and observed within an active runtime.

- `gen_ai.team.*`: Standardizes communication metrics and role distributions across collaborative multi-agent groups.

- `gen_ai.artifact.*` and `gen_ai.memory.*`: Establishes schemas to track data continuity, prompt mutations, and long-term storage retrieval across long-running sessions.

### Model Context Protocol Integration

The integration of Anthropic’s Model Context Protocol (MCP) represents a major advancement for domain-specific telemetry within the GenAI specification. MCP operates over JSON-RPC layers to establish standard communication channels between models, development tools, and external data sources. Because multiple internal multiplexed JSON-RPC messages are frequently transferred across a single persistent transport connection, traditional HTTP or generic RPC telemetry tracking fails to capture these nested interactions.

To address this visibility gap, the specification introduces explicit domain-specific metrics and attributes for tracking MCP performance :

$$\text{mcp.client.operation.duration} \quad \text{(Histogram measuring operational latency)}$$

$$\text{mcp.server.operation.duration} \quad \text{(Histogram measuring server execution latency)}$$

$$\text{mcp.client.session.duration} \quad \text{(Tracks overall client connection lifespan)}$$

$$\text{mcp.server.session.duration} \quad \text{(Tracks overall server connection lifespan)}$$

The specification requires instrumentation layers to propagate trace context parameters directly inside the JSON-RPC request dictionary block. To unify tool execution tracking across ecosystems, the specification enforces explicit cross-compatibility alignments :

```
mcp.protocol.version  (Captures the specific active protocol specification string)
mcp.session.id        (Identifies the individual structural session container)
gen_ai.operation.name (Enforced strictly to "execute_tool" for tool call methods)
```

This alignment ensures that downstream observability platforms can evaluate and display MCP tool transactions using the same standard visual templates applied to traditional GenAI tool tracking.
