# Standards & API Reference

> Project: Executive Reporting Automation · Generated: 2026-05-06

## Industry Standards & Specifications

### ISO Standards

**ISO 8000-1:2022 — Data Quality**
- URL: https://www.iso.org/standard/81745.html
- Defines requirements for data quality along dimensions of accuracy, consistency, completeness, timeliness, and portability. Directly relevant to ensuring data fed into automated executive reports is verifiable and auditable. Poor master data quality is a leading cause of unreliable report outputs.

**ISO/IEC 25012:2008 — Software Product Quality: Data Quality Model**
- URL: https://www.iso.org/standard/35736.html
- Provides a data quality model classifying 15 quality characteristics across inherent and system-dependent dimensions. A foundation for assessing the fitness of source data before it enters an automated reporting pipeline.

### W3C & IETF Standards

**W3C PROV Data Model (PROV-DM)**
- URL: https://www.w3.org/TR/prov-dm/
- Defines a conceptual data model for provenance — tracking entities, activities, and agents involved in producing data. Essential for executive reports that must carry auditable lineage (who generated this report, from which data sources, at what time). Oracle and other enterprise vendors already consume PROV feeds for audit trails.

**RFC 7231 — HTTP/1.1 Semantics and Content**
- URL: https://datatracker.ietf.org/doc/html/rfc7231
- The foundational IETF specification for HTTP semantics. Any REST-based reporting API that retrieves data from source systems, triggers report generation, or delivers report payloads operates over HTTP and must comply with this RFC.

**RFC 8288 — Web Linking**
- URL: https://datatracker.ietf.org/doc/html/rfc8288
- Defines the Link header field for expressing typed relationships between resources. Relevant for report APIs that need to navigate paginated result sets or express relationships between report versions, data sources, and outputs.

**RFC 5545 — iCalendar (Internet Calendaring and Scheduling)**
- URL: https://datatracker.ietf.org/doc/html/rfc5545
- Defines the iCalendar data format for scheduling events, recurrences, and reminders. Directly applicable to scheduling automated report delivery — recurring weekly/monthly executive reports map naturally to iCalendar VEVENT/RRULE patterns. Most calendar and scheduling libraries implement RFC 5545.

**RFC 5321 / RFC 5322 — SMTP & Email Message Format**
- URL: https://datatracker.ietf.org/doc/html/rfc5321 / https://datatracker.ietf.org/doc/html/rfc5322
- Email delivery of reports (PDF attachments, inline HTML summaries) must conform to these IETF standards for message format and transport. Compliance ensures deliverability and proper MIME handling for rich-content report emails.

### Data Model & API Specifications

**OpenAPI Specification v3.2.0**
- URL: https://spec.openapis.org/oas/v3.2.0.html
- The dominant standard for describing RESTful HTTP APIs. An executive reporting automation tool should expose its own API (for triggering report runs, querying schedules, fetching outputs) as an OpenAPI 3.x document, enabling generated SDKs, interactive API explorers, and toolchain integration.

**JSON Schema (Draft 2020-12)**
- URL: https://json-schema.org/specification
- The standard for describing and validating the structure of JSON payloads. Report configuration objects (data sources, schedule parameters, template references, delivery targets) should be defined and validated with JSON Schema. Also used within OpenAPI specs for request/response body validation.

**OData v4 (OASIS/ISO/IEC 20802)**
- URL: https://www.odata.org/documentation/
- An OASIS-approved, ISO/IEC-ratified REST protocol for querying and updating data. OData is widely supported by enterprise data sources (Dynamics 365, SAP, Power BI datasets) and enables standardized filtering, sorting, paging, and aggregation queries. An executive reporting tool that connects to enterprise data sources will likely need OData client support.

**XBRL (eXtensible Business Reporting Language)**
- URL: https://www.xbrl.org/the-standard/what/what-is-xbrl/
- The international digital standard (developed by XBRL International, used in 50+ countries) for structured business and financial reporting. Required for SEC EDGAR filings, ESEF (European Single Electronic Format) annual reports, and FERC regulatory submissions. An AI-native executive reporting tool targeting finance teams must understand XBRL taxonomy structures for both input (reading financial data) and output (generating compliant reports).

