# Infrastructure Testing Suite (Terratest + Go)

This project implements an infrastructure testing framework using Go and Terratest to validate Terraform-based Kubernetes resources. It ensures that infrastructure changes are tested automatically before being applied to production environments.

## Overview

Modern infrastructure workflows require validation to prevent configuration drift, deployment failures, and runtime issues. This project demonstrates how infrastructure can be tested programmatically using Go, following a create–verify–destroy lifecycle.

The testing suite provisions Kubernetes resources using Terraform, validates them through the Kubernetes API, and then safely cleans up the environment.

## Why This Project Matters

Infrastructure failures often originate from untested changes.  
This project demonstrates how infrastructure can be validated before deployment, reducing production risk and improving system reliability.

It reflects real-world SRE practices where infrastructure is treated as testable, versioned code.

## Key Features

- Infrastructure provisioning using Terraform
- Automated validation using Go and Terratest
- Kubernetes resource verification using client-go
- End-to-end lifecycle testing (provision → validate → destroy)
- Idempotent and repeatable test execution

## Architecture Flow

Terraform → Provisions Kubernetes namespace  
↓  
Terratest (Go) → Executes infrastructure lifecycle  
↓  
Kubernetes API → Validates resource existence  
↓  
Terraform → Cleans up resources

## Project Structure


infra-testing-suite-terratest/
├── terraform/
│ ├── main.tf
│ └── provider.tf
├── tests/
│ └── k8s_test.go
├── go.mod
└── README.md


## How It Works

The test follows a structured workflow:

1. Terraform initializes and provisions infrastructure
2. A Kubernetes namespace is created
3. Go test connects to the Kubernetes cluster
4. The namespace is verified using the Kubernetes API
5. Terraform destroys all created resources

This approach ensures that infrastructure changes are validated in a controlled and automated manner.

## Prerequisites

- Go (1.20+ recommended)
- Terraform
- Kubernetes cluster (Minikube, Kind, or cloud cluster)
- kubectl configured with access to the cluster


## Installation

Clone the repository:

git clone https://github.com/Aishhh-27/infra-testing-suite-terratest.git

cd infra-testing-suite-terratest


Initialize Go modules:
go mod tidy


**Running Tests**

Execute the test suite:
go test ./tests -v

**Example Output**


=== RUN   TestTerraformAndK8s
--- PASS: TestTerraformAndK8s
PASS

**Technologies Used**

Go

Terratest

Terraform

Kubernetes (client-go)

**Use Cases**

Validating infrastructure changes before deployment
Testing Terraform modules in CI/CD pipelines
Preventing configuration drift in Kubernetes environments
Building reliable infrastructure automation workflows

**Notes**

The test uses a local kubeconfig file for cluster access
Ensure your Kubernetes cluster is running before executing tests
Terraform state is managed locally for simplicity
Future Improvements
Integration with CI/CD pipelines (GitHub Actions or GitLab CI)
Support for multiple environments (dev, staging, production)
Additional validation for deployments and services
Parameterized tests for reusable infrastructure modules

**Author**

Aishwarya Ganesh
