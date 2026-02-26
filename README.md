# GCP Multi-Region Public Sector Cloud Migration Framework (HLD)

This project demonstrates a GDS-aligned, multi-region public sector architecture built on Google Cloud Platform (GCP).

The solution migrates a legacy public sector web workload into a secure, scalable, and highly available cloud-native environment.

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

---

## Deployment & Security Evidence

### Successful Cloud Run Deployment (europe-west2)

![Cloud Run Deployment Success](docs/evidence/01-cloud-run-deployment-success.png)

---

### Direct Cloud Run Access Blocked (After Ingress Restriction)

After removing public invoker permissions and restricting ingress to Load Balancer only, direct service access returns HTTP 403 (Forbidden):

![Direct Access Forbidden](docs/evidence/02-direct-access-forbidden-after-hardening.png)

## Next Phase

- Enforce Identity-Aware Proxy (IAP)
- Remove public access from Cloud Run
- Optional: Cloud Armor integration