**AsyncAPI v3.1.0**
- URL: https://www.asyncapi.com/docs/reference/specification/v3.1.0
- The industry standard for documenting event-driven and message-driven APIs, adopted by Slack, Salesforce, SAP, and now part of the Linux Foundation. Relevant for the push-notification and webhook delivery mechanisms that send report-ready signals to Slack channels, Teams workspaces, or email systems — components that OAS/REST cannot adequately describe.

**Apache Parquet / Apache Arrow**
- URL: https://arrow.apache.org/ / https://parquet.apache.org/
- De-facto columnar data format standards for analytics workloads. An executive reporting tool that sources data from data warehouses (BigQuery, Snowflake, Redshift) or data lakes will encounter Parquet as the dominant on-disk format and Arrow as the in-memory interchange format. Understanding these is essential for efficient bulk data retrieval.

### Security & Authentication Standards

**OAuth 2.0 (RFC 6749) & OpenID Connect (OIDC)**
- URL: https://datatracker.ietf.org/doc/html/rfc6749 / https://openid.net/developers/how-connect-works/
- The foundational authorization (OAuth 2.0) and authentication (OIDC) standards for enterprise API access. An executive reporting tool must implement OAuth 2.0 client credentials flow (for scheduled/unattended report runs) and authorization code flow (for user-facing data source connections). OIDC handles identity verification for SSO integration with corporate identity providers.

**SAML 2.0**
- URL: https://www.oasis-open.org/standard/saml/
- Security Assertion Markup Language, still widely used for enterprise SSO federation, particularly in large organizations connecting to on-premises identity providers. An executive reporting tool targeting enterprise buyers should support both OIDC and SAML 2.0 for identity federation.

**OWASP API Security Top 10 (2023 edition)**
- URL: https://owasp.org/www-project-api-security/
- The authoritative checklist for API security risks. An executive reporting API handles sensitive business data (revenue, headcount, strategic KPIs) and must be hardened against the OWASP API Top 10, particularly Broken Object Level Authorization (BOLA) — a common vulnerability in multi-tenant reporting systems where users could access other organizations' report data.

**OWASP Application Security Verification Standard (ASVS) v5.0**
- URL: https://owasp.org/www-project-application-security-verification-standard/
- Released May 2025, ~350 requirements across 17 chapters. Provides a measurable, verifiable standard for application security. Enterprise buyers (especially regulated industries) increasingly require ASVS conformance attestation.

**GDPR (EU 2016/679) & CCPA/CPRA**
- URL: https://gdpr.eu/ / https://oag.ca.gov/privacy/ccpa
- The primary data privacy regulatory frameworks. Executive reports frequently contain personal data (individual employee metrics, customer-level data). The reporting tool must implement data minimisation, access controls, audit logs, and right-to-erasure mechanisms to comply. CCPA regulations finalised in 2025 add privacy risk assessment requirements for high-risk processing.

### MCP Server Specifications

**Model Context Protocol (MCP)**
- URL: https://modelcontextprotocol.io/docs/getting-started/intro
- The open standard introduced by Anthropic (November 2024), adopted by OpenAI, Google, and Microsoft in 2025, and donated to the Linux Foundation (Agentic AI Foundation) in December 2025. MCP defines how AI agents connect to external data sources (databases, APIs, file systems) and tools. An AI-native executive reporting tool should expose an MCP server interface, allowing AI agents (Claude, ChatGPT, Copilot Studio) to trigger report generation, query schedules, and retrieve outputs natively — without bespoke integration work. MCP SDK downloads grew from 8M/month (March 2025) to 97M/month (November 2025).

---

## Similar Products — Developer Documentation & APIs

### Power BI REST API

