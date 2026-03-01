# GCP Multi-Region Public Sector Cloud Migration Framework (HLD)

This project demonstrates the design and validation of a production-style, multi-region Google Cloud architecture suitable for public sector and regulated workloads.

The solution includes:

- Global HTTPS Load Balancer
- Google-managed SSL certificate
- Multi-region Serverless Network Endpoint Groups (NEGs)
- Cloud Run backend services
- TLS termination at the edge
- Cost-aware decommissioning strategy

---

## What This Demonstrates

This repository validates practical capability in:

- Designing global, highly available architectures
- Implementing serverless multi-region backends
- Configuring Google-managed SSL and TLS termination
- Applying layered security patterns
- Managing infrastructure lifecycle with cost awareness (FinOps mindset)

All infrastructure was provisioned, validated, and decommissioned within GCP Free Tier constraints.

---

## Architecture Overview

![Target Architecture](docs/architecture/01-target-architecture-multi-region-cloud-run.png)

---

## Key Components

- Global External HTTPS Load Balancer (Premium Tier / Anycast IP)
- L7 URL Routing (URL Map)
- Backend Service abstraction layer
- Serverless Network Endpoint Groups (eu-west1 & eu-west2)
- Multi-region Cloud Run deployment
- TLS termination at Load Balancer
- Ingress restricted to Load Balancer only
- Planned Identity-Aware Proxy (IAP) enforcement

---

## Current State

- Multi-region deployment operational
- Load balancer routing correctly
- Public access temporarily enabled for validation
- ✅ Identity-Aware Proxy (IAP) enforced at Load Balancer layer
- ✅ Backend services protected via OAuth2 identity validation

---

## Deployment & Security Evidence

### Successful Cloud Run Deployment (europe-west2)

![Cloud Run Deployment Success](docs/evidence/01-cloud-run-deployment-success.png)

---

### Direct Cloud Run Access Blocked (After Ingress Restriction)

After removing public invoker permissions and restricting ingress to Load Balancer only, direct service access returns HTTP 403 (Forbidden):

![Direct Access Forbidden](docs/evidence/02-direct-access-forbidden-after-hardening.png)

---

### Identity-Aware Proxy (IAP) Enforcement

- IAP enabled at Load Balancer backend service layer
- OAuth2 authentication enforced before request reaches Cloud Run
- Only authorised Google identities granted access
- Direct backend access blocked (403)

Architecture now follows zero-trust identity perimeter model.

---

### HTTPS Validation

Global HTTPS Load Balancer successfully provisioned with:

- Google-managed SSL certificate (ACTIVE)
- Serverless NEGs across multiple regions
- Cloud Run backend services
- Global static IP with TLS termination

Validated using nip.io domain mapping for TLS verification.

All infrastructure was decommissioned after validation to optimise cost.

---

### Architecture Validation Screenshots

#### Global HTTPS Load Balancer
![Global HTTPS LB](screenshots/01-global-https-lb-overview.png)

#### SSL Certificate (ACTIVE)
![SSL Certificate](screenshots/02-ssl-certificate-active.png)

#### Successful HTTPS Access via nip.io
![HTTPS Working](screenshots/03-https-global-lb-working.png)

#### Serverless Network Endpoint Groups (Multi-Region)
![Serverless NEGs](screenshots/04-serverless-neg-multi-region.png)

#### Cloud Run Backend Services
![Cloud Run](screenshots/05-cloud-run-service.png)

---

## Cost Management Strategy

All production-grade infrastructure was provisioned for validation and immediately decommissioned to minimise spend within GCP Free Tier constraints.

This demonstrates real-world FinOps awareness alongside architectural capability.

---

## Security Hardening Roadmap (next steps)

The validated deployment focused on TLS termination and multi-region availability.

Next-stage enhancements for production readiness include:

- Enforcing Identity-Aware Proxy (IAP) for zero-trust access
- Restricting Cloud Run ingress to internal + load balancer only
- Applying Cloud Armor WAF policies
- Enforcing organisation policy constraints for public endpoint prevention






