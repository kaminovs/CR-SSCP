# CR-SSCP — Coherence-Regulated Self-Sustaining Cognitive Process

CR-SSCP is a research prototype of a persistent, self-regulating AI/LLM process built around **coherence**, **attention**, **memory**, and **action selection**.  
It turns a reactive “single prompt → single answer” model into a **continuous cognitive loop** with internal drives, temporal binding, and active inference in a sandboxed environment.

> Status: experimental / research prototype (rapid iteration).

## What’s inside
- **Core loop** (tick-based) with internal state + logging
- **Simulated user-like inputs** injected periodically (or manual input)
- **Proposal generation** with forced variety (PLANNER / CRITIC / EXPLORER / NARRATIVE / META)
- **Dummy tools** (safe math, time, self-reflection) to test tool-use wiring
- **Session logs** + simple analysis outputs

## Quick start (Google Colab)
1. Open the notebook in Colab
2. Run all cells
3. Review the logs/summary cells at the end

## Notes on GitHub rendering
Some notebook widget metadata may break GitHub rendering.  
If you see “Invalid Notebook”, remove `metadata.widgets` from the `.ipynb` JSON before committing.

## Repository layout (recommended)
- `notebooks/` — main Colab notebooks
- `logs/` — example logs from runs 
- `docs/` — results 
- `README.md` — this file


**v5.7.10** — A minimal, fully runnable, tick-based cognitive architecture that turns a standard LLM into a **persistent, self-regulating agent** with internal coherence, event lifecycle, active inference, and real embodied actions in a sandbox world.

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/kaminovs/CR-SSCP/notebooks/CR_SSCP_v5_7_10_ROUTING_TASKFRAMES.ipynb)
![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![License](https://img.shields.io/badge/License-MIT-green)

> "I act, I feel the outcome, I update my coherence — and I remember."



## Citations

If you use or reference this work, please cite:

@software{kaminovs2026crsscp,
  author       = {Sergejs Kaminovs},
  title        = {CR-SSCP: Coherence-Regulated Self-Sustaining Cognitive Process},
  year         = 2026,
  url          = {https://github.com/kaminovs/CR-SSCP},
  note         = {Research prototype for persistent coherence-regulated AI systems}
}

### Live Demo (example output)

```text
TICK 1
Attention spotlight: ['event_02403e10']
Coherence C_total: 0.590
Mode: REFLECT
Energy: 0.84, Coherence: 0.78, Novelty: 0.73
Executed:   lamp is now on
Event closed: event_02403e10
[PHENOMENAL EXPERIENCE] I feel warm satisfaction as I turn on the lamp under my control.
