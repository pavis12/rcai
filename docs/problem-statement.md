# RCAI — Problem Statement

## Problem

Production incidents rarely come from a single obvious signal.

When a service starts failing, engineers may need to inspect logs, metrics, deployments, dependencies, message-processing systems, and historical information separately. This makes incident investigation time-consuming, especially when multiple services are involved.

RCAI is designed to bring these signals together into a single investigation workflow.

## Goal

The goal of RCAI is to build a backend system that can:

1. Collect production-like telemetry from simulated services.
2. Detect abnormal service behavior using deterministic rules.
3. Correlate related logs, metrics, deployments, and dependencies.
4. Create and track production incidents.
5. Provide APIs for engineers to inspect incident evidence.
6. Use a controlled AI investigation layer to analyze available evidence.
7. Produce root-cause hypotheses with supporting evidence and clearly communicate uncertainty.

## Key Principle

RCAI does not treat AI as the incident detection mechanism.

The deterministic backend should be able to detect and investigate the basic incident context without an LLM.

AI is used as an additional investigation layer that can retrieve approved evidence through controlled tools and reason over that evidence.

## Expected Outcome

For a simulated production failure, an engineer should be able to:

```text
Trigger failure
      ↓
Telemetry generated
      ↓
Kafka receives events
      ↓
Events processed
      ↓
Evidence stored
      ↓
Incident detected
      ↓
Signals correlated
      ↓
Engineer requests investigation
      ↓
AI retrieves approved evidence
      ↓
Evidence-grounded investigation
```

The final system should make it possible to understand **what happened, what evidence supports the investigation, what the likely contributing factors are, and what still needs to be verified.**
