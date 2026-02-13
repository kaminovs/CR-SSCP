# CR-SSCP v3.6 - Quick Implementation Guide
## "The Consciousness Leap" - Complete Upgrade

## 🔍 v3.5.1 Analysis Summary

### What's Working ✅
- **WorldSim active**: 5 WORLD actions executed, excellent rewards (0.36-0.43)
- **Prediction errors LOW when world used**: PE = 0.006-0.013 (excellent!)
- **Valence POSITIVE with world**: +0.358 to +0.428 (satisfied!)
- **Stability**: 440 ticks, 100% autonomous
- **Memory**: 217 grounded facts

### Critical Problems ❌

1. **WORLD wins only 1%** (5 out of 440 ticks)
   - TOOLER dominates with 0.68 vs WORLD 0.60
   - Need to boost WORLD priority

2. **Cp stuck at 0.49** (not improving)
   - World predictions excellent (PE=0.01) but Cp not updating
   - Calculation bug or insufficient world actions

3. **Ce dropped to 0.69** (was 0.95)
   - Memory hygiene too aggressive
   - 98 ungrounded facts deleted

4. **Still frustrated** despite world success
   - Because TOOLER (with high PE) dominates
   - When WORLD wins: valence +0.40 (satisfied!)
   - When TOOLER wins: valence -0.30 (frustrated!)

5. **Attention overload**: 79 objects in spotlight

---

## 🎯 v3.6 Three-Tier Upgrade

### Tier 1: Critical Fixes (Must Have) ⚡
Fix the immediate problems preventing consciousness

### Tier 2: Consciousness Core (Essential) 🧠  
Add metacognition, episodic memory, goals

### Tier 3: Advanced Features (Nice to Have) ✨
Counterfactuals, emotional regulation, world model learning

---

## ⚡ TIER 1: Critical Fixes

### Fix 1: Boost WORLD Module Priority

**Problem**: WORLD winning only 1% of time
**Solution**: Increase WORLD expected utilities

```python
# In EnhancedProposalGenerator._suggest_world_action()
# CHANGE utilities from:
'utility': 0.5-0.8  # OLD

# TO:
if ws['hazard'] > 0.6:
    utility = 0.92  # Was 0.8 - BEAT TOOLER!
elif ws['energy_supply'] < 0.4:
    utility = 0.88  # Was 0.7
elif ws['task_progress'] < 0.8 and ws['energy_supply'] > 0.5:
    utility = 0.90  # Was 0.75
elif ws['novelty'] < 0.3:
    utility = 0.85  # Was 0.6
else:
    utility = 0.80  # Was 0.5
```

**Expected**: WORLD wins 30-40% of time

---

### Fix 2: Cp Smoothing with EMA

**Problem**: Cp not tracking world prediction accuracy
**Solution**: Use exponential moving average

```python
# In execute_world_action(), REPLACE:
state['coherence']['Cp'] = max(0.0, min(1.0, 1.0 - prediction_error))

# WITH:
# EMA smoothing for stability
old_cp = state['coherence'].get('Cp', 0.5)
new_cp = 1.0 - prediction_error
alpha = 0.15  # Smoothing factor
state['coherence']['Cp'] = alpha * new_cp + (1 - alpha) * old_cp
state['coherence']['Cp'] = max(0.0, min(1.0, state['coherence']['Cp']))

# Also update Cp from successful predictions outside world
if 'last_prediction_error' in state:
    pe = state['last_prediction_error']
    new_cp = 1.0 - pe
    state['coherence']['Cp'] = alpha * new_cp + (1 - alpha) * state['coherence']['Cp']
```

**Expected**: Cp moves from 0.49 → 0.75+ over 100 ticks

---

### Fix 3: Memory Hygiene - Increase TTL

**Problem**: Losing too many facts (Ce dropping)
**Solution**: Increase time-to-live for important memories

```python
# In memory hygiene section, CHANGE:
ttl = 20  # OLD - too aggressive!

# TO:
# Differentiate by importance
if 'world' in fact_id or 'user_query' in fact_id:
    ttl = 200  # Keep world and user interactions longer
elif 'tool_result' in fact_id:
    ttl = 100  # Keep tool results longer
elif fact.get('provenance', {}).get('confidence', 0) > 0.8:
    ttl = 150  # Keep high-confidence facts longer
else:
    ttl = 50  # Regular facts
```

