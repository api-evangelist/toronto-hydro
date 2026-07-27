---
name: Onboard as a Toronto Hydro Green Button third party
description: >-
  Work out what a developer must actually do to reach Toronto Hydro's mandated Green Button
  Connect My Data surface — an application through the vendor onboarding portal, a
  connectivity test, the Third Party Terms and the insurance they require — and understand
  what the ApplicationInformation resource represents once you are approved.
api: openapi/toronto-hydro-green-button-espi-openapi.yml
operations:
  - findApplicationInformations
  - getApplicationInformation
generated: '2026-07-27'
method: generated
---

# Onboard as a Toronto Hydro Green Button third party

## What you are dealing with

Toronto Hydro has a real, live Green Button implementation and **no developer product**.
There is no `developer.torontohydro.com`, no `api.` or `docs.` subdomain (none of them
resolve), no published base URI, no API reference, no OpenAPI, no sandbox and no self-serve
keys. Every technical detail is handed out inside a private onboarding process.

The OpenAPI in this repo is the **Green Button Alliance's** document, harvested verbatim
with provenance. Operation names, parameters and resource shapes are real ESPI; the
`servers[]` host is the GBA sandbox. **Never treat it as a Toronto Hydro endpoint and never
guess a Toronto Hydro base URI.**

## Steps

1. **Confirm the mandate applies.** Ontario Regulation 633/21 (Energy Data) under the
   Electricity Act, 1998 requires rate-regulated Ontario electricity and gas utilities to
   offer Green Button Download My Data and Connect My Data, conforming to NAESB REQ.21 ESPI
   v3.3, as of 1 November 2023. Toronto Hydro-Electric System Limited is inside that class.
   Toronto Hydro's own Third Party Terms define Green Button as the standardized format "as
   implemented by utilities in accordance with O.Reg 633/21".

2. **Start at the public Green Button page.**
   <https://www.torontohydro.com/for-home/green-button>. It states the three requirements
   verbatim: submit an online application, complete a connectivity test, and comply with the
   Third-Party Terms and Conditions for Green Button Connect My Data.

3. **Apply through the third-party portal.**
   <https://torontoonboarding.savagedata.com/> — a live registration application
   (`3rdPartyRegistration`) operated by Toronto Hydro's platform vendor, Savage Data Systems.
   Toronto Hydro says "Additional information will be provided in the third-party portal";
   the base URI, credentials and connectivity-test criteria all live behind it. Note the host
   negotiates TLS 1.2 only — see `security/toronto-hydro-domain-security.yml`.

4. **Read the Third Party Terms before you build.**
   <https://www.torontohydro.com/green-button/third-party-terms>. They are the real contract
   and they carry obligations most API terms do not:
   - Insurance: Workman's Compensation, Commercial General Liability, Professional Liability
     and Property Damage, at your expense, with certificates on request naming Toronto Hydro
     as an additional insured, a waiver of subrogation, and 30 days written notice of
     cancellation.
   - Purpose limitation: data may be used only to present customers solutions that optimize
     energy usage, reduce consumption or reduce energy costs.
   - Fair use in place of rate limits: you may not burden Toronto Hydro's infrastructure "to
     an unreasonable and disproportionate extent" or interfere with normal functioning.
   - Termination: a three-Business-Day cure window on notice of default, immediate
     termination in the enumerated cases, and no liability to you for the consequences.
   - Toronto Hydro's Conditions of Service and Privacy Policy are incorporated by reference.

5. **Expect no marketplace listing.** Toronto Hydro states it cannot provide customers with
   a list of participating third parties. Customer acquisition is entirely your side of the
   flow — the customer must already know you before any authorization begins.

6. **Understand the ApplicationInformation resource.** Once approved, your registration is
   modelled by the ESPI resource behind these operations:
   - `findApplicationInformations` — `GET /espi/1_1/resource/ApplicationInformation`
   - `getApplicationInformation` — `GET /espi/1_1/resource/ApplicationInformation/{applicationInformationId}`

   It carries `client_id`, `client_secret`, `redirect_uri`, `scope`, `grant_types`,
   `thirdPartyApplicationType` (1=Web, 2=Desktop, 3=Mobile, 4=Device) and the status fields
   the Data Custodian maintains. This is the OAuth client record — the machine-readable
   counterpart of the application you filed.

## What you cannot find out in advance

- The ESPI base URI, the authorization endpoint and the token endpoint. None are published,
  and no OpenID Connect or RFC 8414 discovery document is served anywhere — see
  `well-known/toronto-hydro-well-known.yml`.
- The scope names. The `scopes` object in the source spec is empty and Toronto Hydro
  publishes no scope reference. Do not hard-code scope strings; use your onboarding packet.
- Rate limits, quotas, data latency, interval length and history window — none published.
- Onboarding timeline, fees and SLA — none published.

## Related artifacts

`conventions/toronto-hydro-conventions.yml` · `authentication/toronto-hydro-authentication.yml` ·
`conformance/toronto-hydro-conformance.yml` · `lifecycle/toronto-hydro-lifecycle.yml` ·
`review.yml`
