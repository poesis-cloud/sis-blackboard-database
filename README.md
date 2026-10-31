# SIS Blackboard Database (Helm Chart)

[![CI](https://github.com/poesis-cloud/sis-blackboard-database/actions/workflows/ci.yaml/badge.svg)](https://github.com/poesis-cloud/sis-blackboard-database/actions/workflows/ci.yaml)
[![Release](https://img.shields.io/github/v/release/poesis-cloud/sis-blackboard-database)](https://github.com/poesis-cloud/sis-blackboard-database/releases/latest)
[![Helm](https://img.shields.io/badge/Helm-chart-0F1689?logo=helm&logoColor=white)](ops/helm/Chart.yaml)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16-4169E1?logo=postgresql&logoColor=white)](ops/helm/Chart.yaml)
[![License: BUSL-1.1](https://img.shields.io/badge/license-BUSL--1.1-blue)](LICENSE)

This module packages the PostgreSQL backing store for the
**[SIS Blackboard Manager](../sis-blackboard-manager/)**
(DBM) as a Helm chart.

The Blackboard Database persists the DBM substrate model:
`Blackboard`, `Panel`, `ContributionSlot`, `Contribution`. The DBM is a
passive store of facts — vendor-posted contributions are validated
per-slot and frozen on seal; this database is what holds them durably,
including the byte-stable sealed contribution stream that vendor-side
reducers replay against. See the DBM data model in
[blackboard.puml](../sis-blackboard-manager/def/blackboard/blackboard.puml).

## What's in here

- `ops/helm/Chart.yaml`, `ops/helm/environments/*/values.yaml`: Helm
  chart metadata and per-environment configuration
- `ops/helm/templates/`: Kubernetes manifests
  (StatefulSet/Service/Secret/ConfigMap)
- (No `def/*.sql` schema yet — DBM-side schema bootstrap is a design-time
  TODO; the chart's `initdb` ConfigMap auto-mounts any `def/*.sql` once
  added.)

## How to use

- Configure values in `ops/helm/environments/<env>/values.yaml` and
  deploy with Helm in your target cluster (see `ops/README.md`).
- The chart is re-runnable and environment-configurable
  (credentials, storage, etc.) via values.

## Notes

This repo is in a design-oriented phase; this Helm chart is deployment
scaffolding for the DBM's persistence layer.
