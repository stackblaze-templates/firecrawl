# Firecrawl [![Version](https://img.shields.io/badge/version-1-ff6900)](https://github.com/stackblaze-templates/firecrawl) [![Maintained by StackBlaze](https://img.shields.io/badge/maintained%20by-StackBlaze-blue)](https://stackblaze.com) [![Weekly Updates](https://img.shields.io/badge/updates-weekly-green)](https://github.com/stackblaze-templates/firecrawl/actions) [![License](https://img.shields.io/github/license/stackblaze-templates/firecrawl)](LICENSE) [![Deploy on StackBlaze](https://img.shields.io/badge/Deploy%20on-StackBlaze-orange)](https://stackblaze.com)

<p align="center"><img src="logo.png" alt="firecrawl" width="120"></p>

An AI-ready web scraper. Turn any website into clean, LLM-ready markdown or structured data via API.

> **Credits**: Built on [Firecrawl](https://firecrawl.dev) by [Mendable](https://github.com/mendableai). All trademarks belong to their respective owners.

## Local Development

```bash
docker compose up
```

See the project files for configuration details.

## Deploy on StackBlaze

[![Deploy on StackBlaze](https://img.shields.io/badge/Deploy%20on-StackBlaze-orange)](https://stackblaze.com)

This template includes a `stackblaze.yaml` for one-click deployment on [StackBlaze](https://stackblaze.com). Both options run on **Kubernetes** for reliability and scalability.

<details>
<summary><strong>Standard Deployment</strong> — Single-instance Kubernetes setup for startups and moderate traffic</summary>

<br/>

```mermaid
flowchart LR
    U["Customers"] -->|HTTPS| LB["Edge Network\n+ SSL"]
    LB --> B["Firecrawl\nNode.js"]

    style LB fill:#ff9800,stroke:#e65100,color:#fff
    style B fill:#0041ff,stroke:#002db3,color:#fff
```

**What you get:**
- Single Firecrawl instance on Kubernetes
- Automatic SSL/TLS via StackBlaze edge network
- Automated daily backups
- Zero-downtime deploys

**Best for:** Development, staging, and moderate-traffic production environments.

</details>

<details>
<summary><strong>High Availability Deployment</strong> — Multi-instance Kubernetes setup for business-critical production</summary>

<br/>

```mermaid
flowchart LR
    U["Customers"] -->|HTTPS| CDN["CDN\nStatic Assets"]
    CDN --> LB["Load Balancer\nAuto-scaling"]
    LB --> B1["Firecrawl #1"]
    LB --> B2["Firecrawl #2"]
    LB --> B3["Firecrawl #N"]
    B1 --> R[("Redis\nSessions + Cache")]
    B2 --> R
    B3 --> R

    style CDN fill:#607d8b,stroke:#37474f,color:#fff
    style LB fill:#ff9800,stroke:#e65100,color:#fff
    style B1 fill:#0041ff,stroke:#002db3,color:#fff
    style B2 fill:#0041ff,stroke:#002db3,color:#fff
    style B3 fill:#0041ff,stroke:#002db3,color:#fff
    style R fill:#f44336,stroke:#c62828,color:#fff
```

**What you get:**
- Auto-scaling Firecrawl pods on Kubernetes behind a load balancer
- Redis for shared sessions, cache, and queue management
- CDN for static assets
- Automated failover and self-healing
- Zero-downtime rolling deploys

**Best for:** Production workloads, high-traffic applications, business-critical deployments.

</details>

## Security

### Required environment variables

Before deploying to production, set the following in your environment:

| Variable | Description | Required |
|---|---|---|
| `FIRECRAWL_API_KEY` | API key for authenticating requests to the Firecrawl API | **Yes** |
| `REDIS_URL` | Redis connection URL (e.g. `redis://redis:6379`) | **Yes** |

### Production hardening checklist

- **`FIRECRAWL_API_KEY`**: Always set a strong, randomly generated API key. The `stackblaze.yaml` configures this to be auto-generated on StackBlaze deployments.
- **Redis**: Do not expose the Redis port publicly. It is intentionally not mapped to a host port in `docker-compose.yml`.
- **Network exposure**: Only port `3002` (the Firecrawl API) should be reachable externally. Restrict access at the firewall/ingress level as needed.
- **`NODE_ENV`**: Set to `production` (already configured in `docker-compose.yml`) to disable development-mode debug output.

---

### Maintained by [StackBlaze](https://stackblaze.com)

This template is actively maintained by StackBlaze. We perform **weekly automated checks** to ensure:

- **Up-to-date dependencies** — frameworks, libraries, and base images are kept current
- **Security scanning** — continuous monitoring for known vulnerabilities and CVEs
- **Best practices** — configurations follow current recommendations from upstream projects

Found an issue? [Open a ticket](https://github.com/stackblaze-templates/firecrawl/issues).