- **Description:** Microsoft's REST API for Power BI provides programmatic access to all Power BI service resources — workspaces, datasets, reports, dashboards, and embedded content. Supports automation of report deployment, dataset refresh, and scheduling.
- **API Documentation:** https://learn.microsoft.com/en-us/rest/api/power-bi/
- **SDKs/Libraries:** .NET SDK (github.com/microsoft/PowerBI-CSharp), Python SDK, JavaScript Client APIs (learn.microsoft.com/en-us/javascript/api/overview/powerbi/)
- **Developer Guide:** https://learn.microsoft.com/en-us/power-bi/developer/embedded/embed-organization-app
- **Standards:** REST/JSON; Azure AD (OAuth 2.0) for authentication; OpenAPI-described endpoints
- **Authentication:** OAuth 2.0 via Azure Active Directory (Azure AD app registration required)

### Looker API (Google Cloud)

- **Description:** Google Cloud Looker's REST API provides access to the majority of Looker functionality including running queries, managing users, content, and schedules, exporting dashboards as PDF or CSV, and provisioning user accounts via automation scripts.
- **API Documentation:** https://docs.cloud.google.com/looker/docs/reference/looker-api/latest
- **SDKs/Libraries:** Ruby, Python, TypeScript/JavaScript (official Looker SDKs); docs.cloud.google.com/looker/docs/api-sdk
- **Developer Guide:** https://docs.cloud.google.com/looker/docs/api-getting-started
- **Standards:** REST/JSON; API Explorer (interactive); OpenAPI-described
- **Authentication:** OAuth 2.0 client credentials; API key pairs per Looker instance

### Tableau REST API & Embedding API

- **Description:** Tableau exposes two complementary developer surfaces: the REST API for managing users, content, and permissions on Tableau Server/Cloud; and the Embedding API v3 for integrating Tableau visualizations into custom web applications with modern authentication.
- **API Documentation:** https://www.tableau.com/developer/tools/rest-api / https://help.tableau.com/current/api/embedding_api/en-us/index.html
- **SDKs/Libraries:** JavaScript ES6 module (tableau.embedding.3.n.n.min.js); Tableau Server Client (Python)
- **Developer Guide:** https://tableau.github.io/embedding-playbook/
- **Standards:** REST/JSON; Embedding API v3 uses web components (`<tableau-viz>`); Connected Apps for token-based auth
- **Authentication:** Personal Access Tokens; Connected Apps (JWT-based); legacy username/password

### Grafana HTTP API

- **Description:** Grafana's HTTP API is the same API used by the Grafana frontend to manage dashboards, users, data sources, and alerts. The Reporting API (Enterprise only) allows programmatic interaction with scheduled PDF/PNG report generation and delivery.
- **API Documentation:** https://grafana.com/docs/grafana/latest/developer-resources/api-reference/http-api/
- **SDKs/Libraries:** Grafana Foundation SDK (TypeScript, Python, Go); community clients in multiple languages
- **Developer Guide:** https://grafana.com/docs/grafana/latest/developer-resources/api-reference/
- **Standards:** REST/JSON; Prometheus-compatible metrics endpoints; OpenTelemetry support
- **Authentication:** Service account tokens; Basic authentication; API keys (deprecated in favour of service accounts)

### Metabase API

- **Description:** Metabase (open-source BI) exposes a comprehensive REST API for managing dashboards ("reports" in Metabase terminology), questions, users, databases, and scheduled email delivery. Live OpenAPI docs are served from each running instance at `/api/docs`.
- **API Documentation:** https://www.metabase.com/docs/latest/api
- **SDKs/Libraries:** Metabase Embedding SDK (React components for modular embedding); no official server-side SDK
- **Developer Guide:** https://www.metabase.com/learn/metabase-basics/administration/administration-and-operation/metabase-api
- **Standards:** REST/JSON; OpenAPI 3.x (live docs at /api/docs); JWT-signed embeds (static embedding)
- **Authentication:** Session token (username/password); API key (for scripted access); JWT (for embedded analytics)

### Domo Developer API

- **Description:** Domo's RESTful API provides programmatic access to data import/export, user/group management, card and dataset operations, and Domo app interactions. Supports building custom Domo Apps and automating data pipelines.
- **API Documentation:** https://developer.domo.com / https://knowledge.domo.com/Develop/Domo_APIs
- **SDKs/Libraries:** Python SDK, Java SDK; connector framework for custom data connectors
- **Developer Guide:** https://developer.domo.com (API Explorer available)
- **Standards:** REST/JSON; OAuth 2.0 authentication
- **Authentication:** OAuth 2.0 (client ID + client secret)

