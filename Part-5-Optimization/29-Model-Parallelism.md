# 29. Model Parallelism

Model parallelism means splitting a model across multiple devices.

This is useful when a model is too large for one GPU or when one GPU cannot meet performance targets.

## Tensor Parallelism

Tensor parallelism splits parts of model computations across GPUs. Each GPU handles a slice of the work, then results are combined.

This can improve capacity, but it requires communication between GPUs.

## Pipeline Parallelism

Pipeline parallelism places different model layers on different GPUs. Data flows through the GPUs like stages in a pipeline.

This can help fit large models, but it may introduce scheduling complexity and idle time.

## Tradeoffs

Splitting a model is not always faster. Communication can reduce gains. Debugging also becomes harder.

Use model parallelism when the model cannot fit on one GPU or when benchmarked performance proves it helps.

## Key Ideas

- Model parallelism splits a model across devices.
- Tensor parallelism splits computations.
- Pipeline parallelism splits layers.
- Communication cost is the main tradeoff.

## Developer Checklist

- Try a single-GPU setup first if it meets requirements.
- Use high-speed interconnects when splitting models.
- Measure latency and throughput at realistic concurrency.
- Keep deployment configuration reproducible.

