<picture>
  <source media="(prefers-color-scheme: dark)" srcset="flanj-lockup-dark.svg">
  <img src="flanj-lockup.svg" alt="Flanj" width="166" height="48">
</picture>

# Flanj

Cross-org integration reliability. Flanj detects contract drift where your traffic is, redacted at
the source, and carries evidence the provider can verify across the org boundary into a thread both
teams can act on.

Integrating is the easy part; keeping the integration alive is the work, and it is shared between the
team that ships an API and the team that consumes it. An open-source SDK and a source-available
collector run inside your own environment, record the request and response bodies of the calls your
services make and receive, redact them before they are stored, and detect schema drift with evidence.
Raw bodies never leave your environment; a call you flag crosses the boundary redacted, and only when
you send it. A hosted network layer carries that evidence-backed flag into a shared thread, where a
provider engineer can read the redacted failing call and reply without installing anything.

## Repositories

- [sdk](https://github.com/flanj-io/sdk) — `@flanj/sdk`, a thin OpenTelemetry distribution for
  Node that captures HTTP bodies and redacts them at the source. Apache-2.0.
- [collector](https://github.com/flanj-io/collector) — an OpenTelemetry Collector distribution with
  redaction, drift detection, a local store and a local UI. Elastic License 2.0.

## Elsewhere

- [flanj.io](https://flanj.io) — the site.
- [drift.flanj.io](https://drift.flanj.io) — a daily record of MCP tool-contract drift, breaking schema
  changes and reworded descriptions, per server per day. A preview until launch.
