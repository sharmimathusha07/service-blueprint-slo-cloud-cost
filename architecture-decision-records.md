# Architecture Decision Records

## ADR-001 — Region Selection
**Decision:** Select a cloud region geographically appropriate for the target users.

**Reason:** A nearby region generally reduces network latency and supports the latency SLO.

**Trade-off:** A single region is simpler and cheaper; multi-zone/multi-region resilience increases cost and operational complexity.

## ADR-002 — Recovery Objectives
**Decision:** Define RPO and RTO before selecting backup and recovery mechanisms.

| Scenario | RPO | RTO |
|---|---:|---:|
| Lean | 1440 min | 240 min |
| Balanced | 60 min | 60 min |
| Resilient | 15 min | 30 min |

## ADR-003 — Secrets Management
**Decision:** Keep credentials and API secrets outside source code and Git history.

**Implementation:** Use a managed secrets service or protected environment variables.

**Security rule:** Do not upload `.env` files containing real secrets.

## ADR-004 — Least-Privilege Access
**Decision:** Use separate identities/roles with only the permissions needed for each component.

**Examples:**
- Application role: application data access only.
- Deployment role: deployment permissions only.
- Monitoring role: read-only observability access.
- Database administration: restricted administrative access.

## ADR-005 — Backup Strategy
**Decision:** Use automated backups and periodically test restoration.

**Reason:** A backup that has never been restored/tested cannot reliably demonstrate the RPO/RTO objective.