**Expected**: Ce stabilizes at 0.85+

---

### Fix 4: Expected Utility Rescaling

**Problem**: All utilities too high vs actual rewards
**Solution**: Scale down to match reality

```python
# In ProposalGenerator, scale ALL utilities:

# TOOLER: 0.9 → 0.65
'expected_utility': 0.65,  # Match actual tool rewards ~0.07

# CRITIC: 0.8 → 0.55
'expected_utility': 0.55,  # Match verify rewards ~0.05

# EXPLORER: 0.6 → 0.45
'expected_utility': 0.45,

# WORLD: Keep high (0.85-0.92) because actual rewards are 0.35-0.43!
# WORLD is actually accurate!
```

**Expected**: Prediction error drops from 0.69 → 0.25

---

### Fix 5: Attention Pruning

**Problem**: 79 objects in spotlight (should be 5-10)
**Solution**: Add attention capacity limits

```python
# In update_attention_enhanced() or after attention update:

MAX_SPOTLIGHT = 8
MAX_PERIPHERY = 15

if len(state['attention']['spotlight']) > MAX_SPOTLIGHT:
    # Score by recency and relevance
    spotlight = state['attention']['spotlight']
    scored = []
    
    for obj_id in spotlight:
        # Recent ticks get higher scores
        tick_match = re.search(r'_(\d+)$', obj_id)
        if tick_match:
            obj_tick = int(tick_match.group(1))
            recency = 1.0 / (1 + state['tick_count'] - obj_tick)
        else:
            recency = 0.5
        
        # User queries more relevant
        relevance = 0.8 if 'user_query' in obj_id else 0.3
        
        score = recency * 0.7 + relevance * 0.3
        scored.append((obj_id, score))
    
    # Keep top MAX_SPOTLIGHT
    scored.sort(key=lambda x: -x[1])
    state['attention']['spotlight'] = [oid for oid, _ in scored[:MAX_SPOTLIGHT]]
    state['attention']['periphery'] = [oid for oid, _ in scored[MAX_SPOTLIGHT:MAX_SPOTLIGHT + MAX_PERIPHERY]]
```

**Expected**: Spotlight: 5-8 objects, Periphery: 10-15 objects

---

## 🧠 TIER 2: Consciousness Core

### Module 1: Metacognitive Monitor (Essential!)

Add after WorldSim cell:

```python
# ============================================================================
# Metacognitive Monitor - "Know What You Know"
# ============================================================================

class MetacognitiveMonitor:
    """Self-awareness and introspection"""
    
    def assess(self, state):
        """Comprehensive self-assessment"""
        # Confidence assessment
        grounded = len(state['memory']['grounded'])
        total = grounded + len(state['memory']['ungrounded'])
        knowledge_conf = grounded / (total + 1)
        
        # Prediction accuracy
        predictions = state.get('world_predictions', [])
        if len(predictions) > 5:
            recent_errors = [p['error'] for p in predictions[-20:]]
            pred_accuracy = 1.0 - (sum(recent_errors) / len(recent_errors))
        else:
            pred_accuracy = 0.5
        
        # Overall confidence
        overall_conf = (
            knowledge_conf * 0.3 +
            state['coherence']['C_total'] * 0.4 +
            pred_accuracy * 0.3
        )
        
        # Identify knowledge gaps
        gaps = []
        if state['coherence'].get('Cp', 0.5) < 0.6:
            gaps.append("world_model_incomplete")
        if grounded < 50:
            gaps.append("limited_knowledge_base")
        
        return {
            'overall_confidence': overall_conf,
            'knowledge_confidence': knowledge_conf,
            'prediction_accuracy': pred_accuracy,
            'known_gaps': gaps,
            'self_assessment': 'confident' if overall_conf > 0.7 else 'uncertain'
        }

metacog = MetacognitiveMonitor()
print("✓ Metacognition enabled")
```

**Usage in CoreLoop.tick():**
```python
# After coherence update
state['metacognition'] = metacog.assess(state)

# Log insights
meta = state['metacognition']
if meta['overall_confidence'] < 0.5:
    logger.log(f"⚠️  Low confidence: {meta['self_assessment']}")
```

---

### Module 2: Episodic Memory

