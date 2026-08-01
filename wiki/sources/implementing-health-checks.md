---
title: "Implementing Health Checks"
type: source-summary
sources:
  - raw/papers/Implementing health checks.md
related:
  - "[[health-checks]]"
created: 2026-08-02
updated: 2026-08-02
confidence: high
---

AWS whitepaper by David Yanacek (2019) on using health checks to detect and respond to single-server failures in distributed systems. Servers don't fail cleanly — they enter partially-broken states that can disproportionately harm the system (e.g., a bug that made servers render blank pages faster than healthy ones, causing load balancers to route more traffic to the broken servers — a "black hole").

## Key Ideas

- **Hierarchy of checks**: liveness (basic connectivity), local health checks (disk writes, critical processes, support processes), dependency health checks (interaction with adjacent systems, can false-positive on correlated failures), anomaly detection (compare per-server metrics against fleet peers).
- **Central tradeoff**: thoroughness of checks vs. false positives. When a non-critical check fails fleet-wide, automation that removes servers does more harm than good. Guard heavily against false positives; stop directing traffic to a single bad server but keep traffic flowing if the whole fleet looks troubled.
- **Safe reactions**: fail-open load balancers (Route 53, NLB, ALB), centralized actors that decide before acting, rate-limiting and thresholding on automation, circuit breakers that engage humans in uncertainty.
- **Failure patterns**: bad deployments (deploy waves that keep breaking servers), async queue pollers as black holes, disks filling up (kills monitoring visibility), zombie servers (stale versions; answer health checks with software version and compare across fleet).
- **Best practices**: prioritize health checks over regular work in overload (extra worker threads, max connections, background-thread `isHealthy` flag), external systems test health more accurately than self-report, multiple layers of monitoring ("belt and suspenders").
