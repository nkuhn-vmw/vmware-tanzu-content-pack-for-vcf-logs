# VMware Tanzu Platform Content Pack for VCF Operations for Logs

A content pack for VMware Aria Operations for Logs (VCF Operations for Logs) that provides dashboards, extracted fields, and alerts for monitoring VMware Tanzu Platform (formerly Pivotal Cloud Foundry / TAS) deployments.

## Dashboards

| Dashboard | Description |
|-----------|-------------|
| **Overview** | Total log volume, events by BOSH job, product, availability zone, and environment |
| **Gorouter** | HTTP request metrics, status code distribution, 5xx errors, slowest routes, requests by app/method |
| **Diego** | Container orchestration events, errors, crash events, events by origin and deployment |
| **Cloud Controller** | API events, CC events by app/space/org, error tracking |
| **UAA Security** | Authentication events, failures, successes, events by app and organization |
| **Application Logs** | App log volume, source types, crash/staging events, logs by org/space/app |

## Extracted Fields (51)

The content pack extracts fields from the following log sources:

- **BOSH** — deployment, availability zone, director, instance group, instance ID, job ID
- **Product & Environment** — product name, environment ID
- **Organization / Space / App** — org name, space name, app name (from structured data)
- **Gorouter (RTR)** — request host, method, path, status code, response time, backend time, gorouter time, app ID, app index, error type, VCAP request ID, X-Forwarded-For, bytes sent
- **Diego** — source component, log message, log level
- **Cloud Controller** — CEF signature ID, event name, user, request path, status, result, auth mechanism, source IP
- **UAA** — event type, principal, origin, identity zone
- **Loggregator** — source type, envelope type
- **Application Logs** — source type, instance index
- **Garden** — container handle

## Alerts (8)

| Alert | Condition |
|-------|-----------|
| High Error Rate | Spike in ERROR/FATAL severity events |
| App Crash Storm | High volume of app crash (CRASHED) events |
| 5xx Error Spike | Elevated 5xx HTTP status codes from Gorouter |
| Diego Cell Unhealthy | Cell evacuation or rep connection failure events |
| UAA Auth Failure Spike | High volume of authentication failures |
| CC API Error Spike | Elevated Cloud Controller error responses |
| Gorouter Latency | Backend response times exceeding thresholds |
| Dropped Log Messages | Loggregator dropping messages (pipeline backpressure) |

## Requirements

- VMware Aria Operations for Logs 8.x+ / VCF Operations for Logs 9.x+
- Syslog forwarding configured from your Tanzu Platform deployment

## Installation

1. Download `Tanzu_Platform_Cloud_Foundry-v1.0.vlcp`
2. In Operations for Logs, navigate to **Content Pack Marketplace** > **+ Import Content Pack**
3. Select the `.vlcp` file and import

## Syslog Configuration

Configure your Tanzu Platform to forward logs to your Operations for Logs instance:

### TAS Ops Manager
1. **TAS tile** > **System Logging** > set the syslog endpoint address and port
2. Enable **Include container metrics in Syslog Drains** for app-level metrics

### BOSH Director
1. **BOSH Director tile** > **Syslog** > configure the syslog endpoint
2. This enables component-level logs (Diego, CC, UAA, Gorouter, etc.)

## Compatibility

| Platform | Version | Status |
|----------|---------|--------|
| VMware Tanzu Application Service (TAS) | 4.x, 5.x, 6.x | Tested |
| Pivotal Cloud Foundry (PCF) | 2.x | Expected compatible |
| VMware Aria Operations for Logs | 8.12+ | Tested |
| VCF Operations for Logs | 9.x | Tested |

## License

Apache License 2.0