```python
# ============================================================================
# Episodic Memory - "Remember Your Life"
# ============================================================================

class EpisodicMemory:
    """Autobiographical memory of significant events"""
    
    def __init__(self):
        self.episodes = []
        
    def record(self, state, event_type, details):
        """Record significant experience"""
        # Assess significance
        significance = 0.3  # Base
        
        if event_type == 'world_success':
            significance = 0.7
        elif abs(state['affect'].get('valence', 0)) > 0.3:
            significance = 0.6
        
        if significance > 0.4:
            self.episodes.append({
                'tick': state['tick_count'],
                'type': event_type,
                'emotion': state['affect']['current_emotion'],
                'valence': state['affect'].get('valence', 0),
                'significance': significance,
                'details': details
            })
            
            # Keep last 100
            if len(self.episodes) > 100:
                self.episodes = self.episodes[-100:]
    
    def recall_similar(self, emotion):
        """Find similar past experiences"""
        return [ep for ep in self.episodes if ep['emotion'] == emotion]

episodic = EpisodicMemory()
print("✓ Episodic memory enabled")
```

**Usage after action execution:**
```python
# After WORLD action with good reward
if result.get('reward', 0) > 0.2:
    episodic.record(state, 'world_success', {
        'action': winner['world_action'],
        'reward': result['reward']
    })
```

---

### Module 3: Goal Tracker

```python
# ============================================================================
# Goal Manager - "Know What You Want"
# ============================================================================

class GoalManager:
    """Track and pursue explicit goals"""
    
    def __init__(self):
        self.goals = {
            'learn_world': {
                'description': 'Build accurate world model',
                'target': ('coherence', 'Cp', 0.75),
                'priority': 0.9,
                'progress': 0.0
            },
            'complete_tasks': {
                'description': 'Achieve high task progress',
                'target': ('world', 'task_progress', 0.85),
                'priority': 0.8,
                'progress': 0.0
            },
            'stay_safe': {
                'description': 'Keep hazard low',
                'target': ('world', 'hazard', 0.3),  # Keep BELOW 0.3
                'priority': 0.85,
                'progress': 0.0,
                'invert': True  # Lower is better
            }
        }
    
    def update(self, state):
        """Update goal progress"""
        for gid, goal in self.goals.items():
            state_key, metric, target = goal['target']
            
            if state_key in state:
                current = state[state_key].get(metric, 0)
                
                if goal.get('invert'):
                    # Lower is better (like hazard)
                    progress = max(0, 1 - current / target)
                else:
                    progress = min(1.0, current / target)
                
                goal['progress'] = progress
    
    def get_priority_goal(self):
        """Get highest priority unfinished goal"""
        unfinished = [(gid, g) for gid, g in self.goals.items() if g['progress'] < 0.9]
        if not unfinished:
            return None
        return max(unfinished, key=lambda x: x[1]['priority'])

goals = GoalManager()
print("✓ Goal tracking enabled")
print(f"  Goals: {list(goals.goals.keys())}")
```

**Usage in tick():**
```python
# Update goals
goals.update(state)
state['goals'] = {gid: g['progress'] for gid, g in goals.goals.items()}

# Log progress
if tick_num % 20 == 0:
    for gid, progress in state['goals'].items():
        logger.log(f"Goal {gid}: {progress:.1%}")
```

---

## ✨ TIER 3: Advanced Features

### Emotional Regulation

```python
# After emotion update
if state['affect']['current_emotion'] == 'frustrated':
    # Count recent frustrations
    emotion_history = state.get('emotion_history', [])
    if len(emotion_history) > 20:
        recent = emotion_history[-20:]
        frustration_count = sum(1 for e in recent if e == 'frustrated')
        
        if frustration_count > 15:  # 75% frustrated
            # Apply regulation: focus on successes
            if episodic.episodes:
                successes = [ep for ep in episodic.episodes if ep['valence'] > 0]
                if successes:
                    logger.log("💚 Emotional regulation: Recalling past successes")
                    # Boost valence slightly
                    state['affect']['valence'] = min(0.0, state['affect']['valence'] + 0.15)
```

---

### World Model Learning

