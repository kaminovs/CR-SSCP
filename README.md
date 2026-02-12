# CR-SSCP

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
- `logs/` — example logs from runs (optional)
- `src/` — extracted python modules (future refactor)
- `README.md` — this file

## License
MIT
