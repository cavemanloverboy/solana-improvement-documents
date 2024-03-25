---
simd: '0130'
title: Dynamic Block Limits
authors:
  - Cavey Cool, Magnetar Fields
category: Standard
type: Core
status: Draft
created: 2024-03-24
feature: (fill in with feature tracking issues once accepted)
supersedes: (optional - fill this in if the SIMD supersedes a previous SIMD)
extends: (optional - fill this in if the SIMD extends the design of a previous
 SIMD)
---

## Summary

This proposal introduces dynamic adjustments to the compute unit (CU) limit of
Solana blocks based on network utilization at the end of each epoch. If the
average block utilization exceeds 75%, the CU limit will increase by 20%;
if it falls below 25%, the limit will decrease by 20%. This mechanism aims to
optimize network performance by adapting to actual demand without centralized
or arbitrary adjustments.

## Motivation

The goal of this proposal is to enhance the scalability and efficiency of the
Solana network by dynamically adjusting block CU limits in response to actual
network demand, ensuring Solana scale's with Moore's Law and exponentially
increasing bandwidth.

## Alternatives Considered

**Manual Adjustment**: Periodic manual reviews of network performance to adjust
CU limits. This lacks responsiveness, flexibility, and may be an arbitrary or
centralized decision.

## New Terminology

- **Dynamic Block Limit**: Adjusting block CU limits based on network demand.
- **Epoch Average Utilization**: The average CU utilization over an epoch.
- **CU Limit Adjustment**: The process of modifying the block's CU limit.

## Detailed Design

### Implementation

Record each block's CU utilization to calculate the average for the epoch.
Increase CU limit by 20% if average utilization >75%, decrease by 20% if <25%.

**Safety Measures**: Implement maximum and minimum CU limits to prevent extreme adjustments.

### Interaction and Integration

- Fits into the Solana runtime as a dynamic parameter adjustment mechanism.
(Perhaps in the future, other constant parameters can be made dynamic using a
similar mechanism.)
- Will require updates to how block capacity is calculated and adjusted at the
epoch level.

## Impact

**Validators**: Will benefit from more consistent network performance and
potentially higher throughput during peak times. Revenue capacity will increase
naturally with better hardware, incentivizing validators to upgrade collectively.

**Core Contributors**: Need to consider implications on network stability and
performance monitoring.

## Security Considerations

Implementing dynamic block limits must not introduce vectors for DoS attacks or
manipulation of block capacity. Thorough testing, simulations, and historical
analyses are required to ensure the mechanism's resilience against such threats.

## Drawbacks

**Pros**:

- Offers real-time adjustment according to demonstrated network capacity.
- Directly targets network demand and capacity issues.

**Cons**:

- It may take several epochs to adjust to a large step function increase in demand.
- Introducing dynamic block limits adds complexity to the network's operation/monitoring.

## Backwards Compatibility

- The proposal requires network-wide coordination for activation.