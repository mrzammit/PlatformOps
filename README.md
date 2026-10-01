# PlatformOps Dashboard

A personal C#/.NET project exploring how to monitor and manage independent SaaS production environments from a central control panel. Built incrementally using test-driven development (TDD).

## First milestone: tenant routing audit

A tenant can belong to one environment while its hostname routes to another. For example, a tenant hosted in Azure might use a hostname that resolves to an on-premises environment through a wildcard DNS record.

The first milestone is to compare a tenant's expected environment with its observed routing destination and report mismatches.

Development will use fictional tenants, simulated environments, and a simulated DNS provider. No production infrastructure or credentials are required.

## Current status

Initial solution setup and the first routing audit test. The auditor implementation does not exist yet, so the initial test is expected to fail to compile. There is no runnable dashboard at this stage.

## Project structure

- `src/PlatformOps.Core`: operational rules and domain models.
- `tests/PlatformOps.Core.Tests`: xUnit tests for those rules.

## Getting started

Install the .NET SDK matching the target framework in the project files. Visual Studio 2026 is the primary development environment; the .NET CLI can also be used.

Open the solution in Visual Studio and run tests through Test Explorer, or run these commands from the repository root:

```shell
dotnet restore
dotnet test
```

Until the first implementation is added, compilation errors referencing `TenantRoutingAuditor` are expected.

## Planned architecture

- An ASP.NET Core application serving the dashboard and API.
- A background worker collecting observations and running audits.
- Integration adapters for environment APIs, DNS, and other operational tools.
- A database storing configuration, observations, and audit history.
- Optional environment connectors where direct network access is unavailable.

The dashboard is intended to operate outside the customer request path. Customer traffic will continue to use the existing environment infrastructure.

## Roadmap

- [ ] Implement the tenant routing audit rule using TDD.
- [ ] Model environments, tenants, and hostnames.
- [ ] Add simulated environment and DNS integrations.
- [ ] Expose audit results through an HTTP API.
- [ ] Build a dashboard showing routing mismatches and environment health.
- [ ] Store check history and add automated test execution in GitHub Actions.

## Development approach

Each behavior starts with a failing test, followed by the smallest implementation that passes it and a refactoring step. Unit tests will cover operational rules; integration tests will cover HTTP endpoints and service interactions as those features are introduced.

Examples and configuration will use fictional data. Real tenant information, internal URLs, and secrets must stay outside this repository.
