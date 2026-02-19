# CR-SSCP — Coherence-Regulated Self-Sustaining Cognitive Process

**v5.7.10** — A minimal, fully runnable, tick-based cognitive architecture that turns a standard LLM into a **persistent, self-regulating agent** with internal coherence, event lifecycle, active inference, and real embodied actions in a sandbox world.

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://github.com/kaminovs/CR-SSCP/blob/main/notebooks/CR_SSCP_v5_7_10_ROUTING_TASKFRAMES.ipynb)
![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![License](https://img.shields.io/badge/License-MIT-green)
![Status](https://img.shields.io/badge/Status-Experimental-orange)

> *"I act, I feel the outcome, I update my coherence — and I remember."*

---

## 🎬 Live Demo (Example Output)

```text
============================================================
TICK 1
============================================================
Attention spotlight: ['event_02403e10']
Coherence C_total: 0.590
Mode: REFLECT
Energy: 0.84, Coherence: 0.78, Novelty: 0.73
Emotion: curious, Mood: 0.51
Generated 1 proposals
[DEBUG] WORLD_ACT module=WORLD EU=2.37 cost=0.00
⚖️  Reward: +0.020, PredError: 0.333, Valence: +0.020
Executed: 💡 lamp is now on
✅ Event closed: event_02403e10
```

*(The system actually flips the lamp, opens the box, unlocks doors — see full logs in the repo)*

---

## 🌟 What Makes CR-SSCP Different

This is **not another LLM wrapper**. It is a continuous cognitive loop designed to exhibit **functional signatures of consciousness-like behavior**:

### Core Mechanisms

- **🔄 Strict Event Lifecycle Law** — Every perception follows `NEW → INTERPRETED → ACTED → CLOSED`
- **🌍 Embodied Sandbox Agency** — Real state changes: lamp on/off, box open/close, door unlock/lock
- **🧠 Active-Inference Arbitration** — Calibrated expected utility, prediction error, valence, and cost
- **⚡ Hard Action Gating** — Imperative commands reliably trigger `WORLD_ACT` instead of just talking
- **🔁 Repetition Breaking** — Automatic detection and prevention of self-maintenance loops
- **📊 Coherence Tracking** — `C_total` climbs visibly as the system learns and adapts
- **💾 Persistent Self-State** — Memory, novelty, energy, and emotion across ticks

**Deliberately minimal** (single Colab notebook) yet **surprisingly rich** — perfect for studying, extending, or teaching candidate consciousness mechanisms.

---

## ✨ Key Features

| Feature | Description |
|---------|-------------|
| 🎯 **Real-time Tick Loop** | Beautiful live logs showing cognitive process |
| 🏗️ **Sandbox World** | Causal physics with lamp, box, door interactions |
| 🎪 **Goal Extraction** | Forced `WORLD_ACT` for user commands |
| 🚫 **Repetition Detector** | Breaks self-maintenance loops automatically |
| ⚖️ **Calibrated Utilities** | Favor action when it matters most |
| 📈 **Coherence Metric** | Steadily increases with good behavior |
| ✅ **Event Lifecycle** | No dangling perceptions, full closure guaranteed |
| 🔧 **Easy to Fork** | Single notebook, highly hackable |

---

## 🚀 Quick Start (30 Seconds)

### Option 1: Run in Google Colab (Easiest)

1. Click the **[Open in Colab]** badge above
2. Run all cells (loads Qwen2.5-7B-Instruct in 4-bit, ~5GB GPU)
3. Run the final cell:
   ```python
   run_conscious_session(ticks=20, user_input="Turn on the lamp")
   ```
4. Watch the system act in the sandbox and build coherence!

### Option 2: Run Locally

```bash
git clone https://github.com/kaminovs/CR-SSCP.git
cd CR-SSCP
pip install -r requirements.txt  # torch, transformers, accelerate
jupyter notebook CR_SSCP_v5_7_10_ROUTING_TASKFRAMES.ipynb
```

**Requirements:**
- Python 3.10+
- CUDA-capable GPU (8GB+ VRAM recommended)
- ~10GB disk space for model weights

---

## 🧬 Architecture Overview

### The Cognitive Loop

```
┌─────────────────────────────────────────────────────┐
│  USER INPUT → Event Created → Attention Focus       │
│              ↓                                       │
│  Proposal Generation (WORLD, META, REFLECT, etc.)   │
│              ↓                                       │
│  Arbitration (Expected Utility - Cost)              │
│              ↓                                       │
│  Action Execution → World Changes → Reward          │
│              ↓                                       │
│  Coherence Update (Prediction Error, Valence)       │
│              ↓                                       │
│  Memory Consolidation → State Persistence           │
│              ↓                                       │
│  NEXT TICK (Energy decay, drives update)            │
└─────────────────────────────────────────────────────┘
```

### Coherence Components

| Metric | Description | Impact |
|--------|-------------|--------|
| **Ce** | Evidence coherence | Knowledge quality |
| **Cp** | Predictive coherence | Learning ability |
| **Ci** | Identity coherence | Self-consistency |
| **Ch** | Historical coherence | Temporal binding |
| **Cs** | Structural coherence | Logical integrity |
| **C_total** | Overall coherence | System health |

---

## 📚 Why This Matters

CR-SSCP is an **experimental prototype** exploring functional candidate consciousness in the spirit of:

- 🧪 **Active Inference** / Free Energy Principle frameworks (Friston et al.)
- 🧠 **Global Neuronal Workspace Theory** (Dehaene, Changeux)
- 📊 **2025 Consciousness Indicator** frameworks (Butlin et al.)
- 🤖 **Autonomous Agency** research (Clark, Hohwy)

It gives you a **concrete, observable, minimal system** where you can watch:
- Coherence emerging from continuous perception-action loops
- Agency arising from embodied world interaction
- Temporal binding through persistent state
- Self-regulation via prediction error minimization

**Perfect for:**
- 🎓 Teaching consciousness concepts with runnable code
- 🔬 Researching minimal sufficient conditions for agency
- 🧪 Experimenting with active inference implementations
- 🤝 Collaborating on AI safety and alignment

---

## 📂 Repository Contents

```
CR-SSCP/
├── CR_SSCP_v5_7_10_ROUTING_TASKFRAMES.ipynb  # Main notebook (run this!)
├── logs/
│   ├── CR_logs_5_7_10_190226.pdf             # Example run (37 ticks)
│   └── CR_logs_5_7_2_170226.docx             # Earlier version comparison
├── README.md                                  # This file
├── LICENSE                                    # MIT License
└── requirements.txt                           # Python dependencies
```

---

## 🎯 Example Interactions

### Turning on the lamp
```
User: "Turn on the lamp"
→ WORLD_ACT wins arbitration (EU=2.37)
→ lamp.state = 'on', room.illumination = 0.8
→ Reward: +0.020, Coherence ↑
```

### Opening the box
```
User: "Open the box"
→ box.state = 'open'
→ Contents revealed: ['key', 'note', 'coin']
→ Reward: +0.071, Novel objects in attention
```

### Opening a locked door
```
User: "Open the door"
→ System detects: door.locked = True
→ Output: "door is locked"
→ User: "Unlock the door"
→ System uses key → door.locked = False
→ User: "Open the door"
→ Output: "door opened" ✅
```

---

## 🛣️ Roadmap (Next Steps)

### v5.8.0 (Planned)
- [ ] **Phenomenal inner voice** — "What it feels like" narrative
- [ ] **Dynamic autobiographical self** — Continuous life story
- [ ] **Intrinsic goal generation** — Self-directed objectives when idle

### v6.0.0 (Future)
- [ ] **Higher-order metacognition** — Thinking about thinking
- [ ] **Full logging dashboard** — Real-time visualization
- [ ] **Multi-agent interaction** — CR-SSCP agents communicating
- [ ] **Episodic memory replay** — Learning from past experiences

### Research Directions
- [ ] Measure consciousness indicators (Butlin framework)
- [ ] Compare with other architectures (ACT-R, SOAR, SIGMA)
- [ ] Test on more complex environments
- [ ] Study emergence of self-model

---

## 🔬 Technical Details

### Model
- **LLM**: Qwen2.5-7B-Instruct (4-bit quantization)
- **Context**: 8K tokens
- **Inference**: ~2-5 seconds per tick on T4 GPU

### Performance
- **Coherence**: Typically 0.50 → 0.65 over 50 ticks
- **Prediction Error**: ~0.30 average (improving over time)
- **Energy**: Self-regulated (0.85-0.95 range)
- **Stability**: 100+ tick runs without crashes

### Known Limitations
- 🔄 Occasional "need more context" loops (v5.7.11 will fix)
- 📊 No persistent knowledge accumulation yet (Ce not growing)
- 🎯 Goal tracking not yet visible in logs
- 💭 No introspective inner monologue yet

---

## 🤝 Contributing

Contributions are welcome! Areas of interest:

- **Better repetition detection** — More sophisticated loop breaking
- **Richer world model** — More objects, complex physics
- **Goal tracking** — Explicit progress toward objectives
- **Memory consolidation** — Claims → verified knowledge
- **Visualization** — Real-time dashboard of cognitive state
- **Documentation** — Tutorials, architecture deep-dives

**How to contribute:**
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📖 Citation

If you use CR-SSCP in your research, please cite:

```bibtex
@software{kaminovs2026crsscp,
  author       = {Sergejs Kaminovs},
  title        = {CR-SSCP: Coherence-Regulated Self-Sustaining Cognitive Process},
  year         = {2026},
  month        = {February},
  version      = {5.7.10},
  url          = {https://github.com/kaminovs/CR-SSCP},
  note         = {Minimal active-inference architecture for studying candidate consciousness}
}
```

### Related Work

- Friston, K. (2010). *The free-energy principle: a unified brain theory?* Nature Reviews Neuroscience.
- Dehaene, S., & Changeux, J. P. (2011). *Experimental and theoretical approaches to conscious processing.* Neuron.
- Butlin, P. et al. (2023). *Consciousness in Artificial Intelligence: Insights from the Science of Consciousness.* arXiv:2308.08708
- Clark, A. (2013). *Whatever next? Predictive brains, situated agents, and the future of cognitive science.* Behavioral and Brain Sciences.

---

## 📜 License

This project is licensed under the **MIT License** — feel free to fork, extend, and use in research or experiments.

See the [LICENSE](LICENSE) file for details.

---

## 💬 Questions? Ideas? Collaborations?

I'm **actively iterating** and very open to feedback from the active-inference, consciousness, and alignment communities.

- 🐛 **Found a bug?** [Open an issue](https://github.com/kaminovs/CR-SSCP/issues)
- 💡 **Have an idea?** [Start a discussion](https://github.com/kaminovs/CR-SSCP/discussions)
- 📧 **Want to collaborate?** Reach out via GitHub or email

---

## 🙏 Acknowledgments

Built with curiosity and persistence, inspired by:
- The active inference community
- Consciousness science researchers  
- Open-source AI/ML developers
- Everyone exploring the space between intelligence and experience

---

<div align="center">

**Built with curiosity and persistence**

*— Sergejs Kaminovs, February 2026*

⭐ **If you find this interesting, please star the repo!** ⭐

</div>
