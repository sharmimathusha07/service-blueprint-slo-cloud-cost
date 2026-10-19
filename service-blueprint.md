# Service Blueprint

## Two-Tier Architecture

```text
User
  |
  v
HTTPS / DNS
  |
  v
Application / API Tier
  |               v              v
Database       Monitoring & Logs
  |
  v
Backups

Failure path:
Application/Database failure
        ↓
Monitoring detects issue
        ↓
Alert / Page
        ↓
Rollback, restart, failover or restore backup
        ↓
Service recovery
```

## Request Flow
1. User sends an HTTPS request.
2. DNS routes the request to the application endpoint.
3. Application/API validates the request and applies business logic.
4. Application reads/writes required data in the managed database.
5. Logs and metrics are collected.
6. Response is returned to the user.

## Deployment Flow
Source code → build/test → deployment → application tier → health check → monitoring.

## Data & Recovery
Application data is stored in the database and protected by scheduled backups. Recovery objectives are defined by RPO and RTO.

## Failure Scenarios
- Application instance failure → restart/redeploy or autoscale.
- Database failure → failover/restore according to architecture.
- Deployment failure → rollback to the previous stable version.
- Excess traffic → autoscaling where supported.
