<picture>
  <source media="(prefers-color-scheme: dark)" srcset="flanj-lockup-dark.svg">
  <img src="flanj-lockup.svg" alt="Flanj" width="166" height="48">
</picture>

# Flanj

Nothing threw. Nothing 500'd. The response was 200 OK and a field was renamed. Your integration
didn't break — it started being wrong, and every tool that waits for an error is blind to it.

**Everyone is building ways to evaluate the agent misusing a tool. Nobody evaluates the tool misusing
the agent.** Agents are the most drift-fragile API consumers anyone has built: an agent reads a
tool's description to decide what to do, so a description that moves underneath it changes what it
does — quietly, and with no error anywhere. Which tool *should* have been called is the customer's
ground truth. What the tool promised, and what it promises now, is ours.

An open-source SDK and a source-available collector run inside your own environment, record the
request and response bodies of the calls your services and agents make and receive, redact them
before they are stored, and detect contract drift with evidence. Raw bodies never leave your
environment; a call you flag crosses the org boundary redacted, and only when you send it. A hosted
network layer carries that evidence-backed flag into a shared thread, where an engineer on the other
side can read the redacted failing call and reply without installing anything.

REST drift detection needs a spec somebody published and kept accurate; an MCP server publishes its
contract on every single call — `tools/list` **is** the spec — so for MCP there is nothing to
configure at all. Node is supported; Python is early, MCP client only.

## Repositories

- [sdk](https://github.com/flanj-io/sdk) — `@flanj/sdk`, a thin OpenTelemetry distribution for
  Node that captures HTTP bodies and redacts them at the source. Apache-2.0.
- [collector](https://github.com/flanj-io/collector) — an OpenTelemetry Collector distribution with
  redaction, drift detection, a local store and a local UI. Elastic License 2.0.

## Elsewhere

- [flanj.io](https://flanj.io) — the site.
- [drift.flanj.io](https://drift.flanj.io) — a daily record of MCP tool-contract drift, breaking schema
  changes and reworded descriptions, per server per day. A preview until launch.
