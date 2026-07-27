---
name: Retrieve a customer's Green Button usage data from Toronto Hydro
description: >-
  With an approved third-party registration, take a Toronto Hydro customer through the Green
  Button Connect My Data authorization flow, verify the resulting Authorization resource,
  walk to the customer's UsagePoint records, and pull bulk data — handling the
  consent-revocation reality that makes a 403 an expected steady state rather than a client
  defect.
api: openapi/toronto-hydro-green-button-espi-openapi.yml
operations:
  - findAuthorizations
  - getAuthorization
  - findUsagePoints
  - getUsagePoint
  - downloadBulkData
generated: '2026-07-27'
method: generated
---

# Retrieve a customer's Green Button usage data from Toronto Hydro

## Prerequisites

Complete `toronto-hydro-green-button-onboarding.md` first. You need connection details
Toronto Hydro issues only after the application, connectivity test and Terms acceptance.
**There is no base URI to discover** — none is published, and no anonymously served OpenID
Connect discovery document exists on any Toronto Hydro or Savage Data host.

The referenced OpenAPI is the Green Button Alliance's, not Toronto Hydro's. Operation names
and parameter shapes are real; the `servers[]` host is the GBA sandbox and must be replaced
with the base URI Toronto Hydro issues you.

## Steps

1. **Initiate the authorization from inside your application.** Per Toronto Hydro's Green
   Button Connect My Data Customer Guide, you either email the customer a link or redirect
   them from your app or web page to *Toronto Hydro's authentication page*.

2. **Expect two customer paths.** Option A: the customer signs in with their existing
   Toronto Hydro online account. Option B: a customer with no online account is offered an
   alternative method to provide consent. Either way they land on the authorization page.
   Build for both — do not assume every Toronto Hydro customer has a portal login.

3. **Exchange the code for a token.** OAuth 2.0 authorization code; the spec also declares a
   `clientCredentials` flow. The `scopes` object in the source document is **empty** and
   Toronto Hydro publishes no scope reference, so do not hard-code scope strings — use what
   your onboarding packet specifies. See `scopes/toronto-hydro-scopes.yml`.

4. **Verify the Authorization resource.**
   - `findAuthorizations` — `GET /espi/1_1/resource/Authorization`
   - `getAuthorization` — `GET /espi/1_1/resource/Authorization/{authorizationId}`

   Read `status` (0=Revoked, 1=Active, 2=Denied), `expires_at`, `grant_type`, `scope` and
   `token_type`. Persist `resourceURI` (where the authorized data lives), `authorizationURI`
   (where to update or delete this authorization) and `customerResourceURI` (the separately
   addressed customer/PII data). **Treat `status` and `expires_at` as the authority on
   whether you may still call** — not the age of your token.

5. **Walk to the meter.**
   - `findUsagePoints` — `GET /espi/1_1/resource/UsagePoint`
   - `getUsagePoint` — `GET /espi/1_1/resource/UsagePoint/{usagePointId}`

   `ServiceCategory` is an integer enum (0=electricity, 1=gas, 2=water); Toronto Hydro
   distributes electricity only, so expect 0. `status` is 0=off / 1=on. `isSdp` marks a
   service delivery point and `isVirtual` marks a logical usage point — do not treat a
   virtual usage point as a physical meter.

6. **Pull bulk data.**
   - `downloadBulkData` — `GET /espi/1_1/resource/Batch/Bulk/{bulkId}`

   This is the asynchronous path. A `202 Accepted` here is the expected first answer — poll
   for the Atom feed rather than treating it as a failure.

7. **Scope your time window.** Use `published-min` / `published-max` and `updated-min` /
   `updated-max` (RFC 3339 instants) with `start-index` (1-indexed) and `max-results`.
   Toronto Hydro publishes **no** interval length, history window or data-latency figure for
   either Green Button surface, so do not assume one — the only public data point is a 2019
   community tool's note that portal usage data lagged two to three days. Discover the real
   window empirically after onboarding.

## Handling failures

- **`403 Forbidden` is an expected steady state.** Consent is customer-granted and
  revocable, and Toronto Hydro gives it three ways to end: the customer revokes at any time
  from <https://www.torontohydro.com/my-account/green-button-connections>; the customer's
  account is closed, after which Connect My Data stops — including for the final billing
  period; or Toronto Hydro terminates your entitlement under the Third Party Terms.
  **Re-obtain consent; do not retry.** Confirm by reading `status` on the Authorization.
- **`400 Bad Request`** is almost always a malformed timestamp (not RFC 3339) or a
  non-integer `start-index`, `max-results` or `depth`.
- **Errors carry no body.** No schema, no `application/problem+json`. You will not get a
  machine-readable reason — log the request parameters yourself.
- **No `401`, `404`, `429` or `5xx` is declared** anywhere in the contract, and no rate
  limits are published. The Terms instead impose a discretionary fair-use rule enforced by
  termination, so back off conservatively and build retry budgets regardless.

## Notes an agent should carry

- Responses are **Atom XML**, never JSON.
- The ESPI resources that carry actual interval consumption values (`MeterReading`,
  `IntervalBlock`, `IntervalReading`, `ReadingType`, the usage summaries) are **not defined
  in this specification** and Toronto Hydro publishes no schema for them. Expect them on the
  wire; do not expect this document to describe them.
- If you only need one customer's data once, the far cheaper path is **Download My Data** —
  the customer signs in at <https://www.torontohydro.com/my-account/green-button-data> and
  hands you a standards-conformant Green Button file. No onboarding, no insurance, no
  connectivity test.
- Toronto Hydro's Green Button conformance could not be verified from outside — no base URI,
  no reference, no discovery document, and no public Green Button Alliance
  certified-products register naming Toronto Hydro. See `review.yml`.

## Related artifacts

`conventions/toronto-hydro-conventions.yml` · `authentication/toronto-hydro-authentication.yml` ·
`scopes/toronto-hydro-scopes.yml` · `errors/toronto-hydro-problem-types.yml` ·
`data-model/toronto-hydro-data-model.yml` · `lifecycle/toronto-hydro-lifecycle.yml`