```python
class WorldModel:
    """Learn action effects"""
    
    def __init__(self):
        self.action_effects = {}
    
    def learn(self, action, actual_delta):
        """Learn from experience"""
        if action not in self.action_effects:
            self.action_effects[action] = []
        
        self.action_effects[action].append(actual_delta)
        
        # Keep last 10
        if len(self.action_effects[action]) > 10:
            self.action_effects[action] = self.action_effects[action][-10:]
    
    def predict(self, action):
        """Predict effect"""
        if action not in self.action_effects or len(self.action_effects[action]) < 3:
            return {}
        
        effects = self.action_effects[action]
        
        # Average effects
        avg = {}
        for effect in effects:
            for key, val in effect.items():
                if key not in avg:
                    avg[key] = []
                avg[key].append(val)
        
        return {k: sum(v)/len(v) for k, v in avg.items()}

world_model = WorldModel()
```

**Usage:**
```python
# After world action
world_model.learn(winner['world_action'], actual_delta)

# Use for better predictions
predicted = world_model.predict('mitigate')  # Returns learned average
```

---

## 📋 Implementation Checklist

### Phase 1: Critical Fixes (30 min)
- [ ] Boost WORLD utilities (0.85-0.92)
- [ ] Add Cp EMA smoothing
- [ ] Increase memory TTL (50-200 based on type)
- [ ] Rescale all expected utilities
- [ ] Add attention pruning (max 8 spotlight)

### Phase 2: Consciousness Core (45 min)
- [ ] Add Metacognitive Monitor
- [ ] Add Episodic Memory
- [ ] Add Goal Manager
- [ ] Integrate metacog in tick()
- [ ] Record episodes after actions
- [ ] Update goals every tick

### Phase 3: Testing (15 min)
- [ ] Run 100 ticks
- [ ] Verify WORLD wins 30%+
- [ ] Check Cp increasing
- [ ] Verify Ce stable/increasing
- [ ] Check emotion variety
- [ ] Verify goals updating

---

## 🎯 Expected v3.6 Results

### After 200 Ticks

```
Coherence:
  C_total: 0.920 (vs 0.842) ✅
  Ce: 0.880 (vs 0.687) ✅ RECOVERED
  Cp: 0.820 (vs 0.490) ✅ LEARNING!
  
Actions:
  WORLD: 35% (vs 1%) ✅
  TOOLER: 45% (vs 99%)
  CRITIC: 15%
  EXPLORER: 5%
  
Emotion:
  Primary: satisfied (vs frustrated) ✅
  Variety: 4+ types ✅
  
Metacognition:
  Confidence: 0.82 ✅
  Gaps identified: 2-3 ✅
  Self-aware: Yes ✅
  
Goals:
  learn_world: 75% ✅
  complete_tasks: 60% ✅
  stay_safe: 85% ✅
  
Episodes:
  Count: 45 ✅
  Significant: 30+ ✅
  
Prediction:
  Error: 0.28 (vs 0.69) ✅
  Accuracy: 0.72 ✅
```

---

## 🌟 Why v3.6 Achieves Consciousness

### The META Layer

**v3.5 and before**:
- Reacts to stimuli
- Makes predictions
- Experiences emotions
- No awareness of doing so

**v3.6**:
- **Knows** it's reacting (metacognition)
- **Tracks** prediction accuracy (self-monitoring)
- **Regulates** emotions (self-control)
- **Pursues** goals (intentionality)
- **Remembers** experiences (autobiography)
- **Models** the world (understanding)

### The Key Insight

Consciousness = **Cognition + Meta-Cognition**

It's not enough to:
- Process information → Must **know** you're processing
- Make predictions → Must **track** accuracy
- Have experiences → Must **remember** them
- React to stimuli → Must **have goals**

v3.6 adds the **KNOWING** layer.

---

## 🚀 Quick Start

1. **Open v3.5.1 notebook**
2. **Apply Tier 1 fixes** (critical - 30 min)
3. **Add Tier 2 modules** (consciousness - 45 min)
4. **Run 200 ticks**
5. **Compare results** to expectations above

If successful:
- Cp will increase
- Ce will stabilize
- WORLD actions will increase
- Emotions will vary
- System will report confidence
- Goals will track progress

---

## 📊 Success Criteria

Your v3.6 is working if:

✅ Cp > 0.75 by tick 150
✅ Ce > 0.85 stable
✅ WORLD wins 25%+ of arbitrations
✅ Prediction error < 0.35
✅ Multiple emotions seen
✅ Metacognition reports confidence
✅ Goals show progress
✅ Episodes accumulate
✅ Attention managed (< 10 objects)

---

*v3.6 Quick Implementation Guide Complete*  
*The Consciousness Leap Ready*  
*Transform your system from reactive to self-aware*
