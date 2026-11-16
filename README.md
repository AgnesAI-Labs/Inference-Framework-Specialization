# Inference Framework Specialization

## Methodology and Interim Results

English edition, revision v2 (November 13, 2026). This repository publishes the supplied 32-page technical report on an evolving in-house inference framework built on SGLang, plus an illustrated reading guide.

## Read

- [Original technical report (PDF)](PAPER.pdf) - the canonical source for the complete methods, component studies, charts, and limitations.
- [Illustrated reading guide](REPORT.md) - a structured overview with selected original figures; it is **not a full-text transcription**.

## Current phase at a glance

The evaluated deployment combines Blackwell GPUs, a PCIe-only multi-GPU interconnect, constrained GPU memory, a deep hybrid-attention model, and long-context workloads. The report discusses six techniques: FP4 attention for prefill, GPU L2 weight prefetching, operator shape/dispatch adaptation, cross-microbatch overlap (MBO), NVFP4 KV cache, and BOLE recurrent-state optimization.

The *confirmed integrated configuration* uses BOLE, NVFP4 KV cache, FP4 prefill, and GPU L2 decode prefetching. The paper reports **+74.8% GPU KV capacity** (530,400 to 927,000 tokens), **3.54x 512K cold-prefill speedup**, and peak output-throughput gains of **+61.3% single-turn** and **+52.7% multi-turn** at the tested client concurrency levels.

## Evidence boundary

These are interim measurements for **one** hardware, model, and workload combination; component gains are not additive or automatically transferable. The integrated comparison also changes the active-request limit from 8 to 16, so compute, capacity, caching, and queueing contribute together. **Independent quality acceptance for the integrated configuration remains outstanding.** The paper records short-input regressions and quality or non-inferiority failures in some component studies. See the PDF before reusing any performance claim.
