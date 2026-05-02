# Scalable Inference Serving

A collection of APIs, frameworks, and platforms for scalable machine learning model inference serving, deployment, and management. Includes the KServe Open Inference Protocol (the CNCF standard for model serving on Kubernetes), BentoML, vLLM (high-throughput LLM inference), NVIDIA Triton Inference Server, MLflow Model Registry, and Ray Serve.

**URL:** [https://raw.githubusercontent.com/api-evangelist/scalable-inference-serving/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/scalable-inference-serving/refs/heads/main/apis.yml)

## Tags

AI, CNCF, Deployment, Inference, Kubernetes, LLM, Machine Learning, Model Serving, MLOps, Scalability

## Timestamps

- **Created:** 2024-01-01
- **Modified:** 2026-05-02

## APIs

### KServe Open Inference Protocol API
Standardized distributed generative and predictive AI inference platform for Kubernetes with REST/gRPC endpoints for model inference, health, and metadata. CNCF incubating project.

**Human URL:** [https://kserve.github.io/website/](https://kserve.github.io/website/)

#### Tags

CNCF, Inference, Kubernetes, Model Serving, Open Inference Protocol, Open Source

#### Properties

- [Documentation](https://kserve.github.io/website/docs/intro)
- [OpenAPI](openapi/kserve-open-inference-protocol-openapi.yml)
- [GitHub](https://github.com/kserve/kserve)
- [Getting Started](https://kserve.github.io/website/docs/get_started/)
- [Swagger UI](https://kserve.github.io/website/latest/reference/swagger-ui/)

### BentoML REST API
Open-source unified ML model serving framework with auto-generated REST APIs, adaptive batching, Runner abstraction, and KServe integration.

**Human URL:** [https://www.bentoml.com/](https://www.bentoml.com/)

#### Tags

Batching, Inference, Model Serving, Open Source, Python, REST API

#### Properties

- [Documentation](https://docs.bentoml.com/en/latest/)
- [GitHub](https://github.com/bentoml/BentoML)
- [API Reference](https://docs.bentoml.com/en/latest/reference/index.html)
- [Getting Started](https://docs.bentoml.com/en/latest/get-started/quickstart.html)

### vLLM OpenAI-Compatible API
High-throughput LLM inference engine with PagedAttention, OpenAI-compatible REST API, and KServe integration via LLMInferenceService.

**Human URL:** [https://docs.vllm.ai/](https://docs.vllm.ai/)

#### Tags

GPU, Inference, KV Cache, LLM, Model Serving, Open Source, OpenAI-Compatible

#### Properties

- [Documentation](https://docs.vllm.ai/en/stable/)
- [GitHub](https://github.com/vllm-project/vllm)
- [API Reference](https://docs.vllm.ai/en/stable/serving/openai_compatible_server.html)

### NVIDIA Triton Inference Server HTTP API
Open-source inference server implementing OIP with TensorRT, ONNX, TensorFlow, and PyTorch backends; dynamic batching and GPU/CPU concurrent execution.

**Human URL:** [https://developer.nvidia.com/triton-inference-server](https://developer.nvidia.com/triton-inference-server)

#### Tags

GPU, Inference, Model Serving, NVIDIA, Open Source, TensorRT, Triton

#### Properties

- [Documentation](https://docs.nvidia.com/deeplearning/triton-inference-server/user-guide/docs/)
- [GitHub](https://github.com/triton-inference-server/server)

### MLflow Model Registry REST API
Open-source ML lifecycle platform; REST API for experiments, runs, metrics, artifacts, and model versioning/staging.

**Human URL:** [https://mlflow.org/](https://mlflow.org/)

#### Tags

Experiment Tracking, Machine Learning, Model Registry, MLOps, Open Source, Versioning

#### Properties

- [Documentation](https://mlflow.org/docs/latest/rest-api.html)
- [GitHub](https://github.com/mlflow/mlflow)
- [Getting Started](https://mlflow.org/docs/latest/getting-started/intro-quickstart/)

### Ray Serve REST API
Scalable model serving library on Ray; supports composable multi-model pipelines, autoscaling, and HTTP/gRPC ingress.

**Human URL:** [https://docs.ray.io/en/latest/serve/index.html](https://docs.ray.io/en/latest/serve/index.html)

#### Tags

Autoscaling, Inference, Machine Learning, Model Serving, Open Source, Python, Ray

#### Properties

- [Documentation](https://docs.ray.io/en/latest/serve/index.html)
- [GitHub](https://github.com/ray-project/ray)
- [API Reference](https://docs.ray.io/en/latest/serve/api/index.html)

## OpenAPI Specifications

| Artifact | Description |
|---|---|
| [KServe Open Inference Protocol OpenAPI](openapi/kserve-open-inference-protocol-openapi.yml) | Full OpenAPI 3.1 spec for the OIP V2 REST API covering health, metadata, and inference endpoints with complete request/response schemas. |

## Spectral Rules

| Artifact | Description |
|---|---|
| [KServe Open Inference Protocol Rules](rules/kserve-open-inference-protocol-rules.yml) | Spectral ruleset enforcing OIP path conventions, operation ID naming, required fields, tensor datatype enumeration, and Title Case summary requirements. |

## Capabilities

### Shared Definitions

| Artifact | Description |
|---|---|
| [KServe Open Inference Protocol](capabilities/shared/kserve-open-inference-protocol.yaml) | Shared per-API capability definition with full consumes/exposes structure for all 7 OIP operations. |

### Workflow Capabilities

| Artifact | Description |
|---|---|
| [Model Inference Operations](capabilities/model-inference-operations.yaml) | Unified REST and MCP workflow capability for ML engineers to run inference, monitor health, and inspect model metadata. 8 tools. |

## Schemas

| Artifact | Description |
|---|---|
| [Inference Request Schema](json-schema/kserve-inference-request-schema.json) | JSON Schema for OIP V2 inference requests including tensor inputs, shape, datatype, and optional outputs specification. |
| [Model Metadata Schema](json-schema/kserve-model-metadata-schema.json) | JSON Schema for model metadata responses including tensor specifications and platform information. |

## Structures

| Artifact | Description |
|---|---|
| [Inference Request Structure](json-structure/kserve-inference-request-structure.json) | Hierarchical field documentation for OIP inference request objects. |

## Linked Data

| Artifact | Description |
|---|---|
| [Scalable Inference Serving Context](json-ld/scalable-inference-serving-context.jsonld) | JSON-LD context mapping inference serving vocabulary to schema.org, KServe, and OIP namespaces. |

## Examples

| Artifact | Description |
|---|---|
| [Check Server Liveness Example](examples/kserve-check-server-liveness-example.json) | Example GET /v2/health/live request and response for Kubernetes livenessProbe implementation. |
| [Run Inference Example](examples/kserve-run-inference-example.json) | Example POST /v2/models/{model_name}/infer with BERT tokenized input tensors and sentiment classification output. |
| [Get Model Metadata Example](examples/kserve-get-model-metadata-example.json) | Example GET /v2/models/{model_name} response with ResNet-50 input/output tensor specifications. |

## Vocabulary

| Artifact | Description |
|---|---|
| [Scalable Inference Serving Vocabulary](vocabulary/scalable-inference-serving-vocabulary.yml) | Normative vocabulary covering inference protocols, serving frameworks, LLM concepts (PagedAttention, KV Cache), batching strategies, and MLOps lifecycle. |

## Common Properties

- [Getting Started](https://kserve.github.io/website/docs/get_started/)
- [GitHub Organization](https://github.com/kserve)
- [CNCF Landscape](https://landscape.cncf.io/card-mode?project=incubating)
- [Blog](https://kserve.github.io/website/blog/)

## Maintainers

**API Evangelist** — [kin@apievangelist.com](mailto:kin@apievangelist.com) — [https://apievangelist.com](https://apievangelist.com)
