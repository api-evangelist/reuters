# Reuters

Global news organization providing breaking news, business, financial, and multimedia content through wire services, digital platforms, and content APIs serving media organizations worldwide. Reuters Connect Web Services provides a professional REST API for searching and retrieving editorial content including text, images, video, and graphics.

**URL:** [https://raw.githubusercontent.com/api-evangelist/reuters/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/reuters/refs/heads/main/apis.yml)

## Scope

- **Type:** Index
- **Position:** Consuming
- **Access:** 3rd-Party

## Tags

- Business, Finance, Journalism, Media, News, Wire Service

## Timestamps

- **Created:** 2024-01-01
- **Modified:** 2026-05-02

## APIs

### Reuters Connect API

Professional content delivery platform providing access to news, images, video, and data from Reuters and partner content sources via REST API. Content is organized into channels by category and items can be retrieved individually or searched by keyword.

**Human URL:** [https://www.reutersconnect.com](https://www.reutersconnect.com)

#### Tags

- Content Delivery, Images, Media, News, Search, Video

#### Properties

- [Documentation](https://developers.reutersconnect.com/docs)
- [Authentication](https://developers.reutersconnect.com/authentication)
- [OpenAPI](openapi/reuters-connect-api-openapi.yml)

## Artifacts

### OpenAPI Specifications

- [`openapi/reuters-connect-api-openapi.yml`](openapi/reuters-connect-api-openapi.yml) — Reuters Connect API covering authentication, channels, items, and search.

### JSON Schemas

- [`json-schema/reuters-channel-schema.json`](json-schema/reuters-channel-schema.json) — Schema for Reuters content channels.
- [`json-schema/reuters-item-schema.json`](json-schema/reuters-item-schema.json) — Schema for Reuters content items.
- [`json-schema/reuters-rendition-schema.json`](json-schema/reuters-rendition-schema.json) — Schema for media renditions.
- [`json-schema/reuters-search-result-schema.json`](json-schema/reuters-search-result-schema.json) — Schema for search results.

### JSON Structure

- [`json-structure/reuters-connect-api-structure.json`](json-structure/reuters-connect-api-structure.json) — Entity relationships and endpoint structure for the Reuters Connect API.

### JSON-LD Context

- [`json-ld/reuters-context.jsonld`](json-ld/reuters-context.jsonld) — JSON-LD context mapping Reuters vocabulary to schema.org, IPTC, and rNews ontologies.

### Examples

- [`examples/reuters-authenticate-example.json`](examples/reuters-authenticate-example.json) — Authentication request/response example.
- [`examples/reuters-list-channels-example.json`](examples/reuters-list-channels-example.json) — List channels request/response example.
- [`examples/reuters-search-items-example.json`](examples/reuters-search-items-example.json) — Search items request/response example.

### Rules

- [`rules/reuters-connect-api-rules.yml`](rules/reuters-connect-api-rules.yml) — Spectral ruleset enforcing Reuters Connect API conventions.

### Capabilities

- [`capabilities/shared/reuters-connect.yaml`](capabilities/shared/reuters-connect.yaml) — Shared Naftiko capability definition for the Reuters Connect API.
- [`capabilities/content-delivery.yaml`](capabilities/content-delivery.yaml) — Workflow capability for content discovery and delivery (4 MCP tools).

### Vocabulary

- [`vocabulary/reuters-vocabulary.yml`](vocabulary/reuters-vocabulary.yml) — Domain vocabulary covering 14 key Reuters and news industry terms.

## Links

- **Website**: [reuters.com](https://www.reuters.com)
- **Developer Portal**: [reutersconnect.com](https://www.reutersconnect.com)
- **Developer Documentation**: [developers.reutersconnect.com](https://developers.reutersconnect.com/docs)
- **GitHub Organization**: [github.com/ReutersMedia](https://github.com/ReutersMedia)
- **Support**: [Reuters Contact](https://www.reuters.com/info-pages/contact-us/)

## Maintainers

**FN:** Kin Lane

**Email:** kin@apievangelist.com
