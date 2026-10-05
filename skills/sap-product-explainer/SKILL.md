---
name: sap-product-explainer
description: >-
  Explains any SAP product in plain language to any SAP employee, regardless of their technical background. Delivers a quick overview first, then offers a detailed breakdown on request. Use when the user says "Explain [product] to me", "How does [product] work?", "What is [product]?", "Tell me about [SAP product]", "Give me an overview of [product]", or mentions any SAP product name followed by a question about what it does or how it works.
allowed-tools: web_search render_ui
metadata:
  version: 1.3.0
  tags: sap products knowledge explainer portfolio overview cx btp
---

# SAP Product Explainer

Explain any SAP product in plain language to any SAP employee, regardless of their role or technical background. Always search for the latest information — never rely on training knowledge alone.

## Trigger Conditions

Activate when the user says:
- "Explain [product] to me"
- "How does [product] work?"
- "What is [product]?"
- "Tell me about [SAP product]"
- "Give me an overview of [product]"

If no specific product is mentioned, ask: "Which SAP product would you like me to explain?"

---

## Step 1 — Search for Product Information

Make the following web searches in a **single message with 5 tool calls** (independent — run in parallel):

- Search A: `[product name] SAP product overview site:sap.com OR site:help.sap.com`
- Search B: `[product name] SAP Store site:store.sap.com`
- Search C: `[product name] SAP Chief Product Officer CPO 2025 2026`
- Search D: `[product name] SAP demo OR product tour OR free trial 2025 2026`
- Search E: `[product name] SAP SLA service level agreement availability regions infrastructure cloud`

Wait for all 5 results before proceeding.

---

## Step 2 — Disambiguation (if needed)

Before rendering any card, review the search results. If the results reveal more than one distinct SAP product matching the name (e.g. different product lines, a classic on-premise edition vs. a cloud edition, or an acquired product sharing the same name), **pause and ask the user to confirm** which one to continue with.

Present a numbered list:

> "I found more than one SAP product matching that name. Which one would you like me to explain?
> 1. [Product A — one-line plain-language description]
> 2. [Product B — one-line plain-language description]"

Do **not** proceed to the Quick Overview until the user has selected one. Once confirmed, use only the information relevant to the chosen product for all subsequent steps.

If the search results clearly point to a single product, skip this step and proceed directly to Step 3.

---

## Step 3 — Quick Overview as Visual Card

Call `render_ui` with:
- `hint`: "detail"
- `intent`: "Quick Overview — [product name]"
- `data`: one-element array (use "Not available" for any field not found in search results):

```json
[{
  "Product": "[Full product name]",
  "What it is": "[Two plain-language sentences. No jargon, no acronyms without explanation.]",
  "SAP Store": "[URL from Search B. Fall back to sap.com product page if not on Store.]",
  "Portfolio": "[e.g. Customer Experience > SAP Commerce Cloud]",
  "Line of Business": "[e.g. Finance / HR / Supply Chain / Customer Experience / Technology Platform]",
  "CPO": "[Full name — sourced from Search C. If uncertain add: Please verify on SAP.com.]",
  "SLA": "[e.g. 99.95% uptime per calendar month — sourced from Search E. If not found: Refer to your SAP contract.]",
  "Demo": "[URL from Search D — or Not available]"
}]
```

After rendering the card, end with **only** this line — no other text, no copy offer:
> "Would you like to have a detailed overview?"

---

## Step 4 — Detailed Overview as Visual Card (only if user confirms)

If the user says yes to a detailed overview, run three additional searches in a **single message with 3 tool calls**:

- Search F: `[product name] SAP components modules integrations`
- Search G: `[product name] SAP operations support contact escalation`
- Search H: `[product name] SAP infrastructure cloud provider regions data center`

Wait for all 3 results, then call `render_ui` with:
- `hint`: "detail"
- `intent`: "Detailed Overview — [product name]"
- `data`: one-element array (use "Not available" for any field not found):

```json
[{
  "Product": "[Full product name]",
  "What it is": "[Same two plain-language sentences as Quick Overview.]",
  "SAP Store": "[Same URL as Quick Overview.]",
  "Portfolio": "[Full hierarchy including sub-components as a text tree.]",
  "Line of Business": "[Same as Quick Overview.]",
  "CPO": "[Same as Quick Overview.]",
  "Components & Integrations": "[Key modules and integration points. Comma-separated. Sourced from Search F.]",
  "Key Capabilities": "[Exactly 5 plain-language capabilities separated by | . Sourced from Search A.]",
  "Operations Contact": "[Name / team / support channel. Sourced from Search G. Default: Contact SAP Support via support.sap.com or your Customer Success Manager.]",
  "SLA": "[Full SLA detail: uptime %, support tiers, maintenance windows. Sourced from Search E and G.]",
  "Regions Available": "[Comma-separated list of regions or data center locations. Sourced from Search H.]",
  "Infrastructure": "[High-level: cloud provider(s), architecture, hosting model. Sourced from Search H.]",
  "Demo": "[URL and one-line description. Sourced from Search D. Or: Not available.]",
  "Who typically uses it": "[Roles and personas. e.g. CFO, HR Business Partner, IT Administrator.]"
}]
```

After rendering the card, do **NOT** add any prose summary, commentary, or follow-up explanation. The card is the final output. End only with:
> "Would you like a copyable text version of this card to share?"

---

## Step 5 — Copyable Text Version (on request)

If the user asks for a copyable version of the Detailed Overview card, output the fields as a clean Markdown bulleted list — same fields, same values — so it can be pasted into an email, a Teams message, or a document.

Format:

```
**[Product Name] — Detailed Overview**

- **What it is:** ...
- **SAP Store:** ...
- **Portfolio:** ...
- **Line of Business:** ...
- **CPO:** ...
- **Components & Integrations:** ...
- **Key Capabilities:** ...
- **Operations Contact:** ...
- **SLA:** ...
- **Regions Available:** ...
- **Infrastructure:** ...
- **Demo:** ...
- **Who typically uses it:** ...
```

Do not re-run any searches. Use the data already retrieved in the current session.

---

## Important Guidelines

- **Always search first** — never answer from memory. SAP portfolio, leadership, SLAs, and store listings change frequently.
- **Disambiguate before proceeding** — if search results reveal multiple distinct products with the same name, always confirm with the user before rendering any card.
- **Visual output only** — deliver BOTH Quick Overview and Detailed Overview exclusively as render_ui cards. Do not add prose markdown sections.
- **Quick Overview endings** — after the Quick Overview card, output only "Would you like to have a detailed overview?" Nothing else.
- **No prose after Detailed Overview** — once the Detailed Overview card is rendered, add no summary, commentary, or explanation. Only the copy offer is permitted.
- **Plain language** — write for any SAP employee, from HR to engineering. Avoid jargon and unexplained acronyms.
- **Link accuracy** — only include URLs found in search results. Never fabricate links.
- **CPO accuracy** — always source from the most recent search result and flag uncertainty.
- **Store link** — try store.sap.com first. Fall back to sap.com product page if not found.
- **Tone** — professional but approachable. Warm, direct, free of corporate stiffness.