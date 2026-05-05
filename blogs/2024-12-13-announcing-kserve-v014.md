---
title: "Announcing KServe v0.14"
url: "https://kserve.github.io/website/blog/kserve-0.14-release"
date: "Fri, 13 Dec 2024 00:00:00 GMT"
author: ""
feed_url: "https://kserve.github.io/website/blog/rss"
---
<p><em>Published on December 23, 2024</em></p>
<p>We are excited to announce KServe v0.14. In this release we are introducing a new Python client designed for KServe, and a new model cache feature; we are promoting OCI storage for models as a stable feature; and we added support for deploying models directly from Hugging Face.</p>
<h2 class="anchor anchorTargetStickyNavbar_Vzrq" id="-key-features">🚀 Key Features<a class="hash-link" href="https://kserve.github.io/website/blog/kserve-0.14-release#-key-features" title="Direct link to 🚀 Key Features">​</a></h2>
<h3 class="anchor anchorTargetStickyNavbar_Vzrq" id="introducing-inference-client-for-python">Introducing Inference client for Python<a class="hash-link" href="https://kserve.github.io/website/blog/kserve-0.14-release#introducing-inference-client-for-python" title="Direct link to Introducing Inference client for Python">​</a></h3>
<p>The KServe Python SDK now includes both <a class="" href="https://github.com/kserve/kserve/blob/v0.14.0/python/kserve/kserve/inference_client.py#L388" rel="noopener noreferrer" target="_blank">REST</a> and <a class="" href="https://github.com/kserve/kserve/blob/v0.14.0/python/kserve/kserve/inference_client.py#L61" rel="noopener noreferrer" target="_blank">GRPC</a> inference clients. The new Inference clients of the SDK were delivered as <strong>alpha</strong> features.</p>
<p>Inline with the features documented in issue <a class="" href="https://github.com/kserve/kserve/issues/3270" rel="noopener noreferrer" target="_blank">#3270</a>, both clients have the following characteristics:</p>
<ul>
<li class="">The clients are asynchronous</li>
<li class="">Support for HTTP/2 (via <a class="" href="https://www.python-httpx.org/" rel="noopener noreferrer" target="_blank">httpx</a> library)</li>
<li class="">Support Open Inference Protocol v1 and v2</li>
<li class="">Allow client send and receive tensor data in binary format for HTTP/REST request, see <a class="" href="https://kserve.github.io/archive/0.14/modelserving/data_plane/binary_tensor_data_extension/" rel="noopener noreferrer" target="_blank">binary tensor data extension docs</a>.</li>
</ul>
<p>As usual, the version 0.14.0 of the KServe Python SDK is <a class="" href="https://pypi.org/project/kserve/0.14.0/" rel="noopener noreferrer" target="_blank">published to PyPI</a> and available to install via <code>pip install</code>.</p>
<h3 class="anchor anchorTargetStickyNavbar_Vzrq" id="support-for-oci-storage-for-models-modelcars-becomes-stable">Support for OCI storage for models (modelcars) becomes stable<a class="hash-link" href="https://kserve.github.io/website/blog/kserve-0.14-release#support-for-oci-storage-for-models-modelcars-becomes-stable" title="Direct link to Support for OCI storage for models (modelcars) becomes stable">​</a></h3>
<p>In KServe version 0.12, support for using OCI containers for model storage was introduced as an experimental feature. This allows users to store models in containers in OCI format, and allows the usage of OCI-compatible registries for publishing the models.</p>
<p>This feature was implemented by configuring the OCI model container as a sidecar in the InferenceService pod, which was the motivation for naming the feature as modelcars. The model files are made available to the model server by configuring <a class="" href="https://kubernetes.io/docs/tasks/configure-pod-container/share-process-namespace/" rel="noopener noreferrer" target="_blank">process namespace sharing</a> in the pod.</p>
<p>There was one small but important detail that was unsolved and motivated the experimental status: since the modelcar is part of the main containers of the pod, there was no certainty that the modelcar would start quickly. The model server would be unstable if it starts first than the modelcar, and since there was no prefetching of the model image, this was thought as a likely condition.</p>
<p>The unstable situation has been mitigated by configuring the OCI model as an init container in addition to also configuring it as a sidecar. The configuration as an init container ensures that the model is fetched before the main containers are started. The prefetching allows the modelcar to start quickly.
The stabilization is available since KServe version 0.14, where modelcars are now a stable feature.</p>
<h4 class="anchor anchorTargetStickyNavbar_Vzrq" id="future-plan">Future plan<a class="hash-link" href="https://kserve.github.io/website/blog/kserve-0.14-release#future-plan" title="Direct link to Future plan">​</a></h4>
<p>Modelcars is one implementation option for supporting OCI images for model storage. There are other alternatives commented in <a class="" href="https://github.com/kserve/kserve/issues/4083" rel="noopener noreferrer" target="_blank">issue #4083</a>.</p>
<p>Using volume mounts based on OCI artifacts is the optimal implementation, but this is only <a class="" href="https://kubernetes.io/blog/2024/08/16/kubernetes-1-31-image-volume-source/" rel="noopener noreferrer" target="_blank">recently possible since Kubernetes 1.31</a> as a native alpha feature. KServe can now evolve to use this new Kubernetes feature.</p>
<h3 class="anchor anchorTargetStickyNavbar_Vzrq" id="introducing-model-cache">Introducing Model Cache<a class="hash-link" href="https://kserve.github.io/website/blog/kserve-0.14-release#introducing-model-cache" title="Direct link to Introducing Model Cache">​</a></h3>
<p>With models increasing in size, specially true for LLM models, pulling from storage each time a pod is created can result in unmanageable start-up times. Although OCI storage also has the benefit of model caching, the capabilities are not flexible since the management is delegated to the cluster.</p>
<p>The Model Cache was proposed as another alternative to enhance KServe usability with big models, released in KServe v0.14 as an <strong>alpha</strong> feature.
In this release local node storage is used for storing models and <code>LocalModelCache</code> custom resource provides the control about which models to store in the cache.
The local model cache state can always be rebuilt from the models stored on persistent storage like model registry or S3.
Read the <a class="" href="https://docs.google.com/document/d/1nao8Ws3tonO2zNAzdmXTYa0hECZNoP2SV_z9Zg0PzLA/edit" rel="noopener noreferrer" target="_blank">design document for the details</a>.</p>
<p><img alt="!localmodelcache" class="img_ev3q" height="1416" src="https://kserve.github.io/website/assets/images/localmodelcache-59f819fe261fb8fcd66a6c875a73b3d6.png" width="2462" /></p>
<p>By caching the models, you get the following benefits:</p>
<ul>
<li class="">
<p>Minimize the time it takes for LLM pods to start serving requests.</p>
</li>
<li class="">
<p>Sharing the same storage for pods scheduled on the same GPU node.</p>
</li>
<li class="">
<p>Model Cache allows scaling your AI workload efficiently without worrying about the slow model server container startup.</p>
</li>
</ul>
<p>The model cache is currently disabled by default. To enable, you need to modify the <code>localmodel.enabled</code> field on the <code>inferenceservice-config</code> ConfigMap.</p>
<p>You can follow <a class="" href="https://kserve.github.io/archive/0.14/modelserving/storage/modelcache/localmodel/" rel="noopener noreferrer" target="_blank">local model cache tutorial</a> to cache LLMs on local NVMe of your GPU nodes and deploy LLMs with <code>InferenceService</code> by loading models from local cache to accelerate the container startup.</p>
<h3 class="anchor anchorTargetStickyNavbar_Vzrq" id="support-for-hugging-face-hub-in-storage-initializer">Support for Hugging Face hub in storage initializer<a class="hash-link" href="https://kserve.github.io/website/blog/kserve-0.14-release#support-for-hugging-face-hub-in-storage-initializer" title="Direct link to Support for Hugging Face hub in storage initializer">​</a></h3>
<p>The KServe storage initializer has been enhanced to support downloading models directly from Hugging Face. For this, the new schema <code>hf://</code> is now supported in the <code>storageUri</code> field of InferenceServices. The following YAML partial shows this:</p>
<div class="language-yaml codeBlockContainer_Ckt0 theme-code-block"><div class="codeBlockContent_QJqH"><pre class="prism-code language-yaml codeBlock_bY9V thin-scrollbar" style="color: #393A34; background-color: #f6f8fa;" tabindex="0"><code class="codeBlockLines_e6Vv"><span class="token-line" style="color: #393A34;"><span class="token key atrule" style="color: #00a4db;">apiVersion</span><span class="token punctuation" style="color: #393A34;">:</span><span class="token plain"> serving.kserve.io/v1beta1</span><br /></span><span class="token-line" style="color: #393A34;"><span class="token plain"></span><span class="token key atrule" style="color: #00a4db;">kind</span><span class="token punctuation" style="color: #393A34;">:</span><span class="token plain"> InferenceService</span><br /></span><span class="token-line" style="color: #393A34;"><span class="token plain"></span><span class="token key atrule" style="color: #00a4db;">metadata</span><span class="token punctuation" style="color: #393A34;">:</span><span class="token plain"></span><br /></span><span class="token-line" style="color: #393A34;"><span class="token plain">  </span><span class="token key atrule" style="color: #00a4db;">name</span><span class="token punctuation" style="color: #393A34;">:</span><span class="token plain"> huggingface</span><span class="token punctuation" style="color: #393A34;">-</span><span class="token plain">llama3</span><br /></span><span class="token-line" style="color: #393A34;"><span class="token plain"></span><span class="token key atrule" style="color: #00a4db;">spec</span><span class="token punctuation" style="color: #393A34;">:</span><span class="token plain"></span><br /></span><span class="token-line" style="color: #393A34;"><span class="token plain">  </span><span class="token key atrule" style="color: #00a4db;">predictor</span><span class="token punctuation" style="color: #393A34;">:</span><span class="token plain"></span><br /></span><span class="token-line" style="color: #393A34;"><span class="token plain">    </span><span class="token key atrule" style="color: #00a4db;">model</span><span class="token punctuation" style="color: #393A34;">:</span><span class="token plain"></span><br /></span><span class="token-line" style="color: #393A34;"><span class="token plain">      </span><span class="token key atrule" style="color: #00a4db;">storageUri</span><span class="token punctuation" style="color: #393A34;">:</span><span class="token plain"> hf</span><span class="token punctuation" style="color: #393A34;">:</span><span class="token plain">//meta</span><span class="token punctuation" style="color: #393A34;">-</span><span class="token plain">llama/meta</span><span class="token punctuation" style="color: #393A34;">-</span><span class="token plain">llama</span><span class="token punctuation" style="color: #393A34;">-</span><span class="token plain">3</span><span class="token punctuation" style="color: #393A34;">-</span><span class="token plain">8b</span><span class="token punctuation" style="color: #393A34;">-</span><span class="token plain">instruct</span><br /></span></code></pre></div></div>
<p>Both public and private Hugging Face repositories are supported. The credentials can be provided by the usual mechanism of binding Secrets to ServiceAccounts, or by binding the credentials Secret as environment variables in the InferenceService.</p>
<p>Read the <a class="" href="https://kserve.github.io/archive/0.14/modelserving/storage/huggingface/hf/" rel="noopener noreferrer" target="_blank">documentation</a> for more details.</p>
<h2 class="anchor anchorTargetStickyNavbar_Vzrq" id="️-enhancements-and-improvements">🛠️ Enhancements and Improvements<a class="hash-link" href="https://kserve.github.io/website/blog/kserve-0.14-release#%EF%B8%8F-enhancements-and-improvements" title="Direct link to 🛠️ Enhancements and Improvements">​</a></h2>
<h3 class="anchor anchorTargetStickyNavbar_Vzrq" id="hugging-face-vllm-backend-changes">Hugging Face vLLM backend changes<a class="hash-link" href="https://kserve.github.io/website/blog/kserve-0.14-release#hugging-face-vllm-backend-changes" title="Direct link to Hugging Face vLLM backend changes">​</a></h3>
<ul>
<li class="">vLLM backend to update to 0.6.1 <a class="" href="https://github.com/kserve/kserve/pull/3948" rel="noopener noreferrer" target="_blank">#3948</a></li>
<li class="">Support trust_remote_code flag for vllm <a class="" href="https://github.com/kserve/kserve/pull/3729" rel="noopener noreferrer" target="_blank">#3729</a></li>
<li class="">Support text embedding task in hugging face server <a class="" href="https://github.com/kserve/kserve/pull/3743" rel="noopener noreferrer" target="_blank">#3743</a></li>
<li class="">Add health endpoint for vLLM backend <a class="" href="https://github.com/kserve/kserve/pull/3850" rel="noopener noreferrer" target="_blank">#3850</a></li>
<li class="">Added <code>hostIPC</code> field to <code>ServingRuntime</code> CRD, for supporting more than one GPU in Serverless mode <a class="" href="https://github.com/kserve/kserve/issues/3791" rel="noopener noreferrer" target="_blank">#3791</a></li>
<li class="">Support shared memory volume for vLLM backend <a class="" href="https://github.com/kserve/kserve/pull/3910" rel="noopener noreferrer" target="_blank">#3910</a></li>
</ul>
<h3 class="anchor anchorTargetStickyNavbar_Vzrq" id="other-enhancements">Other Enhancements<a class="hash-link" href="https://kserve.github.io/website/blog/kserve-0.14-release#other-enhancements" title="Direct link to Other Enhancements">​</a></h3>
<ul>
<li class="">New flag for automount serviceaccount token by <a class="" href="https://github.com/kserve/kserve/pull/3979" rel="noopener noreferrer" target="_blank">#3979</a></li>
<li class="">TLS support for inference loggers <a class="" href="https://github.com/kserve/kserve/issues/3837" rel="noopener noreferrer" target="_blank">#3837</a></li>
<li class="">Allow PVC storage to be mounted in ReadWrite mode via an annotation <a class="" href="https://github.com/kserve/kserve/issues/3687" rel="noopener noreferrer" target="_blank">#3687</a></li>
<li class="">Support HTTP Headers passing for KServe python custom runtimes <a class="" href="https://github.com/kserve/kserve/pull/3669" rel="noopener noreferrer" target="_blank">#3669</a></li>
</ul>
<h2 class="anchor anchorTargetStickyNavbar_Vzrq" id="️-whats-changed">⚠️ What's Changed<a class="hash-link" href="https://kserve.github.io/website/blog/kserve-0.14-release#%EF%B8%8F-whats-changed" title="Direct link to ⚠️ What's Changed">​</a></h2>
<ul>
<li class="">Ray is now an optional dependency <a class="" href="https://github.com/kserve/kserve/pull/3834" rel="noopener noreferrer" target="_blank">#3834</a></li>
<li class="">Support for Python 3.12 is added, while support Python 3.8 is removed <a class="" href="https://github.com/kserve/kserve/pull/3645" rel="noopener noreferrer" target="_blank">#3645</a></li>
</ul>
<h2 class="anchor anchorTargetStickyNavbar_Vzrq" id="-release-notes">🔍 Release Notes<a class="hash-link" href="https://kserve.github.io/website/blog/kserve-0.14-release#-release-notes" title="Direct link to 🔍 Release Notes">​</a></h2>
<p>For complete release notes including all changes, bug fixes, and known issues, visit the <a class="" href="https://github.com/kserve/kserve/releases/tag/v0.14.0" rel="noopener noreferrer" target="_blank">GitHub release page</a>.</p>
<h2 class="anchor anchorTargetStickyNavbar_Vzrq" id="-acknowledgments">🙏 Acknowledgments<a class="hash-link" href="https://kserve.github.io/website/blog/kserve-0.14-release#-acknowledgments" title="Direct link to 🙏 Acknowledgments">​</a></h2>
<p>We want to thank all the contributors who made this release possible:</p>
<ul>
<li class=""><strong>Core Contributors</strong>: The KServe maintainers and regular as well as new contributors</li>
<li class=""><strong>Community</strong>: Everyone who reported issues, provided feedback, and tested features</li>
</ul>
<h2 class="anchor anchorTargetStickyNavbar_Vzrq" id="-join-the-community">🤝 Join the community<a class="hash-link" href="https://kserve.github.io/website/blog/kserve-0.14-release#-join-the-community" title="Direct link to 🤝 Join the community">​</a></h2>
<ul>
<li class="">Visit our <a class="" href="https://kserve.github.io/website/" rel="noopener noreferrer" target="_blank">Website</a> or <a class="" href="https://github.com/kserve" rel="noopener noreferrer" target="_blank">GitHub</a></li>
<li class="">Join the Slack (<a class="" href="https://github.com/kserve/community?tab=readme-ov-file#questions-and-issues" rel="noopener noreferrer" target="_blank">#kserve</a>)</li>
<li class="">Attend our community meeting by subscribing to the <a class="" href="https://zoom-lfx.platform.linuxfoundation.org/meetings/kserve?view=month" rel="noopener noreferrer" target="_blank">KServe calendar</a>.</li>
<li class="">View our <a class="" href="https://github.com/kserve/community" rel="noopener noreferrer" target="_blank">community github repository</a> to learn how to make contributions. We are excited to work with you to make KServe better and promote its adoption!</li>
</ul>
<hr />
<p><em>The KServe team is committed to making machine learning model serving simple, scalable, and standardized. Thank you for being part of our community!</em></p>
