<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/banner-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="assets/banner-light.svg">
  <img alt="Carlos Daniel Quispe — AI Implementation Specialist" src="assets/banner-light.svg" width="100%">
</picture>

<p align="center">
  <a href="https://www.linkedin.com/in/carlosdanielquispebr">
    <img alt="LinkedIn" src="https://img.shields.io/badge/LinkedIn-0B1220?style=flat-square&logo=linkedin&logoColor=5EEAD4">
  </a>
  <a href="mailto:hello@danielquispe.dev">
    <img alt="Email" src="https://img.shields.io/badge/hello@danielquispe.dev-0B1220?style=flat-square&logo=maildotru&logoColor=5EEAD4">
  </a>
  <a href="https://borapay.app">
    <img alt="BoraPay" src="https://img.shields.io/badge/borapay.app-0B1220?style=flat-square&logo=pix&logoColor=5EEAD4">
  </a>
</p>

<p align="center">
  <sub><b>Payments</b> · <b>Conversational AI</b> · <b>Automation</b> — São Paulo, Brazil</sub>
</p>

---

I build web software that moves money, answers customers and removes manual work.

> [!NOTE]
> **Most of my work lives in private repositories.** The contribution graph below is
> real, but the code behind it is closed — client systems and a payments product in
> production. What I *can* show, I show here.

<br>

## BoraPay

<table>
<tr>
<td width="60%" valign="top">

**Cross-border Pix[^pix] infrastructure between Brazil and Peru.**

A merchant in Peru charges in soles. A tourist from Brazil pays with Pix in
reais. BoraPay quotes the rate, generates the QR, confirms the payment and
tracks settlement into the merchant's local bank account.

Built end to end — architecture, data modelling, integrations, deploys and
production maintenance.

**In production, with real merchants.**

</td>
<td width="40%" valign="top">

| | |
|:--|:--|
| **Backend** | Laravel |
| **Frontend** | Vue + Inertia |
| **Data** | PostgreSQL |
| **Infra** | Laravel Cloud · Cloudflare Edge |
| **Rails** | Pix |

<a href="https://borapay.app">
  <img alt="Visit BoraPay" src="https://img.shields.io/badge/Visit-borapay.app-5EEAD4?style=for-the-badge&labelColor=0B1220">
</a>

</td>
</tr>
</table>

```mermaid
flowchart LR
    M["Merchant · Peru<br/>charges in S/"] --> API["Laravel API"]
    API --> FX["FX quote"]
    FX --> QR["Pix QR"]
    QR --> T["Tourist · Brazil<br/>pays in R$"]
    T -. "webhook" .-> API
    API --> DB[("PostgreSQL")]
    API --> Q["Async queue"]
    Q --> S["Settlement tracking"]
    S --> M

    style API fill:#0B1220,stroke:#5EEAD4,color:#E6EDF3
    style DB fill:#0B1220,stroke:#5EEAD4,color:#E6EDF3
    style Q fill:#0B1220,stroke:#5EEAD4,color:#E6EDF3
```

<details>
<summary><b>How a single charge actually flows</b></summary>

<br>

```mermaid
sequenceDiagram
    autonumber
    participant M as Merchant PE
    participant B as BoraPay
    participant P as Pix network
    participant T as Tourist BR

    M->>B: amount in soles
    B->>B: lock FX quote
    B->>P: create charge
    P-->>B: QR payload
    B-->>T: QR code
    T->>P: pays in reais
    P-->>B: confirmation webhook
    B->>B: idempotent write + audit trail
    B-->>M: confirmed, settlement queued
```

Engineering concerns that shape the system: **idempotent webhook handling**
(the network retries), **async queues** for anything slower than a request,
**traceability** on every state change, and **failure handling** that never
leaves a charge in an unknown state.

</details>

<br>

## Stack

| | |
|:--|:--|
| **Backend** | PHP · Laravel · PostgreSQL · REST APIs · queues · webhooks |
| **Frontend** | Vue · Inertia · TypeScript · Tailwind |
| **AI** | Generative AI APIs · conversational agents · WhatsApp integrations |
| **Infra** | Laravel Cloud · Cloudflare · Git |

<br>

<details>
<summary><b>Background</b></summary>

<br>

**AI Implementation Specialist** — YaVendió, São Paulo &nbsp;·&nbsp; <sub>current</sub>
Conversational AI for commerce: agent configuration, WhatsApp integration,
catalog structuring, commercial flow validation and merchant onboarding.

**Full-stack developer** — BoraPay &nbsp;·&nbsp; <sub>independent project</sub>
Cross-border Pix payment flows between Brazil and Peru.

**Studying** — Data Science & AI Engineering, SENATI
**Certified** — Meta · *Facilitate client onboarding to WhatsApp for Business*

**Languages** — Spanish <sub>native</sub> · Portuguese <sub>professional</sub> · English

</details>

<details>
<summary><b>Also building</b></summary>

<br>

**[danielquispe.dev](https://danielquispe.dev)** — personal site and technical
writing. Work in progress.

</details>

<br>

---

<p align="center">
  <sub>Open to interesting problems in payments, messaging and automation.</sub><br>
  <sub><a href="mailto:hello@danielquispe.dev">hello@danielquispe.dev</a></sub>
</p>

[^pix]: Pix is Brazil's instant payment system, run by the central bank. Over 700 financial institutions support it, and it settles in seconds.
