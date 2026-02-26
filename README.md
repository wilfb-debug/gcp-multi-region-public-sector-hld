# GCP Multi-Region Public Sector Cloud Migration Framework (HLD)

## Project Overview

This project demonstrates a GDS-aligned multi-region public sector application architecture built on Google Cloud Platform (GCP).

The solution migrates a legacy public sector web workload into a secure, scalable, and highly available cloud-native environment using:

- Cloud Run (Serverless Compute)
- Global External HTTPS Load Balancer
- Serverless Network Endpoint Groups (NEGs)
- Multi-region deployment (europe-west1 & europe-west2)

This architecture is designed to meet OFFICIAL-SENSITIVE public sector requirements including high availability, perimeter security, and controlled ingress.

---

## Architecture Summary

Internet traffic enters via a Global External Application Load Balancer (Premium Tier).  
Traffic is routed to backend services connected to serverless NEGs in:

- europe-west1 (Belgium)
- europe-west2 (London)

Ingress to Cloud Run services is restricted to load balancer traffic only.

High availability is achieved through multi-region deployment and global load distribution.

---

## Security Posture (Lab Phase)

- Cloud Run ingress restricted to external application load balancers
- Direct run.app endpoints disabled
- HTTPS termination at load balancer
- Global Anycast IP
- IAM temporarily relaxed for lab validation
- Cloud Armor (Standard tier implied via HTTPS LB)

Production environments would enforce Identity-Aware Proxy (IAP) and remove public invocation permissions.

---

## High Availability Design

- Multi-region Cloud Run deployment
- Global Load Balancer with Premium Tier
- Automatic failover between regions
- Serverless auto-scaling

Target Availability: 99.9%+

---

## Future Enhancements (Production Model)

- Identity-Aware Proxy (IAP)
- Private Service Connect
- Dedicated Interconnect for hybrid connectivity
- Cloud SQL with private IP
- VPC Service Controls
- Cloud KMS CMEK encryption
- Audit logging & SCC integration

---

## Skills Demonstrated

- GCP Load Balancing (L7)
- Serverless NEGs
- Multi-region architecture
- IAM and ingress control
- Public sector security design patterns
- High-Level Design (HLD) documentation
