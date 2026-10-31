# Scalable Inference Serving

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

A collection of APIs, frameworks, and platforms for scalable machine learning model inference serving, deployment, and management. This includes the KServe Open Inference Protocol (the CNCF standard for model serving on Kubernetes), BentoML (developer packaging and serving), vLLM (high-throughput LLM inference), NVIDIA Triton Inference Server, and supporting observability and registry tools. KServe recently joined CNCF as an incubating project (November 2025).

**Areas:** Artificial Intelligence · CNCF · Deployment · Inference · Kubernetes · LLM · Machine Learning · Model Serving · MLOps · Scalability

## Scalable Inference Serving on APIs.io

Everything profiled for Scalable Inference Serving is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/scalable-inference-serving/](https://apis.io/providers/scalable-inference-serving/)** — or go straight to one of the APIs or properties below.

### APIs (9)

- [BentoML REST API](https://apis.io/apis/scalable-inference-serving/bentoml-rest-api/) — BentoML is an open-source unified inference platform for deploying and scaling AI models. It auto-generates RESTful APIs from Python service definitions,…
- [vLLM OpenAI-Compatible API](https://apis.io/apis/scalable-inference-serving/vllm-openai-compatible-api/) — vLLM is a high-throughput and memory-efficient inference engine for LLMs, implementing PagedAttention for efficient KV cache management. vLLM exposes an…
- [NVIDIA Triton Inference Server HTTP API](https://apis.io/apis/scalable-inference-serving/nvidia-triton-inference-server-http-api/) — NVIDIA Triton Inference Server is an open-source inference serving software that implements the KServe Open Inference Protocol (V2). Supports TensorRT,…
- [MLflow Model Registry REST API](https://apis.io/apis/scalable-inference-serving/mlflow-model-registry-rest-api/) — MLflow is an open source platform for managing the ML lifecycle, including experiment tracking, reproducibility, and deployment. The MLflow REST API manages…
- [Ray Serve REST API](https://apis.io/apis/scalable-inference-serving/ray-serve-rest-api/) — Ray Serve is a scalable model serving library built on Ray, designed for building online inference APIs. Supports composable deployments, autoscaling, HTTP…
- [Scalable Inference Serving Health API](https://apis.io/apis/scalable-inference-serving/scalable-inference-serving-health-api/) — Server and model liveness and readiness probes
- [Scalable Inference Serving Inference API](https://apis.io/apis/scalable-inference-serving/scalable-inference-serving-inference-api/) — Model inference request endpoints
- [Scalable Inference Serving Metadata API](https://apis.io/apis/scalable-inference-serving/scalable-inference-serving-metadata-api/) — Server and model metadata endpoints
- [Scalable Inference Serving Models API](https://apis.io/apis/scalable-inference-serving/scalable-inference-serving-models-api/) — Model management and metadata operations

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Scalable Inference Serving Agentic Access](https://apis.io/agentic-access/scalable-inference-serving/scalable-inference-serving-agentic-access/)

#### JSON Schema (15)

The data models the API reads and writes.

- [Inference Request](https://apis.io/schemas/scalable-inference-serving/kserve-inference-request/)
- [Model Metadata](https://apis.io/schemas/scalable-inference-serving/kserve-model-metadata/)
- [ErrorResponse](https://apis.io/schemas/scalable-inference-serving/scalable-inference-serving-errorresponse/)
- [InferenceRequest](https://apis.io/schemas/scalable-inference-serving/scalable-inference-serving-inferencerequest/)
- [InferenceResponse](https://apis.io/schemas/scalable-inference-serving/scalable-inference-serving-inferenceresponse/)
- [ModelMetadataResponse](https://apis.io/schemas/scalable-inference-serving/scalable-inference-serving-modelmetadataresponse/)
- [ModelReadyResponse](https://apis.io/schemas/scalable-inference-serving/scalable-inference-serving-modelreadyresponse/)
- [RequestInput](https://apis.io/schemas/scalable-inference-serving/scalable-inference-serving-requestinput/)
- [RequestOutput](https://apis.io/schemas/scalable-inference-serving/scalable-inference-serving-requestoutput/)
- [ResponseOutput](https://apis.io/schemas/scalable-inference-serving/scalable-inference-serving-responseoutput/)
- [ServerLiveResponse](https://apis.io/schemas/scalable-inference-serving/scalable-inference-serving-serverliveresponse/)
- [ServerMetadataResponse](https://apis.io/schemas/scalable-inference-serving/scalable-inference-serving-servermetadataresponse/)
- [ServerReadyResponse](https://apis.io/schemas/scalable-inference-serving/scalable-inference-serving-serverreadyresponse/)
- [TensorDatatype](https://apis.io/schemas/scalable-inference-serving/scalable-inference-serving-tensordatatype/)
- [TensorMetadata](https://apis.io/schemas/scalable-inference-serving/scalable-inference-serving-tensormetadata/)

#### JSON Structure (2)

Data models expressed in JSON Structure.

- [Kserve Inference Request Structure](https://apis.io/json-structure/scalable-inference-serving/kserve-inference-request-structure/)
- [Scalable Inference Serving Structure](https://apis.io/json-structure/scalable-inference-serving/scalable-inference-serving-structure/)

#### JSON-LD (1)

Linked-data contexts for the provider's vocabulary.

- [Scalable Inference Serving Context](https://apis.io/jsonld/scalable-inference-serving/scalable-inference-serving-context/)

#### Vocabulary (1)

The provider's domain terms, defined.

- [Scalable Inference Serving Vocabulary](https://apis.io/vocabularies/scalable-inference-serving/scalable-inference-serving-vocabulary/)

#### Examples (9)

Example requests and responses.

- [Kserve Check Server Liveness Example](https://apis.io/examples/scalable-inference-serving/kserve-check-server-liveness-example/)
- [Kserve Get Model Metadata Example](https://apis.io/examples/scalable-inference-serving/kserve-get-model-metadata-example/)
- [Kserve Run Inference Example](https://apis.io/examples/scalable-inference-serving/kserve-run-inference-example/)
- [Scalable Inference Serving Checkmodelreadiness Example](https://apis.io/examples/scalable-inference-serving/scalable-inference-serving-checkmodelreadiness-example/)
- [Scalable Inference Serving Checkserverliveness Example](https://apis.io/examples/scalable-inference-serving/scalable-inference-serving-checkserverliveness-example/)
- [Scalable Inference Serving Checkserverreadiness Example](https://apis.io/examples/scalable-inference-serving/scalable-inference-serving-checkserverreadiness-example/)
- [Scalable Inference Serving Getmodelmetadata Example](https://apis.io/examples/scalable-inference-serving/scalable-inference-serving-getmodelmetadata-example/)
- [Scalable Inference Serving Getservermetadata Example](https://apis.io/examples/scalable-inference-serving/scalable-inference-serving-getservermetadata-example/)
- [Scalable Inference Serving Runinference Example](https://apis.io/examples/scalable-inference-serving/scalable-inference-serving-runinference-example/)

#### Collections (5)

Postman and Open Collection request collections.

- [KServe Open Inference Protocol API](https://apis.io/collections/scalable-inference-serving/open-kserve-open-inference-protocol/)
- [KServe Open Inference Protocol Health API](https://apis.io/collections/scalable-inference-serving/open-scalable-inference-serving-health-api/)
- [KServe Open Protocol Health Inference API](https://apis.io/collections/scalable-inference-serving/open-scalable-inference-serving-inference-api/)
- [KServe Open Inference Protocol Health Metadata API](https://apis.io/collections/scalable-inference-serving/open-scalable-inference-serving-metadata-api/)
- [KServe Open Inference Protocol Health Models API](https://apis.io/collections/scalable-inference-serving/open-scalable-inference-serving-models-api/)

#### Governance rules (2)

Spectral rulesets for the provider's contracts.

- [Scalable Inference Serving — kserve open inference protocol rules](https://apis.io/rules/scalable-inference-serving/kserve-open-inference-protocol-rules/)
- [Scalable Inference Serving — jsonschema rules](https://apis.io/rules/scalable-inference-serving/scalable-inference-serving-jsonschema-spectral-rules/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Scalable Inference Serving Plans Pricing](https://apis.io/plans/scalable-inference-serving/scalable-inference-serving-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Scalable Inference Serving Rate Limits](https://apis.io/rate-limits/scalable-inference-serving/scalable-inference-serving-rate-limits/)

#### FinOps (1)

What the API costs to run, by operation.

- [Scalable Inference Serving Finops](https://apis.io/finops/scalable-inference-serving/scalable-inference-serving-finops/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Getting started](https://kserve.github.io/website/docs/get_started/)
- [Blog](https://kserve.github.io/website/blog/)
- [GitHub](https://github.com/kserve)

## API Evangelist rating

**Unrated** — no public website could be reached for this company, so there was almost nothing to measure and nothing a reader could check.

This is not a score of zero. No rating is published for this company. If that is wrong because something public exists that we missed, say so on this repository or email [info@apievangelist.com](mailto:info@apievangelist.com) and it will be re-run — free, and no justification needed.

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Scalable Inference Serving: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/scalable-inference-serving/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
