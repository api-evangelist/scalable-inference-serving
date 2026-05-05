---
title: "Production-Grade LLM Inference at Scale with KServe, llm-d, and vLLM"
url: "https://kserve.github.io/website/blog/production-grade-llm-inference-kserve-llm-d-vllm"
date: "Tue, 21 Apr 2026 00:00:00 GMT"
author: ""
feed_url: "https://kserve.github.io/website/blog/rss"
---
<p>Everyone is racing to run Large Language Models (LLMs), in the cloud, on-prem, and even on edge devices. The real challenge, however, isn't the first deployment; it's scaling, managing, and maintaining hundreds of LLMs efficiently. We initially approached this challenge with a straightforward vLLM deployment wrapped in a Kubernetes StatefulSet.</p>
<h2 class="anchor anchorTargetStickyNavbar_Vzrq" id="the-problem-with-simple-llm-deployments">The Problem with "Simple" LLM Deployments<a class="hash-link" href="https://kserve.github.io/website/blog/production-grade-llm-inference-kserve-llm-d-vllm#the-problem-with-simple-llm-deployments" title="Direct link to The Problem with &quot;Simple&quot; LLM Deployments">​</a></h2>
<p>The approach quickly introduced severe operational bottlenecks:</p>
<ul>
<li class=""><strong>Storage Drag:</strong> Models like Llama 3 can easily reach hundreds of gigabytes in size. Relying on sluggish network storage (NFS) for these massive safetensors was a non-starter.</li>
<li class=""><strong>Infrastructure Lock-in:</strong> Switching to local LVM persistent volumes solved the speed problem but created a rigid node-to-pod affinity. A single hardware failure meant a manual intervention to delete the Persistent Volume Claim (PVC) and reschedule the pod, which is an unacceptable burden for day-2 operations.</li>
<li class=""><strong>Naive Load Balancing:</strong> Beyond the looming retirement of NGINX Ingress Controller, a simple round-robin load-balancing strategy is fundamentally inefficient for LLMs. It fails to utilize the critical <strong>KV-cache</strong> on the GPU, a core feature of vLLM that significantly boosts throughput. In a world where GPU costs are paramount, squeezing efficiency out of every core is non-negotiable.</li>
</ul>
<h2 class="anchor anchorTargetStickyNavbar_Vzrq" id="what-we-needed-from-an-operator">What We Needed from an Operator<a class="hash-link" href="https://kserve.github.io/website/blog/production-grade-llm-inference-kserve-llm-d-vllm#what-we-needed-from-an-operator" title="Direct link to What We Needed from an Operator">​</a></h2>
<p>Running LLMs at scale demanded a purpose-built Kubernetes Operator designed for the intricacies of AI/ML. After evaluating the landscape, we identified a clear set of requirements:</p>
<ul>
<li class=""><strong>Full spec-level customization:</strong> We needed the ability to override the runtime specification beyond what typical Custom Resources expose — tailoring vLLM flags for specialized hardware and rapid iteration.</li>
<li class=""><strong>Flexible deployment patterns:</strong> Rather than being locked into a single prefill/decode architecture, we needed an operator that could adapt to our evolving serving topologies.</li>
<li class=""><strong>Standard Kubernetes API integration:</strong> The solution had to work with the Kubernetes API surface we already knew, not introduce an entirely new abstraction layer.</li>
</ul>
<h2 class="anchor anchorTargetStickyNavbar_Vzrq" id="the-winning-combination-kserve--llm-d--vllm">The Winning Combination: KServe + llm-d + vLLM<a class="hash-link" href="https://kserve.github.io/website/blog/production-grade-llm-inference-kserve-llm-d-vllm#the-winning-combination-kserve--llm-d--vllm" title="Direct link to The Winning Combination: KServe + llm-d + vLLM">​</a></h2>
<p><img alt="kserve-architecture" class="img_ev3q" height="540" src="https://kserve.github.io/website/assets/images/kserve-architecture-8672b33fd4c9370d856ad3b661303be6.webp" width="960" /></p>
<p>Our journey led us back to the most flexible and powerful solution: <a class="" href="https://github.com/llm-d/llm-d" rel="noopener noreferrer" target="_blank"><strong>llm-d</strong></a>, powered by <a class="" href="https://github.com/kserve/kserve" rel="noopener noreferrer" target="_blank"><strong>KServe</strong></a> and its cutting-edge <strong>Inference Gateway Extension</strong>.</p>
<p>This combination solved every scaling and operational challenge we faced by delivering:</p>
<ul>
<li class=""><strong>Deep Customization:</strong> The <strong>LLMInferenceService</strong> and <strong>LLMInferenceConfig</strong> objects expose the standard Kubernetes API, allowing us to override the spec precisely where needed. This level of granular control is crucial for tailoring vLLM to specialized hardware or quickly implementing flag changes.</li>
<li class=""><strong>Intelligent Routing and Efficiency:</strong> By leveraging <a class="" href="https://www.envoyproxy.io/" rel="noopener noreferrer" target="_blank"><strong>Envoy</strong></a>, <a class="" href="https://aigateway.envoyproxy.io/" rel="noopener noreferrer" target="_blank"><strong>Envoy AI Gateway</strong></a>, and <a class="" href="https://github.com/kubernetes-sigs/gateway-api-inference-extension" rel="noopener noreferrer" target="_blank"><strong>Gateway API Inference Extension</strong></a>, we moved far beyond round-robin. This technology enables <strong>prefix-cache aware routing</strong>, ensuring requests are intelligently routed to the correct vLLM instance to maximize KV-cache utilization and drive up GPU efficiency.</li>
</ul>
<p>On one deployment, we observed a <strong>3x improvement in output tokens/s</strong> and a <strong>2x reduction in time to first token (TTFT)</strong> after enabling prefix-cache aware routing. These numbers were measured when serving Llama 3.1 70B model on 4 MI300X AMD GPUs with the configuration: <code>tensor-parallel-size=4</code>, <code>gpu-memory-utilization=0.90</code>, and <code>--max-model-len=65536</code>. Below is the chart that shows the performance improvement after we released the routing change (at around 12:30PM).</p>
<p><img alt="performance-improvements" class="img_ev3q" height="1230" src="https://kserve.github.io/website/assets/images/performance-improvements-ec24748173796fc10ca0d74cd6b5b1da.png" width="3432" /></p>
<h2 class="anchor anchorTargetStickyNavbar_Vzrq" id="community-contributions-and-collaboration">Community Contributions and Collaboration<a class="hash-link" href="https://kserve.github.io/website/blog/production-grade-llm-inference-kserve-llm-d-vllm#community-contributions-and-collaboration" title="Direct link to Community Contributions and Collaboration">​</a></h2>
<p>Running this stack in production surfaced real issues that we fixed upstream in KServe, benefiting the broader community:</p>
<ul>
<li class=""><strong>New feature requests filed:</strong> <a class="" href="https://github.com/kserve/kserve/issues/4901" rel="noopener noreferrer" target="_blank">#4901</a>, <a class="" href="https://github.com/kserve/kserve/issues/4900" rel="noopener noreferrer" target="_blank">#4900</a>, <a class="" href="https://github.com/kserve/kserve/issues/4898" rel="noopener noreferrer" target="_blank">#4898</a>, <a class="" href="https://github.com/kserve/kserve/issues/4899" rel="noopener noreferrer" target="_blank">#4899</a></li>
<li class=""><strong>storageInitializer made optional</strong> (<a class="" href="https://github.com/kserve/kserve/pull/4970" rel="noopener noreferrer" target="_blank">kserve#4970</a>) — enabling RunAI Model Streamer as an alternative to the default storage initializer</li>
<li class=""><strong>Added support for latest Gateway API Inference Extension</strong> (<a class="" href="https://github.com/kserve/kserve/pull/4886" rel="noopener noreferrer" target="_blank">kserve#4886</a>)</li>
</ul>
<p>These contributions came directly from hitting production edge cases. Validating KServe and llm-d at this scale helped harden the platform for everyone running LLM workloads on Kubernetes.</p>
<h2 class="anchor anchorTargetStickyNavbar_Vzrq" id="acknowledgement">Acknowledgement<a class="hash-link" href="https://kserve.github.io/website/blog/production-grade-llm-inference-kserve-llm-d-vllm#acknowledgement" title="Direct link to Acknowledgement">​</a></h2>
<p>We'd like to thank everyone from the community who has contributed to the successful adoption of KServe, llm-d, and vLLM in Tesla's production environment. In particular, below is the list of people from Red Hat and Tesla teams who have helped through the process (in alphabetical order).</p>
<ul>
<li class=""><strong>Red Hat team</strong>: Sergey Bekkerman, Nati Fridman, Killian Golds, Andres Llausas, Bartosz Majsak, Greg Pereira, Pierangelo Di Pilato, Ran Pollak, Vivek Karunai Kiri Ragavan, Robert Shaw, and Yuan Tang</li>
<li class=""><strong>Tesla team</strong>: Scott Cabrinha and Sai Krishna</li>
</ul>
<h2 class="anchor anchorTargetStickyNavbar_Vzrq" id="get-involved-with-llm-d">Get Involved with llm-d<a class="hash-link" href="https://kserve.github.io/website/blog/production-grade-llm-inference-kserve-llm-d-vllm#get-involved-with-llm-d" title="Direct link to Get Involved with llm-d">​</a></h2>
<p>The work described here is just one example of what becomes possible when a community of engineers tackles hard problems together in the open. If you're running LLMs at scale and wrestling with the same challenges — storage, routing, efficiency, day-2 operations — we'd love to have you involved.</p>
<ul>
<li class=""><strong>Explore the code</strong> → Browse our <a class="" href="https://github.com/llm-d" rel="noopener noreferrer" target="_blank">GitHub organization</a> and dig into the projects powering this stack</li>
<li class=""><strong>Join our Slack</strong> → <a class="" href="https://llm-d.ai/slack" rel="noopener noreferrer" target="_blank">Get your invite</a> and connect directly with maintainers and contributors from Red Hat, Tesla, and beyond</li>
<li class=""><strong>Attend community calls</strong> → All meetings are open! Add our <a class="" href="https://red.ht/llm-d-public-calendar" rel="noopener noreferrer" target="_blank">public calendar</a> (Wednesdays 12:30pm ET) and join the conversation</li>
<li class=""><strong>Follow project updates</strong> → Stay current on <a class="" href="https://twitter.com/_llm_d_" rel="noopener noreferrer" target="_blank">Twitter/X</a>, <a class="" href="https://bsky.app/profile/llm-d.ai" rel="noopener noreferrer" target="_blank">Bluesky</a>, and <a class="" href="https://www.linkedin.com/company/llm-d" rel="noopener noreferrer" target="_blank">LinkedIn</a></li>
<li class=""><strong>Watch demos and recordings</strong> → Subscribe to the <a class="" href="https://www.youtube.com/@llm-d-project" rel="noopener noreferrer" target="_blank">llm-d YouTube channel</a> for community call recordings and feature walkthroughs</li>
<li class=""><strong>Read the docs</strong> → Visit our <a class="" href="https://llm-d.ai/docs/community" rel="noopener noreferrer" target="_blank">community page</a> to find SIGs, contribution guides, and upcoming events</li>
</ul>
