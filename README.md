# DeviceBridge-Perfomance Testing

## Overview
This repository contains the complete setup, deployment instructions, test strategies, and architecture for validating DeviceBridge v4.3.8. The focus is on ensuring reliable, high-volume data integration from medical devices such as infusion pumps and hospital beds, while supporting nurse call alerts, Vault Mobile communication, and backend monitoring.

---

## Environment Setup
Describes how to provision the infrastructure needed to run DeviceBridge:
- **VM Provisioning**: Create 3–4 VMs with recommended specs (4 vCPU, 16–32GB RAM).
- **Disk Layout**: Allocate four 120GB thick-provisioned virtual disks (App, PostgreSQL, MongoDB, Backup).
- **Kubernetes Installation**: Deploy a K8s cluster and configure nodes.
- **Secrets Management**: Store AWS keys and DB credentials securely (e.g., in Kubernetes secrets).

---

## Platform Components
Defines all services deployed within Kubernetes to support DeviceBridge:
- **PostgreSQL**: Stores relational data like configuration, metadata.
- **MongoDB**: Stores telemetry from devices in near real-time.
- **MinIO**: Secure S3-compatible storage for backups or bulk data.
- **DeviceBridge Core Services**: Main service layer that manages data ingest, routing, and alerting logic.

---

## Integration Modules

### Infusion Pumps
Outlines how infusion pumps are integrated and tested:
- **YAML Files**: Used for deploying DeviceBridge pump ingestion services.
- **Integration Steps**: Gateway → MDAP → DeviceBridge → DB.
- **Test Scenarios**: Validate real-time flow, ingestion timing, and alert accuracy.

### Beds
Describes how bed monitoring data is handled:
- **BEDS Dashboard**: Visual interface for real-time bed activity.
- **Alert Flows**: Ensure alerts like bed exit or patient presence trigger correctly through Nurse Call and Vault Mobile.

---

## Monitoring & Tools
Covers the tooling used to monitor system performance and log activity:
- **Splunk Queries**: For real-time error tracking and device data logs.
- **Pod Health Scripts**: Custom shell or Python scripts to validate pod readiness and uptime.
- **Log Paths**: Document where logs are collected/stored from each container or microservice.

---

## Test Plan
Details the types of testing used to validate performance:
- **Load Testing**: Simulate high-volume concurrent devices (e.g., 100+ pumps).
- **Soak Testing**: Run system under normal load for extended durations (12–24 hrs).
- **Functional Validation**: Ensure each device integration works as intended (alert accuracy, data ingestion).

---

## Architecture Diagram
A visual representation of system flow:
- Devices (Pumps, Beds) → Gateways (IQEG, CQI, SCOTI) → DeviceBridge (K8s Pods) → Databases (PostgreSQL, MongoDB) → Vault Mobile/Nurse Call/Splunk.
