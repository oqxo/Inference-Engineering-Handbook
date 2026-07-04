# 40. Kimi K2 Sizing Math

This chapter does the hardware math for running a Kimi K2-class model on premise.

The exact numbers must be validated with the exact model release and serving engine, but the sizing logic is the same.

## Source Notes

At the time of writing, the public model release used for these assumptions is `moonshotai/Kimi-K2-Instruct-0905`.

The model card describes it as a Mixture-of-Experts model with 1T total parameters, 32B activated parameters, and 256K context length. The deployment guide says the smallest deployment unit for Kimi K2 FP8 weights with 256K sequence length on mainstream H200 is a 16-GPU cluster. NVIDIA lists H200 with 141GB GPU memory and 4.8TB/s memory bandwidth.

If a future model named `Kimi K2.7` has different parameters, context length, precision, or deployment guidance, redo the math in this chapter.

## Model Planning Assumptions

For this chapter:

| Property | Value |
| --- | ---: |
| Total parameters | 1 trillion |
| Active parameters | 32 billion |
| Context length target | 256K tokens |
| Serving precision | FP8 |
| Target users | 100 developers |
| Peak active users | 20 |
| Heavy simultaneous generations | 5 to 10 |

## Step 1: Weight Memory

A parameter is a learned number.

At FP8, each parameter is approximately 1 byte.

```text
1 trillion parameters x 1 byte = 1,000,000,000,000 bytes
```

Convert to decimal gigabytes:

```text
1,000,000,000,000 bytes / 1,000,000,000 = 1,000 GB
```

Convert to GiB:

```text
1,000,000,000,000 bytes / 1,073,741,824 = about 931 GiB
```

So the raw FP8 weights are about:

```text
~1 TB decimal
~931 GiB binary
```

But raw weights are not the whole story. You also need:

- Quantization scales and metadata
- Runtime buffers
- KV cache
- Communication buffers
- Fragmentation headroom
- Serving engine overhead

Use a planning multiplier:

```text
Weight planning memory = raw weight memory x 1.10 to 1.20
```

So:

```text
1,000 GB x 1.15 = 1,150 GB planning weight footprint
```

## Step 2: Why FP16 Is Not Practical Here

At FP16 or BF16, each parameter is about 2 bytes.

```text
1 trillion parameters x 2 bytes = 2,000 GB
```

That is about 2 TB before runtime overhead and KV cache.

A 16 x H200 system has:

```text
16 x 141 GB = 2,256 GB raw GPU memory
```

FP16 weights alone would consume most of that. There would not be enough safe room for KV cache and runtime overhead.

Conclusion:

```text
For a 1T-parameter Kimi K2-class model, FP8 is the practical serving target.
```

## Step 3: Minimum GPU Class

For a serious 256K-context Kimi K2 deployment, plan around H200-class or newer high-memory data center GPUs.

Example:

```text
16 x NVIDIA H200 GPUs
141 GB each
Total raw GPU memory = 2,256 GB
```

Now reserve memory for overhead. If the serving stack safely uses 85 percent of raw memory:

```text
2,256 GB x 0.85 = 1,917.6 GB usable planning memory
```

Subtract estimated FP8 weight footprint:

```text
1,917.6 GB - 1,150 GB = 767.6 GB
```

That remaining memory is for KV cache, runtime buffers, and active requests.

This does not mean the system can freely allocate 767 GB only to user context. Serving engines have their own allocation strategies. But it gives a planning envelope.

## Step 4: KV Cache Planning

KV cache memory depends on model architecture, sequence length, number of layers, hidden size, cache format, and serving implementation.

For Kimi K2-class MoE models with optimized attention mechanisms, do not use a generic dense-transformer KV formula blindly. Instead:

1. Start with the vendor or model deployment guide.
2. Run the serving engine with fixed max context.
3. Measure available KV blocks.
4. Load test with real prompts.

Still, the planning rule is simple:

```text
Long context + high concurrency = more KV cache memory
```

If the bank wants 256K context for every developer at once, hardware requirements become much larger. In practice, most requests should be limited.

## Step 5: Practical Context Policy

For 100 developers, do not offer 256K context as the default.

Recommended limits:

| Tier | Max Context | Use |
| --- | ---: | --- |
| Default chat | 16K tokens | Normal Q&A, code help |
| Extended | 32K tokens | Larger files, design reviews |
| Heavy | 128K tokens | Incident logs, large docs |
| Admin-approved | 256K tokens | Rare deep analysis |

This protects the shared cluster from one user consuming too much cache.

## Step 6: Throughput Planning For 100 Developers

Assume:

- 100 developers total
- 20 active at peak
- 5 to 10 heavy generations at once
- Most requests are short or medium

One 16 x H200 Kimi serving unit may be enough for a controlled pilot, but it may not be enough for unrestricted usage by all developers if they use long context heavily.

A practical bank rollout:

```text
Pilot: 1 serving unit
Production baseline: 1 active serving unit + smaller models for routing
High availability: 2 serving units
Growth: add units after measuring real utilization
```

## Step 7: High Availability Math

If the bank needs service continuity during maintenance or GPU failure, one unit is not enough.

For Kimi K2:

```text
One serving unit = 16 x H200 GPUs
Two serving units = 32 x H200 GPUs
```

A bank may choose:

```text
Pilot: 16 GPUs, no full HA
Production: 32 GPUs, active/passive or active/active
```

Active/passive is easier but expensive because standby capacity may sit idle.

Active/active is more efficient but requires better routing and failure handling.

## Step 8: Do Not Use Kimi For Every Request

For cost and capacity, the bank should route tasks:

| Task | Suggested Model |
| --- | --- |
| Simple grammar rewrite | Small local model |
| Code comment explanation | Medium code model |
| Embeddings | Embedding model |
| Document retrieval | Embedding + search |
| Complex architecture reasoning | Kimi K2 |
| Long incident analysis | Kimi K2 with approval or quota |

This model routing can reduce Kimi usage dramatically.

## Minimum Starting Bill Of Materials

For a serious on-prem pilot:

| Component | Minimum Practical Starting Point |
| --- | --- |
| Kimi serving GPUs | 16 x H200-class GPUs |
| GPU nodes | Depends on chassis; commonly 2 x 8-GPU servers or equivalent |
| System RAM | At least 1-2 TB total across GPU servers for loading, staging, OS, and services |
| Local NVMe | Several TB per server for model files, cache, logs, and fast reload |
| Network | High-speed GPU node networking; 200-400Gbps class for multi-node serious serving |
| Storage | Internal artifact store for model weights and indexes |
| Gateway servers | CPU servers, redundant |
| Vector DB | CPU/RAM/NVMe sized by document corpus |
| Monitoring | Metrics, logs, traces, GPU telemetry |

For production with HA:

```text
Double the Kimi serving unit: 32 x H200-class GPUs.
```

## Key Ideas

- A 1T-parameter MoE still needs the full weights stored.
- FP8 weight memory is about 1 TB before overhead.
- FP16/BF16 serving is not practical for this size on a small cluster.
- 16 x H200-class GPUs is the right order of magnitude for one Kimi K2 256K serving unit.
- 32 x H200-class GPUs is the right order of magnitude for HA.
- Context limits are mandatory for shared developer usage.
