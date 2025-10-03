# n8n Automations by Didi

A small library of production-tested n8n workflows I run for clients and for my own stack. Each flow blends webhooks, external APIs, and large-language-model agents to close a specific gap in marketing or RevOps processes.

## Automation Catalog

### Airtable · Claude · DeepL Translation Agent
- **File**: `Airtable-Claude-DeepL Translation Agent Workflow.json`
- **Trigger & Inputs**: POST webhook at `translationreq`; Airtable record ID, source text, target language label, tone, use case, translation style.
- **Flow Highlights**: Stamps Airtable status to "Translating (DeepL)", maps human language names to DeepL codes, runs DeepL and Claude in parallel, injects ROSENTAL Organics brand guardrails, then asks a "Final Comparing Agent" to fuse the best of both translations.
- **Outputs**: Updates the originating Airtable row (`Translation Requests` table) with DeepL/Claude/raw comparison, the polished final copy, title headline, and an explanation of revisions.
- **Resilience**: Dedicated branches capture DeepL/Claude/final-agent errors, push readable diagnostics back to Airtable, and prevent stalled jobs by marking the record status accordingly.
- **Dependencies**: Airtable token with write scope, DeepL API key, Anthropic Claude Sonnet 4 via n8n LangChain nodes.

### Instagram Lead Personalized Email Generator
- **File**: `Instagram Lead Personalized Email Generator.json`
- **Trigger & Inputs**: POST webhook at `samsurvey`; survey answers (business type, goals, revenue), respondent email, Instagram handle, attribution IP.
- **Flow Highlights**: Screens out low-value geographies with an IP lookup, normalises the Instagram handle, launches an Apify Instagram-scraper actor, waits for dataset readiness, then feeds survey answers + live profile stats into an LLM briefed to write a 50–80 word outreach email that sounds like "Sam".
- **Outputs**: Sends HTML-formatted email content through LeadConnector (`/hooks/.../708ae76a...`), mirrors a markdown-safe version to Telegram for QA, and keeps original + cleaned handles for auditing.
- **Quality Controls**: LLM returns `NOT ENOUGH INFORMATION` when inputs are incomplete; an IF gate blocks delivery and surfaces the case for manual follow-up.
- **Dependencies**: Apify actor token, OpenRouter Anthropic credentials, LeadConnector webhook, Telegram bot token/chat ID. Update the country allow/deny lists in the `Country Check` code node to reflect your lead strategy.

### Zoho CRM LLM Lead Enrich Agent
- **File**: `ZohoCRM LLM Lead Enrich Agent.json`
- **Trigger & Inputs**: POST webhook at `leadenrich523213`; Zoho lead ID, lead name, company, optional website and LinkedIn URL.
- **Flow Highlights**: Introduces a random 10–120s delay to fan out load, checks a local n8n Data Table to avoid reprocessing the same name/company, then orchestrates three research passes through OpenRouter (Perplexity Sonar Pro, Claude Sonnet, Gemini 2.5). Each pass must return strict JSON; custom parsers strip markdown fences and citation markers.
- **Intelligence Layer**: A scoring code node compares the LLM outputs field-by-field, rewards specificity (dates, roles, sector keywords), merges the strongest answer set, and records which model won.
- **Outputs**: Updates Zoho CRM custom fields (`Company_Summary`, `Investment_Sectors_LLM`, `Ticket_Size_LLM`, `Investment_Stage_LLM1`, `Joining_Firm`, `Investment_Criteria`) and core fields (`Designation`, `Description`), then logs the processed lead into the data table for dedupe.
- **Dependencies**: Zoho OAuth app with lead write scope, OpenRouter API key, n8n Data Tables project (`stored leadnames dedupe`). Adjust the Zoho field IDs and data table ID to fit your environment.

## Shared Setup
- Import any JSON file into n8n (`Workflows → Import from file`).
- Rebind credentials: Airtable, Anthropic (or OpenRouter), DeepL, Apify, LeadConnector, Telegram, Zoho.
- Update hard-coded webhook paths if you expose them through an API Gateway or reverse proxy.
- Review constants: brand guidelines text block in the translation workflow, geography filters in the email flow, scoring heuristics in the Zoho enrichment merge node.
- Test with representative payloads before going live; each flow expects specific field names as noted above.

## Operating Notes
- Monitor Airtable and Telegram outputs for translation or email QA—both flows surface error context instead of failing silently.
- The Zoho agent writes trace metadata (`_metadata`) you can expand for audit trails or routing logic.
- All workflows are active (`"active": true`), so pause in n8n before importing into a production environment if you need to stage credentials first.

Always open to questions or tweaks—these automations keep evolving as new edge cases show up in client work.
