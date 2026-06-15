# Scalable Inference Serving (scalable-inference-serving)

A collection of APIs, frameworks, and platforms for scalable machine learning model inference serving, deployment, and management. This includes the KServe Open Inference Protocol (the CNCF standard for model serving on Kubernetes), BentoML (developer packaging and serving), vLLM (high-throughput LLM inference), NVIDIA Triton Inference Server, and supporting observability and registry tools. KServe recently joined CNCF as an incubating project (November 2025).

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/scalable-inference-serving/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/scalable-inference-serving/refs/heads/main/apis.yml)

## Tags

- AI
- CNCF
- Deployment
- Inference
- Kubernetes
- LLM
- Machine Learning
- Model Serving
- MLOps
- Scalability

## Timestamps

- **Created:** 2024-01-01
- **Modified:** 2026-05-19

## APIs

### KServe Open Inference Protocol API

KServe implements the Open Inference Protocol (OIP), also known as the KServe V2 Inference Protocol, which provides a standardized REST and gRPC interface for model inference across frameworks. KServe is a standardized distributed generative and predictive AI inference platform for scalable, multi-framework deployment on Kubernetes. CNCF incubating project since November 2025. Supports TensorFlow, PyTorch, scikit-learn, XGBoost, ONNX, vLLM, and HuggingFace.

#### Tags

- CNCF
- Inference
- Kubernetes
- Model Serving
- Open Inference Protocol
- Open Source

#### Properties

