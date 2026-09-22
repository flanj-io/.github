<picture>
  <source media="(prefers-color-scheme: dark)" srcset="flanj-lockup-dark.svg">
  <img src="flanj-lockup.svg" alt="Flanj" width="166" height="48">
</picture>

# Flanj

**Your integration didn't break. It started being wrong.** Every call succeeded. That's why nothing
caught it.

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

## Get started

The collector runs in your environment; the SDK runs in your app. Two ways to run the collector, both
from the [collector README](https://github.com/flanj-io/collector#readme):

**Kubernetes (preferred)** — [Run it on Kubernetes](https://github.com/flanj-io/collector#run-it-on-kubernetes)

```bash
helm install flanj oci://registry-1.docker.io/flanj/flanj-collector \
  --namespace flanj --create-namespace \
  --set specToken.value="$(openssl rand -hex 32)"
```

**Docker** — [Run it with Docker](https://github.com/flanj-io/collector#run-it-with-docker)

```bash
curl -fsSLO https://raw.githubusercontent.com/flanj-io/collector/main/docker-compose.yml
docker compose up -d
```

Then point your app at it — `npm install @flanj/sdk` and `node -r @flanj/sdk/register app.js`
([Node quick start](https://github.com/flanj-io/sdk#quick-start)), or `pip install flanj` and
`import flanj.register` as the first line ([Python quick start](https://github.com/flanj-io/sdk-py#quick-start)).
On Docker the SDK's default endpoint is already the collector; on Kubernetes give your workload
`FLANJ_OTLP_ENDPOINT=http://flanj-collector.flanj:4318/v1/logs`, and for Node the preload as well
(`NODE_OPTIONS="--require @flanj/sdk/register"`). Make a few calls, open the UI at
<http://localhost:5335> (on Kubernetes, after `kubectl -n flanj port-forward sts/flanj-flanj-collector-store 5335:5335`)
and watch **Traffic** fill.

Everything above works with nothing leaving your network. To flag drift to the team on the other side,
set the collector's control plane to `https://app.flanj.io` (`cp_base_url` in its config, or
`controlPlane.baseUrl` on the chart) and press **Connect** in its Settings; the confirmation mail adds
the collector to your workspace at [app.flanj.io](https://app.flanj.io/d).

## Repositories

- [collector](https://github.com/flanj-io/collector) — an OpenTelemetry Collector distribution with
  redaction, drift detection, a local store and a local UI; ships as an image and a Helm chart.
  Elastic License 2.0.
- [sdk](https://github.com/flanj-io/sdk) — `@flanj/sdk`, a thin OpenTelemetry distribution for
  Node that captures HTTP bodies and MCP client traffic and redacts them at the source. Apache-2.0.
- [sdk-py](https://github.com/flanj-io/sdk-py) — `flanj` on PyPI, the same capture for Python's
  MCP client. Early: MCP only, no HTTP body capture yet. Apache-2.0.

## Elsewhere

- [flanj.io](https://flanj.io) — the site.
- [app.flanj.io](https://app.flanj.io/d) — the hosted workspace: every thread you are part of, and the
  collectors you connected. Signing in with your email creates it.
- [drift.flanj.io](https://drift.flanj.io) — a daily record of MCP tool-contract drift, breaking schema
  changes and reworded descriptions, per server per day.
