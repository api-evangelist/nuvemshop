# Nuvemshop / Tiendanube (nuvemshop)

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
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Nuvemshop (branded **Tiendanube** in Spanish-speaking markets) is the leading Latin American e-commerce platform, powering online stores for merchants across Brazil, Argentina, Mexico, Chile, and Colombia.

## Access model (read this first)

- **REST, store-scoped.** Every endpoint lives under a per-store base that embeds the numeric store id, e.g. `https://api.tiendanube.com/2025-03/{store_id}`. The Brazilian mirror `https://api.nuvemshop.com.br/2025-03/{store_id}` serves the same API, and the long-standing `https://api.tiendanube.com/v1/{store_id}` path remains available as the legacy equivalent.
- **OAuth 2 app authorization.** Apps use the authorization-code grant; the token exchange is a `POST https://www.tiendanube.com/apps/authorize/token`. The returned access token is **non-expiring** and the response also returns `user_id` — the store id you put in every API path.
- **Non-standard auth header.** Send the token as `Authentication: bearer ACCESS_TOKEN`. The header name must be `Authentication` (using `Authorization` returns 401) and `bearer` must be **lowercase**.
- **User-Agent required.** Every request must include a descriptive `User-Agent` identifying your app and a contact (e.g. `MyApp (name@email.com)`) or the API returns 400.
- **Per-store rate limiting.** A leaky bucket holds 40 requests by default and drains at 2 req/s; higher plan tiers get 10x. Overflow returns 429 with `x-rate-limit-limit` / `x-rate-limit-remaining` / `x-rate-limit-reset` headers.
- **No WebSocket.** The API is REST plus **webhooks** (HTTP POST callbacks for events like `order/created`). There is no documented `wss://` streaming API.

This entry captures a solid, grounded representative subset (10 resources). Endpoint paths, methods, auth, and rate limits are grounded in the live docs; OpenAPI request/response body schemas are simplified representative models. The platform documents many more resources (Cart, Draft Order, Fulfillment Order, Transaction, Checkout, Discount, Location, Shipping Carrier, Payment Provider, Metafields, Billing, and more) not modeled here.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/nuvemshop/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/nuvemshop/refs/heads/main/apis.yml)

## Tags

- E-commerce
- Online Store
- Latin America
- Brazil
- Argentina
- Storefront
- Products
- Orders
- Merchants
- Webhooks
- SaaS

## Timestamps

- **Created:** 2026-07-12
- **Modified:** 2026-07-12

## APIs

### Nuvemshop Products API

Create, list, retrieve, update, and delete products — the items for sale in a store. Includes lookup by variant SKU and a bulk stock/price update endpoint.

