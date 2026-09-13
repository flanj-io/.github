<picture>
  <source media="(prefers-color-scheme: dark)" srcset="profile/flanj-lockup-dark.svg">
  <img src="profile/flanj-lockup.svg" alt="Flanj" width="166" height="48">
</picture>

# Flanj

Cross-org integration reliability. Flanj detects contract drift where your traffic is, redacted at
the source, and carries evidence the provider can verify across the org boundary into a thread both
teams can act on.

Integrating is the easy part; keeping the integration alive is the work, and it is shared between the
team that ships an API and the team that consumes it. An open-source SDK and a source-available
collector run inside your own environment, record the request and response bodies of the calls your
services make and receive, redact them before they are stored, and detect schema drift with evidence.
Bodies never leave your environment. A hosted network layer carries an evidence-backed flag across
the org boundary into a shared thread, where a provider engineer can read the failing call and reply
without installing anything.

## Repositories

- [sdk](https://github.com/flanj-io/sdk) — `@flanj/sdk`, a thin OpenTelemetry distribution for
  Node that captures HTTP bodies and redacts them at the source. Apache-2.0.
- [collector](https://github.com/flanj-io/collector) — an OpenTelemetry Collector distribution with
  redaction, drift detection, a local store and a local UI. Elastic License 2.0.

## Elsewhere

- [flanj.io](https://flanj.io) — the site.
- [drift.flanj.io](https://drift.flanj.io) — a public dataset of description drift across MCP servers,
  observed daily. A preview until launch.
