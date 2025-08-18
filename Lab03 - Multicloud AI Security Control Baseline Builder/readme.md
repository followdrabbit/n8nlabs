## What this template does

Transforms provider documentation (URLs) into an **auditable security baseline**. It:

* Fetches and sanitizes HTML
* Uses AI to **extract security requirements** (strict 3-line TXT blocks)
* **Composes enforceable controls** (strict 7-line TXT blocks with true-equivalence consolidation)
* **Builds a final baseline** (TXT) with a `Technology:` header
* Returns a downloadable `.txt` via webhook and can **append/create** the file in Google Drive

## Why it’s useful

Eliminates manual copy-paste from docs and produces a consistent, portable baseline ready for review, audit, or enforcement tooling. Ideal for rapidly generating or refreshing baselines across cloud providers or services.

## Multicloud support

The workflow is **multicloud by design**. Pass the target cloud in the request and route the same pipeline for:

* **AWS**, **Azure**, **GCP** (out of the box)
* Extensible to other providers/services by adjusting prompts and routing logic

## How it works (high level)

1. `POST /create` (Basic Auth) with `{ cloudProvider, technology, urls[] }`
2. Resolve Google Drive folder (search-or-create) and generate a per-run `uuid`
3. Download & sanitize each URL
4. AI pipeline: **Extractor → Composer → Baseline Builder** (TXT-only contracts)
5. Append or create file in Drive and return a **downloadable .txt**

## Inputs

```json
{
  "cloudProvider": "AWS",
  "technology": "Amazon S3",
  "urls": [
    "https://docs.aws.amazon.com/AmazonS3/latest/userguide/security-best-practices.html"
  ]
}
```

## Outputs

* **File:** `controls_<technology>_<timestamp>.txt` (downloaded from the webhook)
* **If nothing valid:** JSON with `NO_CONTROLS_FOUND` and troubleshooting hints

## Credentials

* **OpenAI** (kept in n8n’s Credential Manager; no API keys in HTTP headers)
* **Google Drive OAuth2** (optional file operations)
* **Basic Auth** (protects the webhook endpoint)

## Customization & extensions

This template is intentionally modular and can be extended to match your governance model:

* **Prompt-reflective techniques:** add reflection/revision passes to increase precision, reduce hallucination, and enforce stricter formats.
* **Compliance assistants:** plug additional assistants to analyze/label controls against frameworks like **HIPAA, PCI DSS, SOX** (and others), emitting mappings, gaps, and remediation notes.
* **Implementation context:** feed internal implementation docs, runbooks, design records, or **Architecture Decision Records (ADRs)**; have the pipeline extract requirements from these sources and **use them as grounding** for new/updated controls.
* **Local/self-hosted LLMs:** swap the OpenAI nodes for a local LLM endpoint (self-hosted) to keep data on-prem while preserving the pipeline.
* **Provider-specific outputs:** extend the final stage to export Policy-as-Code or IaC snippets (e.g., Rego/Sentinel rules, CloudFormation Guard, ARM/Bicep, Terraform validations).
* **Threat-model tags:** include STRIDE/mitigation tags or risk scoring fields in the 7-line control blocks if your process requires it.

## Security & privacy

* No hardcoded secrets in HTTP nodes; use n8n’s Credential Manager.
* Drive operations are optional and folder-scoped.
* For sensitive environments, switch to a local LLM and provide only sanitized/approved inputs.

## Notes

* Sticky Notes on the canvas summarize **Overview**, **Setup & Credentials**, and **Run & Troubleshooting**.
* Works best with documentation pages that return clean HTML; large/JS-heavy pages may require longer HTTP timeouts.
