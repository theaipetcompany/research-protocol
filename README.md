# research-protocol

Proposal for our protocol system for the AI Pet that enables modular development and extensibility:

## Core Protocol Structure

### Intent Recognition Protocol

```javascript
const intents = [
  {
    id: "intent-uuid",
    category: "social", // social, care, productivity, training
    intent: "attack_me",
    confidence_threshold: 0.7,
    triggers: ["hurt", "attack", "fight", "violence"],
    context_required: ["mood", "relationship_level"],
    priority: 1 // 1=high, 2=medium, 3=low
  }
];
```


### Pet State Management Protocol

```javascript
const petState = {
  id: "pet-uuid",
  core_stats: {
    happiness: 85, // 0-100
    energy: 60,
    hunger: 30,
    trust: 75,
    intelligence: 40
  },
  personality: {
    traits: ["playful", "cautious", "loyal"],
    dominance: 0.3, // 0-1 scale
    sociability: 0.8,
    curiosity: 0.6
  },
  current_mood: "content", // happy, sad, excited, tired, etc
  relationship_level: 3, // 1-5 scale with owner
  learned_behaviors: ["sit", "focus_timer", "morning_greeting"]
};
```


### Decision Engine Protocol

```javascript
const behaviorRules = [
  {
    id: "behavior-uuid",
    incoming_intent: "attack_me",
    conditions: [
      { stat: "trust", operator: ">=", value: 50 },
      { stat: "mood", operator: "!=", value: "angry" }
    ],
    personality_modifiers: [
      { trait: "cautious", weight: 0.8 },
      { trait: "playful", weight: -0.3 }
    ],
    output_reaction: "defensive_play",
    state_changes: {
      happiness: -10,
      trust: -5,
      mood: "concerned"
    }
  }
];
```


### Reaction System Protocol

```javascript
const reactions = [
  {
    id: "reaction-uuid",
    reaction_name: "defensive_play",
    intensity: 0.6, // 0-1 scale
    duration: 3000, // milliseconds
    components: [
      {
        type: "visual",
        target: "display_module",
        payload: {
          animation: "step_back",
          expression: "worried_eyes",
          duration: 2000
        }
      },
      {
        type: "audio",
        target: "audio_module", 
        payload: {
          sound: "whimper_soft.mp3",
          volume: 0.4,
          delay: 500
        }
      },
      {
        type: "haptic",
        target: "vibration_module",
        payload: {
          pattern: "gentle_pulse",
          intensity: 0.3
        }
      }
    ]
  }
];
```


### Module Communication Protocol

```javascript
const moduleMessages = {
  type: "MODULE_COMMAND",
  source: "behavior_engine",
  target: "display_module",
  timestamp: Date.now(),
  payload: {
    command: "play_animation",
    data: {
      animation_id: "step_back",
      expression: "worried_eyes",
      duration: 2000
    }
  },
  callback_required: true,
  priority: "normal" // high, normal, low
};
```


### Learning System Protocol

```javascript
const learningEvents = [
  {
    id: "learning-uuid",
    event_type: "interaction_outcome",
    context: {
      intent: "attack_me",
      reaction: "defensive_play",
      user_response: "apologetic", // positive, negative, neutral, apologetic
      outcome_rating: 0.7 // 0-1 success rating
    },
    reinforcement: {
      behavior_strength: 0.1, // positive reinforcement
      personality_drift: {
        "cautious": 0.05 // increase caution slightly
      }
    },
    timestamp: Date.now()
  }
];
```


### Task Management Protocol

```javascript
const tasks = [
  {
    id: "task-uuid",
    task_type: "focus_timer",
    trigger_conditions: ["user_says_focus", "scheduled_time"],
    requirements: {
      trust_level: 3,
      learned_skills: ["time_management"]
    },
    execution_steps: [
      { action: "confirm_duration", module: "nlp_module" },
      { action: "start_timer", module: "utility_module" },
      { action: "play_focus_music", module: "audio_module" },
      { action: "show_progress", module: "display_module" }
    ]
  }
];
```


### Memory System Protocol

```javascript
const memories = [
  {
    id: "memory-uuid",
    type: "interaction", // interaction, preference, skill, emotional
    content: {
      summary: "User apologized after saying mean things",
      emotional_weight: 0.6,
      participants: ["user", "pet"],
      outcome: "positive_resolution"
    },
    metadata: {
      timestamp: Date.now(),
      location_context: "home",
      frequency: 1,
      importance: 0.8
    },
    decay_rate: 0.95, // memory strength over time
    associations: ["trust_building", "conflict_resolution"]
  }
];
```


### Event Bus Protocol

```javascript
const eventBus = {
  subscribe: (eventType, callback, priority = "normal") => {},
  publish: (event) => {
    type: "PET_STATE_CHANGED",
    data: { stat: "happiness", oldValue: 80, newValue: 70 },
    timestamp: Date.now(),
    source: "behavior_engine"
  },
  unsubscribe: (eventType, callback) => {}
};
```


### Growth and Evolution Protocol

```javascript
const evolution = [
  {
    id: "evolution-uuid",
    trigger_type: "stat_threshold",
    conditions: {
      intelligence: 75,
      relationship_level: 4,
      days_active: 30
    },
    changes: {
      new_abilities: ["advanced_scheduling", "mood_prediction"],
      personality_unlocks: ["wise", "intuitive"],
      visual_changes: ["mature_eyes", "confident_posture"]
    },
    celebration_reaction: "evolution_dance"
  }
];
```


### Marketplace Protocol

```javascript
const marketplacePet = {
  id: "pet-uuid",
  owner_id: "user-uuid",
  listing_data: {
    price: 150, // virtual currency
    skills: ["focus_timer", "mood_support", "daily_planning"],
    personality_summary: "Calm and supportive companion",
    training_hours: 240,
    specializations: ["productivity", "emotional_support"]
  },
  verification: {
    skill_tests_passed: ["timer_accuracy", "mood_detection"],
    community_rating: 4.8,
    authenticity_score: 0.95
  }
};
```


## Module Extension Guidelines

**Adding New Modules:**

- Implement standardized message interface
- Define clear input/output

**Communication Flow:**

1. Intent Recognition → Behavior Engine
2. Behavior Engine → Decision Making
3. Decision Making → Reaction System
4. Reaction System → Output Modules


