---
title: "Best of Both Worlds: Cloud-Native AI Inference at Scale using KServe and llm-d"
url: "https://kserve.github.io/website/blog/cloud-native-ai-inference-kserve-llm-d"
date: "Thu, 05 Mar 2026 00:00:00 GMT"
author: ""
feed_url: "https://kserve.github.io/website/blog/rss"
---
<p>Enterprises today seek to integrate generative AI (GenAI) capabilities into their applications. However, scaling large AI models introduces complexity: managing high-volume traffic from large language models (LLMs), optimizing inference performance, maintaining predictable latency, and controlling infrastructure costs.</p>
<p>Platform engineering leaders require more than just model deployment capabilities. They need a robust, Kubernetes-native infrastructure that supports:</p>
<ul>
<li class="">Efficient GPU utilization</li>
<li class="">Intelligent request routing</li>
<li class="">Distributed inference patterns</li>
<li class="">Cost-aware autoscaling</li>
<li class="">Production-grade governance</li>
</ul>
<p>This article demonstrates how two open-source solutions, KServe and llm-d, can be combined to address these challenges.</p>
<p>We explore the role of each solution, illustrate their integration architecture, and provide practical guidance for AI platform teams, with deeper focus on KServe's LLMInferenceService, available since KServe v0.16.</p>
<h2 class="anchor anchorTargetStickyNavbar_Vzrq" id="kserve-simplified-deployment-of-ai-models-on-kubernetes">KServe: Simplified Deployment of AI Models on Kubernetes<a class="hash-link" href="https://kserve.github.io/website/blog/cloud-native-ai-inference-kserve-llm-d#kserve-simplified-deployment-of-ai-models-on-kubernetes" title="Direct link to KServe: Simplified Deployment of AI Models on Kubernetes">​</a></h2>
<p>KServe is a Kubernetes-based model serving platform that simplifies deploying and managing ML models, including LLMs, at scale.</p>
<p>For platform engineers, KServe acts as the model serving control plane: the layer responsible for lifecycle, scaling, and operational governance.</p>
<p><img alt="KServe Generative Inference Architecture" class="img_ev3q" src="https://kserve.github.io/website/assets/images/kserve_generative_inference-21648e7df404ea6f57b9d3c83e8e0ca4.png" /></p>
<h3 class="anchor anchorTargetStickyNavbar_Vzrq" id="inference-as-a-service">Inference as a Service<a class="hash-link" href="https://kserve.github.io/website/blog/cloud-native-ai-inference-kserve-llm-d#inference-as-a-service" title="Direct link to Inference as a Service">​</a></h3>
<p>InferenceService serves as KServe's core abstraction for model deployment, encapsulating the full serving lifecycle, including:</p>
<ul>
<li class="">Automatic deployment creation and reconciliation</li>
<li class="">Request-based autoscaling with scale-to-zero and autoscaling based on custom metrics</li>
<li class="">Revision management and canary rollouts</li>
<li class="">Endpoint exposure and traffic routing</li>
<li class="">Runtime abstraction across serving backends for both predictive and generative AI</li>
<li class="">Optional pre-processing/post-processing, inference pipelines, and ensembles</li>
</ul>
<p>ML engineers provide trained models. Platform engineers retain operational control without writing custom deployment code.</p>
<h3 class="anchor anchorTargetStickyNavbar_Vzrq" id="llminferenceservice-in-kserve">LLMInferenceService in KServe<a class="hash-link" href="https://kserve.github.io/website/blog/cloud-native-ai-inference-kserve-llm-d#llminferenceservice-in-kserve" title="Direct link to LLMInferenceService in KServe">​</a></h3>
<p>KServe v0.16 introduces stronger generative AI capabilities, including LLMInferenceService, designed specifically for large language model workloads.</p>
<p>Unlike traditional stateless predictors, LLM workloads require:</p>
<ul>
<li class="">Long-running streaming responses</li>
<li class="">GPU-heavy memory footprints</li>
<li class="">Prefix KV-cache management</li>
<li class="">High-concurrency token streaming</li>
<li class="">OpenAI-compatible APIs</li>
</ul>
<p>LLMInferenceService shares common foundations with InferenceService but introduces additional capabilities tailored for large language models, including:</p>
<h3 class="anchor anchorTargetStickyNavbar_Vzrq" id="unlocking-generative-ai-serving-with-llminferenceservice-from-pod-level-speed-to-cluster-wide-intelligence">Unlocking Generative AI Serving with LLMInferenceService: From Pod-Level Speed to Cluster-Wide Intelligence<a class="hash-link" href="https://kserve.github.io/website/blog/cloud-native-ai-inference-kserve-llm-d#unlocking-generative-ai-serving-with-llminferenceservice-from-pod-level-speed-to-cluster-wide-intelligence" title="Direct link to Unlocking Generative AI Serving with LLMInferenceService: From Pod-Level Speed to Cluster-Wide Intelligence">​</a></h3>
<p>Imagine you want to bring the power of generative AI directly into your applications, but without rewriting your entire stack. It offers OpenAI-compatible endpoints like <code>/v1/chat/completions</code>, complete with streaming token responses and multi-turn support. With prompt templating built in, developers can integrate seamlessly with existing tools—whether it's the OpenAI SDKs, LangChain, LlamaIndex, Llama Stack, RAG frameworks, or even enterprise GenAI gateways.</p>
<p>Under the hood, KServe connects to LLM-optimized runtimes such as vLLM, Hugging Face TGI, or other GPU-native backends. These engines bring advanced capabilities like continuous batching, memory-efficient paged attention, and KV-cache reuse, delivering high throughput per GPU.</p>
<p>Yet, while these runtime-level optimizations make each pod lightning fast, true cluster-wide efficiency needs more. That's exactly the role of llm-d: adding an extra layer of intelligence that orchestrates resources and maximizes performance across the entire deployment.</p>
<h3 class="anchor anchorTargetStickyNavbar_Vzrq" id="distributed--multi-node-model-support">Distributed &amp; Multi-Node Model Support<a class="hash-link" href="https://kserve.github.io/website/blog/cloud-native-ai-inference-kserve-llm-d#distributed--multi-node-model-support" title="Direct link to Distributed &amp; Multi-Node Model Support">​</a></h3>
<p>LLMInferenceService supports advanced parallelism strategies implemented by runtimes, including tensor parallelism, pipeline parallelism, and multi-GPU sharding.</p>
<p>This enables hosting 70B+ parameter models, partitioning models across nodes, and serving models larger than single-GPU memory.</p>
<p>KServe orchestrates the deployment topology, while the runtime manages execution parallelism.</p>
<h3 class="anchor anchorTargetStickyNavbar_Vzrq" id="advanced-autoscaling--networking-including-scale-to-zero">Advanced Autoscaling &amp; Networking (Including Scale-to-Zero)<a class="hash-link" href="https://kserve.github.io/website/blog/cloud-native-ai-inference-kserve-llm-d#advanced-autoscaling--networking-including-scale-to-zero" title="Direct link to Advanced Autoscaling &amp; Networking (Including Scale-to-Zero)">​</a></h3>
<p>KServe integrates deeply with Kubernetes to support request- and concurrency-based autoscaling via Knative, GPU-backed scaling, and scale-to-zero for cost control.</p>
<p>It also integrates with the Kubernetes Gateway API for TLS termination, traffic splitting, and advanced routing.</p>
<p>This makes it suitable for development environments, internal copilots, and large-scale production workloads.</p>
<h3 class="anchor anchorTargetStickyNavbar_Vzrq" id="kubernetes-gateway-api-integration">Kubernetes Gateway API Integration<a class="hash-link" href="https://kserve.github.io/website/blog/cloud-native-ai-inference-kserve-llm-d#kubernetes-gateway-api-integration" title="Direct link to Kubernetes Gateway API Integration">​</a></h3>
<p>KServe integrates with Kubernetes Gateway API for:</p>
<ul>
<li class="">Enterprise-grade routing</li>
<li class="">TLS termination</li>
<li class="">Traffic splitting</li>
<li class="">Multi-model routing</li>
</ul>
<p>This enables integration with modern Kubernetes networking stacks.</p>
<h3 class="anchor anchorTargetStickyNavbar_Vzrq" id="where-kserve-alone-is-not-enough">Where KServe Alone Is Not Enough<a class="hash-link" href="https://kserve.github.io/website/blog/cloud-native-ai-inference-kserve-llm-d#where-kserve-alone-is-not-enough" title="Direct link to Where KServe Alone Is Not Enough">​</a></h3>
<p>Even with LLMInferenceService and optimized runtimes, KServe does not inherently:</p>
<ul>
<li class="">Route requests based on KV-cache locality across replicas</li>
<li class="">Separate prefill and decode cluster-wide</li>
<li class="">Perform SLA-aware routing decisions</li>
<li class="">Optimize GPU utilization across multiple pods</li>
</ul>
<p>To address these, we introduce llm-d.</p>
<h2 class="anchor anchorTargetStickyNavbar_Vzrq" id="llm-d-distributed-intelligence-for-llm-inference">llm-d: Distributed Intelligence for LLM Inference<a class="hash-link" href="https://kserve.github.io/website/blog/cloud-native-ai-inference-kserve-llm-d#llm-d-distributed-intelligence-for-llm-inference" title="Direct link to llm-d: Distributed Intelligence for LLM Inference">​</a></h2>
<p>llm-d is a Kubernetes-native distributed inference framework designed to enhance performance and efficiency of LLM workloads.</p>
<p>If KServe is the control plane for models, llm-d is the distributed intelligence scheduling layer.</p>
<p><img alt="llm-d Architecture" class="img_ev3q" src="https://github.com/llm-d/llm-d/raw/main/docs/assets/images/llm-d-arch.svg" /></p>
<h3 class="anchor anchorTargetStickyNavbar_Vzrq" id="kv-cache-aware-scheduling-and-disaggregated-inference-with-llm-d">KV-Cache Aware Scheduling and Disaggregated Inference with llm-d<a class="hash-link" href="https://kserve.github.io/website/blog/cloud-native-ai-inference-kserve-llm-d#kv-cache-aware-scheduling-and-disaggregated-inference-with-llm-d" title="Direct link to KV-Cache Aware Scheduling and Disaggregated Inference with llm-d">​</a></h3>
<p>As LLM deployments mature, scaling is no longer just about adding GPUs. It's about using them intelligently. Modern runtimes such as vLLM introduced prefix (KV) caching to reduce redundant computation, but without smart scheduling, much of that benefit is lost.</p>
<p>This is where llm-d changes the game.</p>
<h3 class="anchor anchorTargetStickyNavbar_Vzrq" id="disaggregated-inference-prefill--decode-separation">Disaggregated Inference (Prefill / Decode Separation)<a class="hash-link" href="https://kserve.github.io/website/blog/cloud-native-ai-inference-kserve-llm-d#disaggregated-inference-prefill--decode-separation" title="Direct link to Disaggregated Inference (Prefill / Decode Separation)">​</a></h3>
<p>LLM inference consists of two distinct phases: prefill and decode. The prefill phase is compute-heavy, processing the full prompt and building the model's attention context. The decode phase is latency-sensitive, generating tokens step by step where responsiveness directly impacts user experience.</p>
<p>llm-d separates these phases across different GPU groups, assigning compute-optimized resources to prefill and latency-optimized resources to decode. With intelligent scheduling between them, workloads are aligned to the right hardware profile.</p>
<p>This phase-aware architecture increases GPU utilization, reduces tail latency, and lowers cost per token by eliminating resource contention between fundamentally different workloads.</p>
<h3 class="anchor anchorTargetStickyNavbar_Vzrq" id="intelligent-inference-scheduler">Intelligent Inference Scheduler<a class="hash-link" href="https://kserve.github.io/website/blog/cloud-native-ai-inference-kserve-llm-d#intelligent-inference-scheduler" title="Direct link to Intelligent Inference Scheduler">​</a></h3>
<p>llm-d's inference scheduler evaluates the following metrics:</p>
<ul>
<li class="">GPU utilization</li>
<li class="">Queue depth</li>
<li class="">Cache residency</li>
<li class="">SLA constraints</li>
<li class="">Load distribution</li>
</ul>
<p>It enhances load balancing with an intelligent scheduler to decrease serving latency and increase throughput with prefix-cache aware routing, utilization-based load balancing, fairness and prioritization for multi-tenant serving, and predicted latency balancing.</p>
<h2 class="anchor anchorTargetStickyNavbar_Vzrq" id="kserve-llminferenceservice-and-llm-d">KServe LLMInferenceService and llm-d<a class="hash-link" href="https://kserve.github.io/website/blog/cloud-native-ai-inference-kserve-llm-d#kserve-llminferenceservice-and-llm-d" title="Direct link to KServe LLMInferenceService and llm-d">​</a></h2>
<h3 class="anchor anchorTargetStickyNavbar_Vzrq" id="responsibility-separation">Responsibility Separation<a class="hash-link" href="https://kserve.github.io/website/blog/cloud-native-ai-inference-kserve-llm-d#responsibility-separation" title="Direct link to Responsibility Separation">​</a></h3>
<p>This layered design ensures composability and specialization, providing a complete, production-ready solution for generative AI. KServe acts as the control plane and LLMInferenceService delivers the generative API abstraction, while llm-d provides the cluster-wide optimization.</p>
<table><thead><tr><th>Layer</th><th>Responsibility</th></tr></thead><tbody><tr><td>KServe</td><td>Model lifecycle, scaling, governance</td></tr><tr><td>LLMInferenceService</td><td>Generative API abstraction</td></tr><tr><td>vLLM</td><td>Efficient execution inside runtime</td></tr><tr><td>llm-d</td><td>Cross-runtime routing &amp; cache awareness</td></tr><tr><td>Kubernetes</td><td>Resource orchestration</td></tr></tbody></table>
<p>Together, KServe and llm-d enable a production-ready, Kubernetes-native inference platform that balances scalability, performance, and cost efficiency, providing the best of both worlds for cloud-native AI inference at scale.</p>
<h2 class="anchor anchorTargetStickyNavbar_Vzrq" id="cost-efficiency-comparison-naive-vs-optimized">Cost Efficiency Comparison: Naive vs Optimized<a class="hash-link" href="https://kserve.github.io/website/blog/cloud-native-ai-inference-kserve-llm-d#cost-efficiency-comparison-naive-vs-optimized" title="Direct link to Cost Efficiency Comparison: Naive vs Optimized">​</a></h2>
<p>Serving LLMs at scale is no longer just a model problem. It is a distributed systems problem where naive load balancing leads to significant inefficiencies and wasted resources — lost cache locality, GPU imbalance, redundant prefill processing, high tail latency, and overprovisioned GPUs.</p>
<p><strong>Naive Problems:</strong></p>
<ul>
<li class="">Cache locality loss</li>
<li class="">GPU imbalance</li>
<li class="">Redundant prefill processing</li>
<li class="">High tail latency</li>
<li class="">Overprovisioned GPUs</li>
</ul>
<h3 class="anchor anchorTargetStickyNavbar_Vzrq" id="optimized-architecture-with-kserve--llm-d">Optimized Architecture with KServe + llm-d<a class="hash-link" href="https://kserve.github.io/website/blog/cloud-native-ai-inference-kserve-llm-d#optimized-architecture-with-kserve--llm-d" title="Direct link to Optimized Architecture with KServe + llm-d">​</a></h3>
<p>The combined KServe and llm-d solution introduces distributed intelligence to solve the problems of naive architectures, delivering superior performance, scalability, and cost control. This optimized architecture is pluggable and extensible to work well with many AI and cloud-native technologies.</p>
<p><img alt="KServe Layered Architecture" class="img_ev3q" src="https://kserve.github.io/website/img/kserve-layer.png" /></p>
<p><strong>Benefits:</strong></p>
<ul>
<li class="">Cache reuse preserved</li>
<li class="">Balanced GPU utilization</li>
<li class="">Reduced recomputation</li>
<li class="">Lower cost per token</li>
<li class="">Controlled autoscaling via LLMInferenceService</li>
</ul>
<h2 class="anchor anchorTargetStickyNavbar_Vzrq" id="benchmark-results-why-cluster-level-intelligence-matters">Benchmark Results: Why Cluster-Level Intelligence Matters<a class="hash-link" href="https://kserve.github.io/website/blog/cloud-native-ai-inference-kserve-llm-d#benchmark-results-why-cluster-level-intelligence-matters" title="Direct link to Benchmark Results: Why Cluster-Level Intelligence Matters">​</a></h2>
<p>By integrating llm-d's cache-aware routing, prefill and decode disaggregation, and SLA-based scheduling with KServe's enterprise-grade generative serving and autoscaling, the system achieves cluster-wide GPU optimization.</p>
<p><em>Note: The following results are based on benchmarks published by the llm-d project</em></p>
<table><thead><tr><th>Optimization Area</th><th>Naive Architecture (Round Robin LB)</th><th>Optimized (KServe + llm-d)</th><th>Source</th></tr></thead><tbody><tr><td>Cache Locality</td><td>Requests routed randomly → KV cache frequently missed</td><td>Cache-aware routing preserves prefix locality</td><td><a class="" href="https://llm-d.ai/blog/kvcache-wins-you-can-see" rel="noopener noreferrer" target="_blank">llm-d blog</a></td></tr><tr><td>Time to First Token (P90)</td><td>Baseline latency under cache-blind scheduling</td><td>Up to ~57× faster P90 TTFT in benchmark</td><td><a class="" href="https://llm-d.ai/blog/kvcache-wins-you-can-see" rel="noopener noreferrer" target="_blank">llm-d blog</a></td></tr><tr><td>Token Throughput</td><td>~4,400 tokens/sec (baseline test cluster)</td><td>~8,730 tokens/sec (~2× improvement)</td><td><a class="" href="https://llm-d.ai/blog/kvcache-wins-you-can-see" rel="noopener noreferrer" target="_blank">llm-d blog</a></td></tr><tr><td>Throughput at Scale</td><td>Degrades under multi-tenant load</td><td>Sustained 4.5k–11k tokens/sec</td><td><a class="" href="https://llm-d.ai/blog/llm-d-v0.5-sustaining-performance-at-scale" rel="noopener noreferrer" target="_blank">llm-d blog</a></td></tr><tr><td>Tail Latency (P95/P99)</td><td>Higher tail latency due to stragglers &amp; imbalance</td><td>~50% tail latency reduction (reported tests)</td><td><a class="" href="https://developers.redhat.com/articles/2025/05/20/llm-d-kubernetes-native-distributed-inferencing" rel="noopener noreferrer" target="_blank">Red Hat Developers</a></td></tr><tr><td>GPU Utilization</td><td>Uneven utilization, idle GPUs possible</td><td>Improved effective utilization via routing intelligence</td><td><a class="" href="https://llm-d.ai/docs/guide/Installation/inference-scheduling" rel="noopener noreferrer" target="_blank">llm-d docs</a></td></tr><tr><td>Autoscaling Control</td><td>Scale reacts to load only</td><td>Works with KServe autoscaling + routing intelligence</td><td><a class="" href="https://kserve.github.io/website/docs/model-serving/predictive-inference/autoscaling/kpa-autoscaler" rel="noopener noreferrer" target="_blank">KServe docs</a></td></tr></tbody></table>
<p>Modern GenAI platforms require cache locality awareness, phase-aware scheduling, distributed intelligence, and composable Kubernetes-native design. This combination ensures a production-ready system that meets the demands of large-scale production workloads.</p>
<h2 class="anchor anchorTargetStickyNavbar_Vzrq" id="next-steps">Next Steps<a class="hash-link" href="https://kserve.github.io/website/blog/cloud-native-ai-inference-kserve-llm-d#next-steps" title="Direct link to Next Steps">​</a></h2>
<p>Explore detailed project documentation:</p>
<ul>
<li class=""><a class="" href="https://kserve.github.io/website/" rel="noopener noreferrer" target="_blank">KServe</a></li>
<li class=""><a class="" href="https://llm-d.ai/" rel="noopener noreferrer" target="_blank">llm-d</a></li>
</ul>
<p>Engage with community resources and Slack channels to stay updated and contribute to ongoing developments:</p>
<ul>
<li class=""><a class="" href="https://kserve.github.io/website/community/get_involved/" rel="noopener noreferrer" target="_blank">KServe community</a></li>
<li class=""><a class="" href="https://llm-d.ai/community/" rel="noopener noreferrer" target="_blank">llm-d community</a></li>
</ul>
