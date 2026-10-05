# SAP Product Explainer

> A Joule Work Desktop skill that explains any SAP product in plain language to any SAP employee.
> Author - Dhriti Chakraborty

![Version](https://img.shields.io/badge/version-1.0.0-blue)
![License](https://img.shields.io/badge/license-Apache%202.0-green)
![Platform](https://img.shields.io/badge/platform-Joule%20Work%20Desktop-orange)
![Tool](https://img.shields.io/badge/tool-web__search-lightgrey)

---

## Overview

SAP's product portfolio is vast. Whether you're in HR, Sales, Finance, or Engineering, it can be hard to speak intelligently about products outside your own area. The **SAP Product Explainer** skill solves that.

Ask Joule about any SAP product and get a plain-language explanation in seconds — no jargon, no acronyms you need to decode, and always sourced from the latest information on SAP.com and the SAP Help Portal.

---

## Features

- **Quick Overview** — delivered first: what the product is, where it fits in SAP's portfolio, which Line of Business it belongs to, and who the CPO is
- **Detailed Overview** — on request: adds key capabilities, demo links, typical users, and component/integration details
- **Always up to date** — searches SAP.com, SAP Help Portal, and SAP Store in real time; never relies on outdated training data
- **Plain language** — written for any SAP employee, from HR to pre-sales to engineering
- **Portfolio tree** — text-based hierarchy showing exactly where the product sits in SAP's suite
- **CPO attribution** — always identifies the responsible Chief Product Officer with source link
- **Adaptive depth** — quick overview first, full detail only when the user asks for it

---

## Installation

### In Joule Work Desktop

1. Open **Joule Work Desktop**
2. Go to **Extensions > Skills**
3. Click **Install Skill** and upload the `SKILL.md` file (or the `.zip` export)
4. The skill activates automatically — no additional connector required

### Requirements

| Requirement | Details |
|---|---|
| Platform | Joule Work Desktop (any version with skill support) |
| Tool | `web_search` (built-in, no connector needed) |
| Connectors | None |

---

## Usage

### Trigger Phrases

| Phrase | Example |
|--------|--------|
| `Explain [product] to me` | "Explain SAP BTP to me" |
| `How does [product] work?` | "How does SAP SuccessFactors work?" |
| `What is [product]?` | "What is SAP Ariba?" |
| `Tell me about [product]` | "Tell me about SAP Commerce Cloud" |
| `Give me an overview of [product]` | "Give me an overview of SAP S/4HANA" |

### Output: Quick Overview

Always delivered first. Includes:

```
📦 What it is
[Two plain-language sentences] [View on SAP Store](url)

🗂 Where it fits in SAP's Portfolio
SAP Portfolio
└── [Suite or Layer]
    └── [Product Family]
        └── [Product Name]

🏢 Line of Business
[e.g. Finance, HR, Supply Chain, Customer Experience]

👔 Chief Product Officer (CPO)
[Name] — [Source link]

Would you like to have a detailed overview?
```

> The portfolio tree is only shown in the quick overview if the hierarchy is short and clean (≤4 levels). If complex, it is deferred to the detailed overview.

### Output: Detailed Overview

Delivered on user confirmation. Adds:

```
⚙️ Key Capabilities
• [5 plain-language capability bullets]

🎬 Demo
[One-liner description] → [Link]

👤 Who typically uses it
[Roles and personas]

🔗 Components & Integrations
• [Key modules, connected SAP/third-party products]
```

---

## License

Apache License 2.0 — see [LICENSE](LICENSE) for details.
