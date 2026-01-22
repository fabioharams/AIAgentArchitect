# AI Agent Architect
AI Agent Architect with expertise in reviewing document-driven projects, assessing and enforcing cloud best practices (across Microsoft Azure, Amazon AWS, Oracle Cloud and Google Cloud), and producing accurate, FinOps-aligned cost estimates to optimize cloud spend and governance.

# Why an AI Agent Architect? #

Many customers are multi-cloud today and the IT teams are facing many challenges like:

- Multi-cloud architectures are becoming each day more complex and it's hard to learn and design right solutions without a strong knowledge.
- Estimate costs for many projects is a difficult part of the process but necessary if you want to establish a FinOps strategy.
- Time to analyse these projects for best-practices and cost analysis takes a lot of time and you need to accelerate to avoid impact on IT demands. 

The new AI Models (specially after GPT 3.5) increased a lot the analysis proccess, with great accuracy. This setup is referencing to ChatGPT 5.2 but of course you can easily change to new models. One of the challenges. Other technology that improved a lot was the engine to draw diagrams (following C4, fluxogram, etc).

# How the Agent works for this scenario #

Normally the IT Teams develop documents with the architecture or planned deployments in a document format (*.DOCX or *.PDF). This solution can extract information from text inside these documents but also can analyse diagrams if present (for example a diagram of proposed architecture/change). 
Other files that can be analysed but with different outputs:

- TF (Terraform files): if you submit *.TF files than the output will be much more precise, because Terraform require to specificy the exactly instance size of the services. 
- YAML (scenarios for Kubernetes): this solution can provide best practices according to Cloud Provider, but will not be able to specify costs, unless you include a file  in the knowledge base to be used internally for pricing reference. 
- Diagram (JPEG, etc): if you specify all the parameters in a image (instance size, etc) you can have almost the same result. This option is interesting for customers that has the practice of drwing all the solution in a visual way. 

If the document contains estimated volumetry then more accurate will be the architecture and estimated costs. Maybe this is very difficult to estimate when the project begins but brings an accurate result.

![Diagram](img/diagram.png)

1) User submission → AI Agent Architect (Copilot Studio)
- Supported file types: DOCX, PDF, Terraform, PNG, YAML
- Action: Parse, extract intent (providers, CAF/WAF hints, pricing clues, diagrams).

2) Analyze & route to up to four cloud agents:

- Microsoft Azure Agent (via MCP server of public docs)
- Amazon AWS Agent (via MCP server of public docs)
- Oracle Cloud OCI Agent (via public website — CAF/WAF)
- Google Cloud GCP Agent (via public website — CAF/WAF)

3) Each agent performs:

- Best practice checks: CAF/WAF, security, resiliency, operations.

4) Cost estimation:

- If the document contains a pricing list → estimate from it.
Else → pull public pricing to estimate.

5) C4 diagramming:

- Every agent can emit C4 diagrams. For multi‑cloud documents, multiple agents run in parallel and their models are aggregated.

6) Final results back to the user:

- Best‑practices aligned with each provider’s CAF/WAF
- C4 diagrams
- Estimated costs