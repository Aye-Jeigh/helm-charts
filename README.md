# KEDA ScaledJobs on AKS with Azure DevOps Helm Chart

## Overview

This repository contains a Helm chart for deploying KEDA ScaledJobs on Azure Kubernetes Service (AKS) with integration to Azure DevOps for ephemeral agents. The chart is designed to streamline the deployment process, ensuring scalability and ease of maintenance.

## Features

- **KEDA ScaledJobs**: Automates scaling based on Azure DevOps pipeline jobs.
- **Ephemeral Agents**: Creates and manages ephemeral agents for Azure DevOps.
- **Seamless Integration**: Easily integrates with Azure DevOps, Argo CD, and Kubernetes.
- **Modularity**: Includes KEDA as an optional subchart for easier management.
- **Advanced Configuration**: Supports custom tolerations, affinities, and resource limits.

## Prerequisites

- Kubernetes cluster (preferably AKS)
- Helm 3.x
- Azure DevOps account
- KEDA installed (if not using the subchart)

## Installation

### Step 1: Install KEDA if it isn't already

```sh
helm repo add kedacore https://kedacore.github.io/charts
```
```sh
helm install keda kedacore/keda --namespace keda --create-namespace
```

### Step 2: Add helm ado-scaledjob-agents helm repo

```sh
helm repo add ado-scaledjob-agents https://aye-jeigh.github.io/helm-charts
```

### Step 3: Customize values.yaml
Edit the `values.yaml` file to customize the settings for your environment.
The following changes are mandatory for the project to work correctly.

```sh
helm show values ado-scaledjob-agents/ado-scaledjob-agents > values.yaml
```
```
common:
  adoUrl: https://dev.azure.com/your-org
  adoPoolName: dev-agents
```
```
triggers:
  poolID: "09"
```

### Step 4: Install the Helm Chart
```sh
helm install dev-agents ado-scaledjob-agents/ado-scaledjob-agents -f values.yaml
```

## Usage

### Customizing the Chart
Refer to the values.yaml file to adjust configurations like resource limits, tolerations, and environment variables.

### Enabling/Disabling Features

Toggle the enabled field in values.yaml to enable or disable specific configurations like scaledjob-large and placeholderjob-large.