### Looker Studio (Google Data Studio) API & Community Connectors

- **Description:** The Data Studio/Looker Studio API manages and migrates assets within a Google Workspace or Cloud Identity organization. The Community Connectors framework (Google Apps Script) allows custom data source integration via `getConfig()`, `getSchema()`, and `getData()` functions. The Linking API enables deep-linking to reports with pre-applied filters.
- **API Documentation:** https://developers.google.com/data-studio/integrate/api
- **SDKs/Libraries:** Google Apps Script (for Community Connectors); no external SDK
- **Developer Guide:** https://developers.google.com/looker-studio/connector / https://codelabs.developers.google.com/codelabs/community-connectors
- **Standards:** REST/JSON (Data Studio API); Google Apps Script (Connectors); Linking API URL-based
- **Authentication:** Google OAuth 2.0 (service accounts for asset management)

### Slack Web API & Incoming Webhooks

- **Description:** Slack provides two delivery surfaces relevant to executive report distribution: Incoming Webhooks (simple, unique URL per channel for posting formatted messages with report summaries) and the Web API (full bot/app API for richer integrations including file uploads and interactive messages).
- **API Documentation:** https://docs.slack.dev/ / https://api.slack.com/messaging/webhooks
- **SDKs/Libraries:** Bolt SDK (JavaScript, Python, Java); Slack Web API clients in all major languages
- **Developer Guide:** https://docs.slack.dev/
- **Standards:** REST/JSON; Block Kit for rich message formatting; Incoming Webhooks accept JSON payloads
- **Authentication:** Bot tokens (OAuth 2.0); Incoming Webhook URLs (HMAC-signed)

### Microsoft Teams Incoming Webhooks & Graph API

- **Description:** Microsoft Teams supports Incoming Webhooks for posting formatted report summaries to channels (Adaptive Cards format). The Microsoft Graph API provides broader access to Teams messaging, user management, and calendar scheduling for report delivery.
- **API Documentation:** https://learn.microsoft.com/en-us/microsoftteams/platform/webhooks-and-connectors/how-to/add-incoming-webhook
- **SDKs/Libraries:** Microsoft Graph SDK (C#, Python, JavaScript, Java, Go); Teams Bot Framework
- **Developer Guide:** https://learn.microsoft.com/en-us/microsoftteams/platform/
- **Standards:** REST/JSON; Adaptive Cards (cross-platform card format); Bot Framework protocol
- **Authentication:** OAuth 2.0 via Azure AD; Incoming Webhooks use per-connector URL (no auth token on payload)

---

## Notes

**Evolving Areas**

- **MCP ecosystem:** The MCP server specification is evolving rapidly. The Linux Foundation donation (December 2025) signals long-term stability, but tooling and hosted-server patterns are still maturing. Monthly SDK downloads approaching 100M by end of 2025 indicate strong and accelerating adoption.
- **XBRL and AI:** Integrating XBRL taxonomy awareness into an AI-native reporting tool is technically complex but represents a significant differentiator for regulated industries (financial services, public companies). XBRL parsers in Python (Arelle) and Java are available under open-source licences.
- **AsyncAPI adoption:** Still in early adoption relative to OpenAPI. An executive reporting tool that sends push notifications (report-ready signals, anomaly alerts) would benefit from AsyncAPI documentation for its webhook and event interfaces.
- **Report delivery standards gap:** There is no universal standard specifically for report delivery scheduling or report interchange formats. XBRL addresses financial report structure; iCalendar addresses scheduling; neither provides a complete "report definition language." This is an opportunity for the AI-native tool to define its own open schema (documented with JSON Schema + OpenAPI), potentially contributing to emerging industry practices.
- **Privacy compliance in 2026:** With California's CCPA 2025 regulations taking effect January 2026 and 16 US states now having comprehensive privacy laws, any executive reporting tool processing employee or customer-level data needs robust data access controls, audit logging, and data minimisation features from v1.
