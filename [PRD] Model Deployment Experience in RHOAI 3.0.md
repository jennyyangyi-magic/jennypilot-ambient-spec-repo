# Model Deployment Wizard in RHOAI 3.0

| Created | Jul 3, 2025 |
| :---- | :---- |
| **Last Updated** | Jul 3, 2025 |
| **Resolved** | Discovery/WIP |
| **Authors** | [Jenny Yi](mailto:yyi@redhat.com)[Adam Bellusci](mailto:abellusc@redhat.com) |
| **Relevant Docs/Artifacts** | [https://miro.com/app/board/uXjVITZX0EE=/](https://miro.com/app/board/uXjVITZX0EE=/)  |
| **Replaces** |  |
| **Replaced by** |  |
| **Jira** | [RHOAIENG-22487](https://issues.redhat.com/browse/RHOAIENG-22487) Need to create RHAIRFE  |

# Problem Context

Components: 

* K-serve  
* Vllm  
* llm-d  
* MaaS\*  
  * Not a component but a feature

Stakeholders

* PM  
  * Adam  
  * Naina (llm-d)  
  * Jonathan (MaaS and Observability)  
    * [Model-as-a-Service Worksheet](https://docs.google.com/document/d/142X3mx_SIdSWMvgf3ppSW83J__ZtQ4EDmOiF0IKZYJc/edit?tab=t.0)  
* Eng  
  * Daniele Zonca  
* UXD  
  * Vince Conzola

Open Discussions

* Static, admin creates the hardware profiles  
  * Avoid creating a hardware profiles for every scenario  
    * Flow of creating a hardware profile with recommendation  
  * Pre-defined hardware profiles by platform admin  
    * Closest hardware recommendation to the profile  
  * Originally for notebooks and workbenches  
* Who are the intended users of hardware profiles?  
  * **Data scientists**, AI engineers  
  * Cluster admin creates hardware profiles  
* Who gets to create hardware profiles:  
  * Admin  
    * Knows the cluster  
* Who gets to deploy a model?  
  * Admin only?  
  * End-user?   
    * It seems like hardware profiles is especially beneficial for those who don’t understand the cluster set up/hardware availability   
* Hardware profile connection with model validation  
  * Model validation:  
    * Is it possible to associate hardware profile templates with    
  * Questions  
    * How are users aware of whats in the cluster   
* Llm-d infiniband requirement  
  * Key-value pairs  
  * As long as RESTFUL kubernetes, should work

* Pre-defined, meaningful set of hardware profiles  
  * Match existing cloud provider options  
  * Hardware profile always a superset  
    * Hardware profile should always have more resources than recommended minimum  
  * How does hardware profiles get set up  
    * Check-box of things to set up  
    * UI   
* Recommended hardware profile after selecting a model   
* Model validation recommendation \-\> export into a hardware profile  
  * If admin persona \-\> they’ll know whats in the cluster  
  * If end user \-\> won’t know  
  * Filter for model selection and hardware recommendation results because of hardware availability   
  * Defining/integrating Kueue: quota management  
    * Counter for available resources  
    * Put on hold   
    * Enable: node affinity

Ideal scenario:

Red Hat ships recommended hardware profiles as “t-shirt sizes” for model deployments

* Llama 3.3  70B \-\> hardware profile of gpu.a100-4x.large

```py
apiVersion: accelerators.opendatahub.io/v1alpha
kind: HardwareProfile
metadata:
  name: gpu.a100-4x.large
spec:
  displayName: "4x A100 80GB High-Memory GPU"
  description: "Use for large models like LLaMA 3.3 70B, optimized for tensor parallel inference"
  resources:
    limits:
      cpu: "32"
      memory: "512Gi"
      nvidia.com/gpu: 4
    requests:
      cpu: "16"
      memory: "256Gi"
      nvidia.com/gpu: 4
  nodeSelector:
    node-type: gpu-a100
    gpu.memory: "80Gi"
  tolerations:
    - key: "nvidia.com/gpu"
      operator: "Exists"
      effect: "NoSchedule"
  priority: 10
```

* Model validation tests the same hardware scenarios as the hardware profiles we recommend  
  * Single server  
  * multi-node/distributed

User Model selection:

* When listing configs that we’ve tested, cross-check if there is existing hardware profile that matches 

\-\> Matching HWP to Jounce HW Configurations:

* Hardware profiles:  
  * 

User configure model deployment:

* User selects a model  
* Inputs expected traffic/RPS, SLO/Use Case  
  * TTFT \<200ms  
  * RPS of 10,000 RPS  
* We can recommend t-shirt sizes hardware profiles for selected model and replicas   
  * “Recommended hardware profiles (created by the Admin)”  
    * Theres no hardware profile exist, contact your administrator   
  * Heres the other

GPU Sizing

* If a user wants to load a model that is too big for the selected hardware profile

Questions:

* Can we recommend multiple vendors so its not NVIDIA specific  
  * First principle: Democratize accelerators  
    * How do we make AMD work as well?  
* Hardware recommendation  
  * Model Validation hardware scenarios, batch job:  
    * 8xH100  
    * 4xH100  
  *   
  * 

# Features

## Enhancements to Model Deployment Wizard

**Feature Overview:**  
*An elevator pitch (value statement) that describes the Feature in a clear, concise way. ie: Executive Summary of the user goal or problem that is being solved, why does this matter to the user? The “What & Why”...* 

* Text

**Goals:**

*Provide high-level goal statement, providing user context and expected user outcome(s) for this Feature. Who benefits from this Feature, and how? What is the difference between today’s current state and a world with this Feature?*

* Text

**Out of Scope:**

*High-level list of items or persona’s that are out of scope.*

* Text

**Requirements:**

*A list of specific needs, capabilities, or objectives that a Feature must deliver to satisfy the Feature. Some requirements will be flagged as MVP. If an MVP gets shifted, the Feature shifts. If a non MVP requirement slips, it does not shift the feature.*

* Text

**Done \- Acceptance Criteria:**

*Acceptance Criteria articulates and defines the value proposition \- what is required to meet the goal and intent of this Feature. The Acceptance Criteria provides a detailed definition of scope and the expected outcomes \- from a users point of view*

* Text

**Use Cases \- i.e. User Experience & Workflow:**

*Include use case diagrams, main success scenarios, alternative flow scenarios.*

* Text

**Documentation Considerations:**

*Provide information that needs to be considered and planned so that documentation will meet customer needs. If the feature extends existing functionality, provide a link to its current documentation..*

* Text

**Questions to answer:**

*Include a list of refinement / architectural questions that may need to be answered before coding can begin.*

* Text

**Background & Strategic Fit:**

*Provide any additional context is needed to frame the feature.*

* Text

**Customer Considerations**

*Provide any additional customer-specific considerations that must be made when designing and delivering the Feature.*

* Text