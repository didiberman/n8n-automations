# n8n Automations by Didi

A small library of production-tested n8n workflows I run for clients and my own stack. Every flow blends webhooks, external APIs, and LLM agents to close a specific gap in marketing or RevOps processes.

## Automation Catalog

### Airtable · Claude · DeepL Translation Agent
**In plain words**: Turns Airtable translation requests into polished, on-brand copy by letting both DeepL and Claude take a pass before choosing the best version.

**Why it matters**: Saves a large ecommerce brand hundreds of hours otherwise spent on manual translation, tone checks, and brand-guideline comparisons. Next on the roadmap is automatic prompt refinement so the flow can self-tune instructions when results miss the mark.

**How it works**: A webhook call moves the Airtable record to "Translating (DeepL)", maps the requested language to DeepL codes, runs DeepL and a Claude prompt that includes ROSENTAL Organics brand guidelines, then asks a "Final Comparing Agent" to fuse the strongest lines from both outputs.

**Outputs**: Writes DeepL, Claude, and final translations plus a title and short rationale back to the original Airtable row in the `Translation Requests` table.

**Safeguards**: Error branches catch issues in DeepL, Claude, or the final agent, update Airtable with human-readable diagnostics, and prevent jobs from stalling.

**Dependencies**: Airtable token with write scope, DeepL API key, and Anthropic Claude Sonnet 4 credentials configured in n8n LangChain nodes.

---

### Instagram Lead Personalized Email Generator
**In plain words**: Converts a lead’s survey answers and Instagram profile into a short, friendly outreach email that sounds like "Sam" and sends it automatically.

**Why it matters**: Helps an Instagram marketing expert with 150k+ followers quickly analyse each prospect’s page, respond with relevant commentary, and stay on top of high-volume inbound interest—driving more bookings while reclaiming manual drafting time.

**How it works**: After a survey webhook hits `samsurvey`, the flow screens out low-priority regions via an IP lookup, cleans the Instagram handle, launches an Apify scraper for profile stats, and feeds survey answers plus top posts into an LLM briefed to stay under 80 words.

**Outputs**: Delivers formatted HTML to LeadConnector for emailing and forwards a Telegram-ready Markdown copy for quick review, keeping both the raw and cleaned handles for context.

**Quality controls**: If the LLM reports `NOT ENOUGH INFORMATION`, an IF node stops the send so you can follow up manually instead of shipping a weak email.

**Dependencies**: Apify actor token, OpenRouter Anthropic access, LeadConnector webhook URL, and Telegram bot credentials; adjust the allow/deny country lists in the `Country Check` node to suit your campaign.

---

### Zoho CRM LLM Lead Enrich Agent
**In plain words**: Looks up new venture leads, summarises what the firm does, and fills in the missing details inside Zoho CRM automatically.

**Why it matters**: Saves the venture capital firm hundreds of hours of manual research and data entry, so investors can focus on evaluating deals instead of copying information into the CRM.

**How it works**: A webhook call triggers a random 10–120 second delay to spread API load, checks an n8n Data Table so repeat leads are skipped, then runs three OpenRouter models (Perplexity, Claude, Gemini) with JSON-only prompts and custom parsers that strip markdown.

**Outputs**: Scores the three responses, keeps the most complete set, updates Zoho CRM custom fields (`Company_Summary`, `Investment_Sectors_LLM`, `Ticket_Size_LLM`, `Investment_Stage_LLM1`, `Joining_Firm`, `Investment_Criteria`) plus `Designation` and `Description`, and logs the lead to the dedupe table.

**Safeguards**: Dedupe checks prevent double processing, the scoring script rewards precise roles/dates/sector keywords, and metadata records which model produced the chosen answer.

**Dependencies**: Zoho OAuth app with lead write scope, OpenRouter API key, and access to the n8n Data Table project (`stored leadnames dedupe`); update field IDs and table references to match your environment.

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
