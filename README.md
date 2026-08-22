# Toronto Hydro (toronto-hydro)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Toronto Hydro is the municipally owned local electricity distribution company (LDC) for the City of Toronto, delivering power to roughly 800,000 residential and business customers across Canada's largest city. It sits in the wires-and-meters layer of Ontario's electricity value chain — it does not generate power and it does not run the wholesale market (that is IESO) — so the only customer-facing data it owns is smart-meter consumption, billing and account data. Its API posture is a clean example of a mandate that produced an implementation but not a developer product: Ontario's O. Reg. 633/21 under the Electricity Act, 1998 compelled rate-regulated electricity and gas utilities to offer Green Button Download My Data and Connect My Data conforming to NAESB REQ.21 ESPI v3.3 by 1 November 2023, and Toronto Hydro runs both — customer-facing Download My Data and Connect My Data pages behind its account login, a published third-party terms-and-conditions document, and a live third-party onboarding portal operated by its platform vendor Savage Data Systems. But there is no developer.torontohydro.com, no docs. or api. subdomain, no published base URI, no OpenAPI, and no self-serve keys. Consumer data is available only to companies that apply, pass a connectivity test and sign the third-party terms; market and grid data are not published openly at all. Mandated, implemented, and completely gated.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/toronto-hydro/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/toronto-hydro/refs/heads/main/apis.yml)

## Tags

- Energy
- Canada
- Utilities
- Electricity
- Smart Metering
- Green Button
- Grid
- Ontario
- Consumer Data
- Electricity Distribution

## Timestamps

- **Created:** 2026-07-27
- **Modified:** 2026-07-27

## APIs

### Toronto Hydro Green Button Connect My Data

Toronto Hydro's Green Button Connect My Data (CMD) implementation, required of rate-regulated Ontario electricity utilities by O. Reg. 633/21 and built to the NAESB REQ.21 Energy Services Provider Interface (ESPI) v3.3 standard. A registered and approved third party receives a redirect to a Toronto Hydro authentication page where the customer signs in to their Toronto Hydro online account (or uses an alternate consent method if they have no online account) and authorizes ongoing machine-to-machine delivery of their electricity usage, billing and account data. Toronto Hydro publishes no base URI, no API reference and no machine-readable contract for this API — the resource shapes come from the ESPI standard rather than from the utility. Access is application-approval only, via the third-party onboarding portal operated by platform vendor Savage Data Systems, and requires a connectivity test plus acceptance of Toronto Hydro's Third Party Terms and Conditions for Green Button Connect My Data.

- **Human URL:** [https://www.torontohydro.com/for-home/green-button](https://www.torontohydro.com/for-home/green-button)
- **Base URL:** not published

#### Tags

- Green Button
- Connect My Data
- ESPI
- Energy Usage
- Consumer Data
- Consent

#### Properties

- [Documentation](https://www.torontohydro.com/for-home/green-button)
- [Developer Portal](https://torontoonboarding.savagedata.com/)
- [Terms of Service](https://www.torontohydro.com/green-button/third-party-terms)
- [Getting Started](https://www.torontohydro.com/documents/d/guest/green-button-connect-my-data-customer-guide)
- [Login](https://www.torontohydro.com/my-account/green-button-connections)

### Toronto Hydro Green Button Download My Data

Toronto Hydro's Green Button Download My Data (DMD) implementation, also required by O. Reg. 633/21 and built to NAESB REQ.21 ESPI v3.3. A Toronto Hydro customer signs in to their own account and downloads their electricity consumption, billing and customer data as a standards-conformant Green Button (ESPI XML) file they can hand to any tool they choose. This is a customer-account-gated self-service export rather than a programmatic API — there is no anonymous endpoint, no key, and no documented URL pattern — but the file it emits is a real, standardized, machine-readable energy-data artifact, which is what makes DMD the practical integration path for anyone not willing to complete third-party onboarding for CMD.

- **Human URL:** [https://www.torontohydro.com/for-home/green-button](https://www.torontohydro.com/for-home/green-button)
- **Base URL:** not published

#### Tags

- Green Button
- Download My Data
- ESPI
- Energy Usage
- Consumer Data

#### Properties

- [Documentation](https://www.torontohydro.com/for-home/green-button)
- [Login](https://www.torontohydro.com/my-account/green-button-data)

## Common Properties

- [Website](https://www.torontohydro.com/)
- [Documentation](https://www.torontohydro.com/for-home/green-button)
- [Developer Portal](https://torontoonboarding.savagedata.com/)
- [Terms of Service](https://www.torontohydro.com/green-button/third-party-terms)
- [Privacy Policy](https://www.torontohydro.com/privacy-policy)
- [Support](https://www.torontohydro.com/contact-us)
- [FAQ](https://www.torontohydro.com/frequently-asked-questions)
- [Blog](https://www.torontohydro.com/newsroom)
- [LinkedIn](https://ca.linkedin.com/company/toronto-hydro)

## Mandate Posture

| Field | Value |
| --- | --- |
| Mandate regime | `green-button-ontario` (O. Reg. 633/21 under the Electricity Act, 1998) |
| Mandate status | `live-implemented` — verified live DMD, CMD and third-party onboarding surfaces |
| Data standard | Green Button / NAESB REQ.21 ESPI v3.3 (version attributed to the regime and platform vendor, not stated by Toronto Hydro) |
| Consumer data API | Yes — Green Button Connect My Data, consent-gated |
| Open market data | No — no grid, system or market data API; that layer belongs to IESO |
| Access gate | `application-approval` — online application, connectivity test, third-party terms |
| Auth model | OAuth-style redirect + customer consent at a Toronto Hydro authentication page; credentials issued after approval |
| Machine-readable contracts | None published (0 OpenAPI, 0 AsyncAPI, 0 collections) |

See [review.yml](review.yml) for every URL probed, its HTTP status, and exactly what was and was not verified.

## Maintainers

- Kin Lane — kin@apievangelist.com
