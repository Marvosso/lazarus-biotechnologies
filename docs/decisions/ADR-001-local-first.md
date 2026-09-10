# ADR-001 — Local-First Infrastructure

**Status:** Accepted  
**Date:** 2026-09-10
**Supersedes:** None

## Context

Lazarus Biotechnologies requires persistent enterprise infrastructure
capable of generating realistic security telemetry while maintaining
minimal recurring operating costs.

Deploying the entire environment in a public cloud would increase
recurring costs without providing equivalent educational value for
every workload.

## Decision

Persistent compute workloads will run locally whenever practical.

Cloud services will be introduced when they provide meaningful
technical or educational capabilities that cannot reasonably be
reproduced locally.

Organizational scale may be simulated while representative systems
produce genuine security telemetry.

## Alternatives Considered

### Cloud-First

Deploy most infrastructure within Microsoft Azure.

Rejected because persistent compute and telemetry could create
unnecessary recurring costs.

### Fully Local

Keep all infrastructure local.

Rejected because this would unnecessarily eliminate opportunities to
gain experience with real cloud identity and security technologies.

### Hybrid Local-First

Use local infrastructure for persistent workloads and targeted cloud
services where justified.

Selected.

## Rationale

The hybrid local-first approach supports the project's $0 recurring
cost target while preserving opportunities to work with enterprise
cloud technologies.

## Security Implications

Local infrastructure must be properly segmented and isolated.

Cloud credentials and secrets must never be stored in the public
repository.

Attack simulations must remain limited to systems specifically
authorized for testing.

## Cost Implications

Target recurring cost: $0/month.

Soft ceiling: $10/month.

Cloud resources exceeding the project's normal cost constraints
require explicit justification.

## Consequences

Local hardware capacity becomes an architectural constraint.

Some enterprise-scale behavior will need to be simulated rather than
physically reproduced.

Cloud exercises may need to be temporary to control costs.
