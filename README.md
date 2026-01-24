# AI Agent Architect #
AI Agent Architect with expertise in reviewing document-driven projects, assessing and enforcing cloud best practices (across Microsoft Azure, Amazon AWS, Oracle Cloud and Google Cloud), and producing accurate, FinOps-aligned cost estimates to optimize cloud spend and governance.

## Why an AI Agent Architect? ##

Many customers are multi‑cloud today, and IT teams face several challenges:

- Growing complexity: Multi‑cloud architectures are becoming more complex every day. It’s difficult to design the right solutions without strong, hands‑on expertise.
- Cost estimation: Estimating costs across multiple projects is tough but essential to build a solid FinOps strategy.
- Time‑consuming reviews: Analyzing projects for best practices and cost optimization takes significant time, and you need to accelerate this work to keep up with IT demand.

Recent AI models (especially since GPT‑3.5) have greatly improved the analysis process with high accuracy. This setup references ChatGPT 5.2, but you can easily switch to newer models as they become available. Another area that has advanced significantly is diagram generation — with better support for C4, flowcharts, and similar notations.

## How the Agent works for this scenario ##

Normally, IT teams prepare documents that describe the architecture or planned deployments in formats like *.DOCX or *.PDF. This solution can extract information from the text inside these documents, and it can also analyze diagrams if they are included (for example, a proposed architecture or change diagram).
Other file types that can be analyzed (with different output quality):

- Terraform (.tf): If you submit.tf files, the output will be more precise, because Terraform requires you to specify the exact instance sizes and service configurations.
- YAML (Kubernetes scenarios): The solution can provide best practices according to the cloud provider, but it cannot estimate costs unless you include a pricing reference file in the internal knowledge base.
- Diagrams (JPEG, PNG, etc.): If the image clearly specifies all parameters (instance sizes, regions, tiers, etc.), the results can be almost as accurate. This is useful for customers who prefer to draw the full solution visually.

If the document includes estimated volumetry (for example, users per day, requests per second, data size, retention time), the architecture and cost estimates will be more accurate. It can be difficult to provide these numbers at the start of a project, but they lead to much better results.

This solution is a good example of how to use a multi‑agent architecture to solve the problem, using Microsoft Copilot Studio.


![Diagram](img/diagram.png)

1. User submission → AI Agent Architect (Copilot Studio)
- Supported file types: DOCX, PDF, Terraform, PNG, YAML
- Action: Parse, extract intent (providers, CAF/WAF hints, pricing clues, diagrams).

2. Analyze & route to up to four cloud agents:

- Microsoft Azure Agent (via MCP server of public docs)
- Amazon AWS Agent (via MCP server of public docs)
- Oracle Cloud OCI Agent (via public website — CAF/WAF)
- Google Cloud GCP Agent (via public website — CAF/WAF)

Microsoft and Amazon offer MCP servers for their technical libraries for free, and you can connect to them at no cost. As of the date of this publication, I have not found MCP servers from Google Cloud or Oracle Cloud (specifically for technical libraries, not for their cloud services).
As a workaround, I am connecting to the publicly available technical documentation on their websites. It is not required to use MCP servers to access technical documentation.

This demo connects to the CAF (Cloud Adoption Framework) and WAF (Well‑Architected Framework), which are the recommended reference frameworks from these cloud providers.


3. Each agent performs:

- Best practice checks: CAF/WAF, security, resiliency, operations.

4. Cost estimation:

- If the document contains a pricing list → estimate from it.
Else → pull public pricing to estimate.

Many enterprises with large cloud contracts receive special discounts for certain services, instance types, regions, and more.
This repository does not include example pricing files. However, you can upload your invoice or spreadsheet with your custom pricing as Knowledge in Copilot Studio for each Agent (see details below).
Doing this allows the Agents to reference your negotiated rates when estimating costs—so results better reflect your real‑world pricing.

5. C4 diagramming:

- Every agent can emit C4 diagrams. For multi‑cloud documents, multiple agents run in parallel and their models are aggregated.

6. Final results back to the user:

- Best‑practices aligned with each provider’s CAF/WAF
- C4 diagrams
- Estimated costs

## Using Copilot Studio with Azure Credits ##

This solution use Microsoft Copilot Studio as the platform. I strongly recommend because it enables to use advanced features (connecting to MCP servers, publish on Microsoft Teams, etc) but it's possible to use Microsoft Copilot Chat  (but with limitations).
If you have a Microsoft Azure Subscription then it's possible to consume Azure credits for Copilot Studio. Please check the links bellow for more information:

- [Copilot Studio - Pay-as-you-go pricing](https://azure.microsoft.com/en-us/pricing/details/copilot-studio/)
- [Manage Copilot Studio credits and capacity](https://learn.microsoft.com/en-us/power-platform/admin/manage-copilot-studio-messages-capacity)

# Step 0 - Get Access to Copilot Studio #

If you never tried Copilot Studio before then I recommend to follow these steps described here:
- Get access to [Copilot Studio](https://learn.microsoft.com/en-us/microsoft-copilot-studio/requirements-licensing-subscriptions)

# Step 1 - Create your agent #

1. Open your browser and access Copilot Studio using https://copilotstudio.microsoft.com 

![Open Copilot Studio](img/step11.png)

2. On the left side, click **Agents**, and then on the right side, click  **+ Create blank agent** . This will start the wizard process.

![Create blank agent](img/step12.png)

3. In **Details**, click the **Edit** button and provide a **Name** for your agent (e.g., AI Agent Architect) and a **Description**. You can also upload an image file for the **Icon**.

![Details](img/step13.png)

4. Select the agent model. **GPT-5 Reasoning** offer great results and explanation but you can try other newest model. 

![Model](img/step14.png)


