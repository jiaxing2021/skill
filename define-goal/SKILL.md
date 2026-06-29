---
name: define-goal

description: Help the user define a concrete, measurable goal before starting work. Shapes vague intentions into bounded, verifiable objectives with clear success criteria and scope boundaries. Use when the user asks to set a goal, define an objective, clarify what they want, or when a task description is ambiguous or too broad. Invoked via /define-goal.
---
# Define Goal

## Purpose

Shape the user's intent into an objective that can be pursued honestly. Prefer measurable outcomes, explicit evidence, and bounded scope over activity descriptions.

## When to Use

- User invokes `/define-goal`
- User says "I want to...", "help me with...", or describes a vague intention
- A task description is ambiguous, too broad, or lacks success criteria
- Before starting large multi-step work where scope creep is a risk

Do NOT use this skill for simple, clear implementation tasks (e.g., "add a log line to function X").

## Workflow

### Step 1: Restate the Likely Goal

Before doing any work, restate the user's intent in concrete terms. A usable goal must name:

-**Outcome**: The specific thing that will be true when done

-**Artifact**: The main system, file, module, or behavior involved

-**Verification**: How completion will be proven

-**In scope**: What is included

-**Out of scope**: What is explicitly excluded (when ambiguity would matter)

-**Stop condition**: When to stop and ask the user instead of guessing

### Step 2: Quantify When Possible

Prefer numbers that represent real success, not decorative precision:

| Type | Examples |

|------|---------|

| Pass/fail validators | Specific test commands, CI checks, lint rules, acceptance criteria |

| Quality thresholds | Latency, error rate, accuracy, recall, memory, coverage, build time |

| Artifact constraints | File paths, affected modules, output formats, target environments |

| Evidence counts | Number of reproduced bugs, successful test runs, reviewed examples |

### Step 3: Repair Weak Goals

Before proceeding, check the goal against the quality bar:

**Reject pure activity goals** — rewrite them into verifiable outcomes:

| Weak (Reject) | Strong (Accept) |

|---------------|-----------------|

| "Make checkout faster" | "Reduce checkout API p95 latency below 250ms, verify with `npm run test:checkout` passing across 3 consecutive runs" |

| "Improve the code" | "Resolve all lint warnings in `src/`, verify with `npm run lint` exiting cleanly" |

| "Keep investigating" | "Identify the root cause of the segfault in `main.cpp:42`, reproduce with a minimal test case, and propose a fix verified by the test passing" |

| "Work on the model" | "Quantize `bge-small-zh` to INT8 with less than 2% cosine similarity drop vs FP32 baseline, verify with `scripts/compare_pt_onnx.py`" |

### Step 4: Ask Clarifying Questions (Only When Needed)

Ask only when a reasonable rewrite would risk pursuing the wrong outcome. Keep questions short and focused:

- "What metric defines success here: accuracy, latency, or output format?"
- "Which environment should I verify against: local x86 or target aarch64?"
- "What is the minimum evidence you want before I mark this done?"

If the user cannot provide a metric, propose the most honest binary validator available and ask for confirmation.

### Step 5: Lock the Goal and Plan

Once the goal passes the quality bar:

1.**State the final goal** in one concise sentence to the user

2.**Use `CreatePlan`** to formalize the goal into a structured plan with clear tasks

3.**Use `TodoWrite`** to track execution progress against the plan

## Goal Quality Checklist

Before proceeding to execution, verify:

- [ ] What concrete thing will be true when this is done?
- [ ] What evidence will prove it?
- [ ] What quantitative or binary threshold defines success?
- [ ] What scope boundaries are set?
- [ ] What should cause me to stop and ask instead of guessing?

If any item is unclear, go back to Step 4 and ask.

## Quantification Heuristics by Task Type

### Bug Fixes

- Define success as: reproduction first, fix second, regression test third
- Validator: a failing-then-passing test case

### Performance

- Name the metric, target threshold, measurement method, and number of runs
- Example: "RKNN inference latency < 50ms per query, measured with `time` over 100 runs"

### Feature Implementation

- Define observable acceptance criteria
- Example: "New `/embed` endpoint returns 512-dim vectors, verified by `test_similarity.py` with cosine > 0.95 for known pairs"

### Refactoring

- Define what must remain unchanged (behavior, test results)
- Define what improves (readability score, line count, duplication)

### Research / Investigation

- Define the decision the research must enable
- Define sources in scope and evidence standard

## Output Format

Present the locked goal to the user in this format:

```

## Goal

[One concise sentence describing the objective]


## Success Criteria

- [Criterion 1 with metric/threshold]

- [Criterion 2 with metric/threshold]


## Scope

- **In**: [what is included]

- **Out**: [what is excluded]


## Verification

- [Exact command or method to prove completion]


## Stop Conditions

- [When to pause and ask the user]

```

Then ask the user to confirm before proceeding to execution.

## Guidelines

-**Never start work without a locked goal** when this skill is active

-**Never silently expand scope** — if something new comes up, flag it and ask

-**Prefer asking once** over guessing wrong and re-doing work

- Keep the goal visible throughout execution by referencing it in progress updates
- If the goal becomes stale mid-work (context changed), pause and re-validate with the user
