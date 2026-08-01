---
title: "Health Checks"
type: concept
sources:
  - raw/papers/Implementing health checks.md
related:
  - "[[implementing-health-checks]]"
created: 2026-08-02
updated: 2026-08-02
confidence: high
---

Health checks ask a service on a particular server whether it is capable of performing work successfully. They detect and respond to single-server failures that would otherwise go unnoticed, because servers rarely fail cleanly — they fail partially and can cause disproportionate harm (e.g., a broken server answering quickly becomes a "black hole" that attracts more traffic under least-requests load balancing).

## Hierarchy of Checks

1. **Liveness** — basic connectivity: listening on expected port, accepts TCP, returns HTTP 200. Usually built into the service (EC2 status checks, load balancer pings). No application authoring required.
2. **Local health checks** — verify resources not shared with peers: disk read/write, critical processes, support processes (monitoring daemons, metering). Unlikely to false-positive fleet-wide.
3. **Dependency health checks** — verify interaction with adjacent systems: credentials, config/metadata freshness, network connectivity to dependencies. Powerful but dangerous: a dependency outage becomes a cascading failure unless fail-open protection exists.
4. **Anomaly detection** — compare aggregated per-server metrics (error rates, latency) against fleet peers. Catches what a server can't detect about itself: clock skew, stale code, unanticipated failure modes. Requires homogeneous fleets and that errors actually get reported.

## Central Tradeoff

Thoroughness vs. false positives. The ideal check tests everything — but if a non-critical check fails and the failure is correlated across the fleet, automation that removes servers does more harm than good. The rule: stop directing traffic to a single bad server, but keep traffic flowing if the entire fleet appears to have trouble.

## Reacting Safely

- **Fail open** — load balancers (Route 53, NLB, ALB) send traffic to all servers when all fail health checks at once. Useful but hard to reason about for partial/gray failures; Amazon restricts fast-acting LB checks to local health checks.
- **Centralized actors** — servers report problems to a central authority that decides how to react, instead of acting locally.
- **Rate-limiting and thresholding** — automation stops and engages humans when thresholds are crossed (critical for stateful servers with durability requirements like DynamoDB, S3, RDS).
- **Health checks without a circuit breaker** — configure the work producer (load balancer, queue poller) for liveness/local checks only; external monitoring systems handle dependency checks and anomaly detection.

## Prioritize Health Over Work

In overload, slow health-check responses shrink the fleet and cause a downward spiral. Best practices: reserve worker threads for health-check pings (idle workers are cheap), enforce max connections, implement own concurrent-request limits, run dependency checks in a background thread updating an `isHealthy` flag.

## Failure Patterns and Compensating Controls

- **Deployments** — deploy scripts that report "done" before the code actually works. Mitigations: fleet-size/error-rate alarms that halt and roll back, phased per-AZ deployments with integration tests.
- **Async processors** — queue pollers with shallow checks pull work they can't process. Mitigation: SQS redelivery on visibility timeout, error alarms.
- **Disks filling up** — kills logging and monitoring visibility. Mitigation: proxy-level (ALB/API Gateway) error/latency metrics, SQS processing-delay metrics.
- **Zombie servers** — stale servers coming back online out of sync. Mitigation: reply to health checks with software version, compare across fleet, block outdated servers from re-entering service.

External systems test a server's health more accurately than the server tests itself; combine self-reporting with external checks ("belt and suspenders").
