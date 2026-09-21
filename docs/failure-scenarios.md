# RCAI — Failure Scenarios

This document defines the initial production failure scenarios that RCAI will simulate, detect, correlate, and investigate.

## Scenario 1 — Database Latency → Payment Failures

### Situation

The payment service depends on a database. The database begins responding slowly.

### Expected behavior

1. Database latency increases.
2. Payment service response latency increases.
3. Payment error rate increases.
4. RCAI detects abnormal behavior.
5. RCAI correlates database and payment signals.
6. The investigation identifies database latency as a possible root cause.

### Evidence

* Database latency metrics
* Payment service latency
* Payment error rate
* Application logs
* Service dependency information
* Recent deployment information

---

## Scenario 2 — Kafka Consumer Lag → Delayed Order Processing

### Situation

The order-processing consumer becomes slow or unavailable.

### Expected behavior

1. Orders continue to enter the Kafka topic.
2. The consumer processes messages slowly.
3. Kafka consumer lag increases.
4. Order processing becomes delayed.
5. RCAI detects the abnormal lag.
6. RCAI correlates consumer and order-processing signals.
7. The investigation identifies the consumer/Kafka processing path as a possible cause.

### Evidence

* Kafka consumer lag
* Message processing rate
* Order processing metrics
* Consumer logs
* Consumer health status
* Related service activity

---

## Scenario 3 — Deployment → Sudden Error Spike

### Situation

A new version of a service is deployed and errors increase shortly afterward.

### Expected behavior

1. A new service version is deployed.
2. The deployment event is recorded.
3. Error rate increases after the deployment.
4. RCAI detects the abnormal error rate.
5. RCAI correlates the incident with the deployment timeline.
6. The investigation identifies the deployment as a possible contributing factor.

### Evidence

* Deployment events
* Error rate metrics
* Application logs
* Service health metrics
* Incident timeline
* Previous version information

---

## Investigation Principle

RCAI must distinguish between **evidence** and **hypotheses**.

The system should not automatically claim that a signal is the root cause simply because it occurred before an incident.

For example:

> **Evidence:** Database latency increased at 14:30 and payment errors increased at 14:31.

> **Hypothesis:** Increased database latency may have contributed to the payment failures.

The AI investigation should communicate uncertainty when the available evidence is insufficient.