- **Human URL:** [https://tiendanube.github.io/api-documentation/resources/product](https://tiendanube.github.io/api-documentation/resources/product)
- **Base URL:** `https://api.tiendanube.com/2025-03/{store_id}`

#### Tags

- Products
- Catalog
- E-commerce

#### Properties

- [Documentation](https://tiendanube.github.io/api-documentation/resources/product)
- [API Reference](https://tiendanube.github.io/api-documentation/resources/product)
- [OpenAPI](openapi/nuvemshop-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/nuvemshop.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/nuvemshop.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Nuvemshop Product Variants API

Manage the variants (size, color, and other option combinations) owned by a product, including per-variant pricing and stock, bulk collection replacement, and a dedicated stock-update endpoint.

- **Human URL:** [https://tiendanube.github.io/api-documentation/resources/product-variant](https://tiendanube.github.io/api-documentation/resources/product-variant)
- **Base URL:** `https://api.tiendanube.com/2025-03/{store_id}`

#### Tags

- Variants
- Inventory
- Stock

#### Properties

- [Documentation](https://tiendanube.github.io/api-documentation/resources/product-variant)
- [OpenAPI](openapi/nuvemshop-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/nuvemshop.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/nuvemshop.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Nuvemshop Product Images API

Create, list, retrieve, update, and delete the images attached to a product, uploaded by URL or as base64-encoded attachments.

- **Human URL:** [https://tiendanube.github.io/api-documentation/resources/product-image](https://tiendanube.github.io/api-documentation/resources/product-image)
- **Base URL:** `https://api.tiendanube.com/2025-03/{store_id}`

#### Tags

- Images
- Media
- Catalog

#### Properties

- [Documentation](https://tiendanube.github.io/api-documentation/resources/product-image)
- [OpenAPI](openapi/nuvemshop-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/nuvemshop.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/nuvemshop.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Nuvemshop Categories API

Create, list, retrieve, update, and delete the hierarchical categories used to organize a store's catalog.

- **Human URL:** [https://tiendanube.github.io/api-documentation/resources/category](https://tiendanube.github.io/api-documentation/resources/category)
- **Base URL:** `https://api.tiendanube.com/2025-03/{store_id}`

#### Tags

- Categories
- Taxonomy
- Catalog

#### Properties

- [Documentation](https://tiendanube.github.io/api-documentation/resources/category)
- [OpenAPI](openapi/nuvemshop-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/nuvemshop.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/nuvemshop.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Nuvemshop Orders API

Create, list, retrieve, and update orders, read value/edition history and subscriptions, and drive lifecycle actions — close, re-open, and cancel an order.

- **Human URL:** [https://tiendanube.github.io/api-documentation/resources/order](https://tiendanube.github.io/api-documentation/resources/order)
- **Base URL:** `https://api.tiendanube.com/2025-03/{store_id}`

#### Tags

- Orders
- Sales
- Fulfillment

#### Properties

- [Documentation](https://tiendanube.github.io/api-documentation/resources/order)
- [OpenAPI](openapi/nuvemshop-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/nuvemshop.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/nuvemshop.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Nuvemshop Customers API

Create, list, retrieve, update, and delete the customer accounts registered in a store.

- **Human URL:** [https://tiendanube.github.io/api-documentation/resources/customer](https://tiendanube.github.io/api-documentation/resources/customer)
- **Base URL:** `https://api.tiendanube.com/2025-03/{store_id}`

#### Tags

- Customers
- CRM
- Accounts

#### Properties

- [Documentation](https://tiendanube.github.io/api-documentation/resources/customer)
- [OpenAPI](openapi/nuvemshop-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/nuvemshop.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/nuvemshop.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Nuvemshop Coupons API

Create, list, retrieve, update, and delete discount coupons that a store offers to its shoppers.

- **Human URL:** [https://tiendanube.github.io/api-documentation/resources/coupon](https://tiendanube.github.io/api-documentation/resources/coupon)
- **Base URL:** `https://api.tiendanube.com/2025-03/{store_id}`

#### Tags

- Coupons
- Discounts
- Promotions

#### Properties

- [Documentation](https://tiendanube.github.io/api-documentation/resources/coupon)
- [OpenAPI](openapi/nuvemshop-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/nuvemshop.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/nuvemshop.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Nuvemshop Webhooks API

Register and manage webhook subscriptions that POST event notifications (`order/created`, `product/updated`, `customer/created`, and many more) to your application. Server-to-endpoint HTTP callbacks, not a streaming socket.

- **Human URL:** [https://tiendanube.github.io/api-documentation/resources/webhook](https://tiendanube.github.io/api-documentation/resources/webhook)
- **Base URL:** `https://api.tiendanube.com/2025-03/{store_id}`

#### Tags

- Webhooks
- Events
- Notifications

#### Properties

- [Documentation](https://tiendanube.github.io/api-documentation/resources/webhook)
- [OpenAPI](openapi/nuvemshop-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/nuvemshop.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/nuvemshop.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Nuvemshop Scripts API

Create, list, retrieve, update, and delete script-store associations that inject custom JavaScript into a merchant's storefront.

- **Human URL:** [https://tiendanube.github.io/api-documentation/resources/script](https://tiendanube.github.io/api-documentation/resources/script)
- **Base URL:** `https://api.tiendanube.com/2025-03/{store_id}`

#### Tags

- Scripts
- Storefront
- Customization

#### Properties

- [Documentation](https://tiendanube.github.io/api-documentation/resources/script)
- [OpenAPI](openapi/nuvemshop-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/nuvemshop.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/nuvemshop.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Nuvemshop Store API

Retrieve the authenticated store's general settings and metadata — name, domain, country, currency, language, and contact details.

- **Human URL:** [https://tiendanube.github.io/api-documentation/resources/store](https://tiendanube.github.io/api-documentation/resources/store)
- **Base URL:** `https://api.tiendanube.com/2025-03/{store_id}`

#### Tags

- Store
- Settings
- Merchant

#### Properties

- [Documentation](https://tiendanube.github.io/api-documentation/resources/store)
- [OpenAPI](openapi/nuvemshop-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/nuvemshop.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/nuvemshop.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [Domain Security](security/nuvemshop-domain-security.yml)
- [Authentication](authentication/nuvemshop-authentication.yml)
- [GitHub Organization](https://github.com/TiendaNube)
- [LinkedIn](https://www.linkedin.com/company/tiendanube)
- [Website](https://www.tiendanube.com)
- [Documentation](https://tiendanube.github.io/api-documentation/)
- [Plans](plans/nuvemshop-plans-pricing.yml)
- [Rate Limits](rate-limits/nuvemshop-rate-limits.yml)
- [Fin Ops](finops/nuvemshop-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