- [Documentation](https://kserve.github.io/website/docs/intro)
- [OpenAPI](https://raw.githubusercontent.com/api-evangelist/scalable-inference-serving/main/openapi/kserve-open-inference-protocol-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Git Hub](https://github.com/kserve/kserve)
- [Changelog](https://github.com/kserve/kserve/releases)
- [Getting Started](https://kserve.github.io/website/docs/get_started/)
- [Swagger U I](https://kserve.github.io/website/latest/reference/swagger-ui/)
- [Postman Collection](collections/kserve-open-inference-protocol.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/kserve-open-inference-protocol.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### BentoML REST API

BentoML is an open-source unified inference platform for deploying and scaling AI models. It auto-generates RESTful APIs from Python service definitions, provides built-in OpenAPI/Swagger documentation, supports adaptive batching, and integrates with KServe for Kubernetes deployment. BentoML 1.0 introduced the Runner abstraction for parallelizing inference workloads with adaptive batching and independent scaling of pre/post-processing from model inference.

#### Tags

- Batching
- Inference
- Model Serving
- Open Source
- Python
- REST API

#### Properties

- [Documentation](https://docs.bentoml.com/en/latest/)
- [Git Hub](https://github.com/bentoml/BentoML)
- [Getting Started](https://docs.bentoml.com/en/latest/get-started/quickstart.html)
- [Pricing](https://www.bentoml.com/pricing)
- [API Reference](https://docs.bentoml.com/en/latest/reference/index.html)
- [Postman Collection](collections/kserve-open-inference-protocol.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/kserve-open-inference-protocol.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### vLLM OpenAI-Compatible API

vLLM is a high-throughput and memory-efficient inference engine for LLMs, implementing PagedAttention for efficient KV cache management. vLLM exposes an OpenAI-compatible REST API allowing seamless migration from OpenAI endpoints. In 2026, vLLM integrates with KServe via LLMInferenceService and llm-d for production-grade distributed LLM inference. Powers major LLM deployments at scale.

#### Tags

- GPU
- Inference
- KV Cache
- LLM
- Model Serving
- Open Source
- OpenAI-Compatible

#### Properties

- [Documentation](https://docs.vllm.ai/en/stable/)
- [Git Hub](https://github.com/vllm-project/vllm)
- [API Reference](https://docs.vllm.ai/en/stable/serving/openai_compatible_server.html)
- [Changelog](https://github.com/vllm-project/vllm/releases)
- [Postman Collection](collections/kserve-open-inference-protocol.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/kserve-open-inference-protocol.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### NVIDIA Triton Inference Server HTTP API

NVIDIA Triton Inference Server is an open-source inference serving software that implements the KServe Open Inference Protocol (V2). Supports TensorRT, ONNX, TensorFlow, PyTorch, and Python backends. Provides dynamic batching, model ensembles, model analyzers, and GPU/CPU inference. Used extensively in production ML pipelines requiring maximum throughput.

#### Tags

- GPU
- Inference
- Model Serving
- NVIDIA
- Open Source
- TensorRT
- Triton

#### Properties

- [Documentation](https://docs.nvidia.com/deeplearning/triton-inference-server/user-guide/docs/)
- [Git Hub](https://github.com/triton-inference-server/server)
- [Getting Started](https://github.com/triton-inference-server/tutorials)
- [API Reference](https://docs.nvidia.com/deeplearning/triton-inference-server/user-guide/docs/customization_guide/inference_protocols.html)
- [Postman Collection](collections/kserve-open-inference-protocol.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/kserve-open-inference-protocol.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### MLflow Model Registry REST API

MLflow is an open source platform for managing the ML lifecycle, including experiment tracking, reproducibility, and deployment. The MLflow REST API manages experiments, runs, metrics, parameters, artifacts, and the Model Registry for versioning and staging model deployments. CNCF-adjacent; used with KServe for model lifecycle management.

#### Tags

- Experiment Tracking
- Machine Learning
- Model Registry
- MLOps
- Open Source
- Versioning

#### Properties

- [Documentation](https://mlflow.org/docs/latest/rest-api.html)
- [Git Hub](https://github.com/mlflow/mlflow)
- [Getting Started](https://mlflow.org/docs/latest/getting-started/intro-quickstart/)
- [API Reference](https://mlflow.org/docs/latest/rest-api.html)
- [Postman Collection](collections/kserve-open-inference-protocol.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/kserve-open-inference-protocol.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Ray Serve REST API

Ray Serve is a scalable model serving library built on Ray, designed for building online inference APIs. Supports composable deployments, autoscaling, HTTP ingress, gRPC, WebSockets, and request batching. Integrates with any ML framework. The Ray Serve dashboard and REST API manage deployments, replicas, routes, and application status.

#### Tags

- Autoscaling
- Inference
- Machine Learning
- Model Serving
- Open Source
- Python
- Ray

#### Properties

- [Documentation](https://docs.ray.io/en/latest/serve/index.html)
- [Git Hub](https://github.com/ray-project/ray)
- [Getting Started](https://docs.ray.io/en/latest/serve/getting_started.html)
- [API Reference](https://docs.ray.io/en/latest/serve/api/index.html)
- [Postman Collection](collections/kserve-open-inference-protocol.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/kserve-open-inference-protocol.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [Authentication](https://kserve.github.io/website/docs/intro)
- [Getting Started](https://kserve.github.io/website/docs/get_started/)
- [GitHub Organization](https://github.com/kserve)
- [C N C F  Landscape](https://landscape.cncf.io/card-mode?project=incubating)
- [Blog](https://kserve.github.io/website/blog/)
- [OpenAPI](https://raw.githubusercontent.com/api-evangelist/scalable-inference-serving/main/openapi/kserve-open-inference-protocol-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Spectral Ruleset](https://raw.githubusercontent.com/api-evangelist/scalable-inference-serving/main/rules/kserve-open-inference-protocol-rules.yml)
- [JSON Schema](https://raw.githubusercontent.com/api-evangelist/scalable-inference-serving/main/json-schema/kserve-inference-request-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](https://raw.githubusercontent.com/api-evangelist/scalable-inference-serving/main/json-schema/kserve-model-metadata-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON-LD](https://raw.githubusercontent.com/api-evangelist/scalable-inference-serving/main/json-ld/scalable-inference-serving-context.jsonld) — [JSON-LD](https://www.w3.org/TR/json-ld11/)
- [Vocabulary](https://raw.githubusercontent.com/api-evangelist/scalable-inference-serving/main/vocabulary/scalable-inference-serving-vocabulary.yml)

## Maintainers

**Email:** kin@apievangelist.com
**URL:** https://apievangelist.com
