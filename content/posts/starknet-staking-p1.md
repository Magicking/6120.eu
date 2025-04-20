+++
title = "StarkNet Phase 1 - Freebox Validator"
date = "2025-03-31T19:00:03+01:00"
tags = ["starknet", "cairo"]
description = "My experience running a StarkNet validator on a Freebox router during Phase 1, including challenges and learnings"
showFullContent = false
readingTime = true
hideComments = false
color = "" #color from the theme settings
+++

## Introduction

This post is the beginning of a series of blog posts on hosting Starknet nodes. I always enjoy the challenges of hosting high-availability infrastructures and blockchain nodes always have their own set of problematics: large underlying databases, reactivity, syncing & signing speed... May this series help the path towards decentralization of Starknet. It begins with the cheapest system I could put my hands on.

# Phase 1

[StarkNet staking 1st phase](https://www.starknet.io/blog/staking-phase-1/) consist of solely running a full RPC node, at the time of writing, staking ask for 20_000 Strk tokens (~3700$). As there is no validator duties linking performance and reward it's an ideal moment to start scaling from the bottom.

As a minimum viable product I choose a Virtual Machine (VM) running on my Internet Service Provider(ISP) router Freebox, because it's a system that cost me almost nothing, always running and can host VMs.

## Hardware Setup

The Freebox Delta router, while primarily designed for home networking, surprisingly packs enough punch for our needs. Under the hood, it features a Quad-Core Armv8 Cortex A-72 processor and 2GB of RAM, which while modest, proved sufficient for our initial testing phase. The storage setup: two Crucial BX500 SATA SSDs in a 1TB RAID1 configuration.

## Initial Setup and Challenges

Getting the StarkNet full node up and running on the Freebox was an exercise in resource optimization. The initial state synchronization proved to be the first major hurdle using a combination of snapshot and desktop computer, with the limited CPU & RAM. The process took several days to complete, with the node frequently hitting memory limits during peak synchronization periods. Network bandwidth, while not a primary concern give the Freebox's gigabit connection a low latency, and careful monitoring to ensure it didn't impact household internet usage.

## Validator Implementation

The validator setup was surprisingly straightforward once the full node was operational as there was no implementation existing (Note, there are now 2 implementations existing). Monitoring was handled through a combination of Prometheus and Grafana, giving us real-time insights into the node's performance and health.

## Performance Analysis

During normal operation, the Freebox validator handled block processing adequately, maintaining sync with the network without issues. However, the limitations became apparent during high transaction volume periods. The quad-core ARM processor, while efficient, struggled to keep up with the computational demands of processing large blocks during network congestion. This was particularly evident during High TPS events, where transaction throughput would spike dramatically.

![](/img/posts/starknet-p1/rpc-grafana-head.png)

## Lessons Learned

The Freebox experiment taught us several valuable lessons about validator requirements. While the setup worked for Phase 1's basic requirements, it highlighted the importance of having headroom for processing power during network stress. The RAID1 storage setup proved fine, but the 2GB RAM limitation was a constant challenge. For future phases, we'll need to consider more powerful hardware for full node, and separate signers particularly as validator duties become active.

## Next Steps

Moving forward, we're considering several options to improve our setup. A dedicated mini-PC with more RAM and a more powerful processor would be the logical next step, while still maintaining the cost-effectiveness that made the Freebox experiment appealing. We're also exploring ways to optimize the node software to better handle high-throughput periods.

## Conclusion

The Freebox validator experiment was a valuable learning experience in Phase 1 of StarkNet's staking journey. While the hardware limitations prevented optimal performance during high-stress periods, it successfully demonstrated that running a validator doesn't require expensive enterprise-grade equipment. The experience has given us valuable insights into the minimum requirements for future phases and helped us identify areas for improvement in our setup.

# Artifacts

- A [Grafana JSON Dashboard](https://gist.github.com/Magicking/73cc2802da9cd6c76905dac670b72cac) to monitor your Pathfinder instances.

![](/img/posts/starknet-p1/pathfinder-metrics.png)