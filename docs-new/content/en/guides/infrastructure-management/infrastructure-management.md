---
title: "Infrastructure Management"
description: "Meshery provides the ability to manage infrastructure for agility, maintainability, diversity, reliability and isolation, security, and speed."
weight: 5
aliases:
  - /guides/infrastructure-management/overview
  - /tasks/application-management
  - /tasks/infrastructure-management
---

## Using Meshery Designs to Manage Your Infrastructure

Meshery is a versatile platform designed to streamline the lifecycle, configuration, and performance management of infrastructure across Kubernetes clusters.

### Designs in Meshery

Meshery employs the concept of [Designs](/concepts/logical/designs) as a fundamental construct for managing infrastructure. Designs provide a structured way to organize and deploy various components of your infrastructure. To do so, Meshery utilizes a declarative approach to infrastructure management, similar to Kubernetes manifests. Meshery Designs are written in YAML and are validated against a schema.

#### Importing Existing Infrastructure and Applications

Meshery facilitates the import of infrastructure in multiple formats, including Kubernetes manifests, Helm Charts, and Docker Compose files. Import existing infrastructure definitions by directly from filesystem, via URL, or import directly from a GitHub repository.

- Kubernetes Manifest
- Meshery Design
- Helm Charts
- Docker Compose

See [Importing Designs](/extensions/kanvas/import-export-designs) for more information.

{{% alert title="Note" type="info" %}}
Meshery is actively developing the ability to import custom models and components, expanding the platform's flexibility. Support for OCI registries is expected in the near future.
{{% /alert %}}