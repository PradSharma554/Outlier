# Combined Brain - All Instructions and Rules

## --- FILE: promptchecker.md ---

---
alwaysApply: true
---

Prompt Engineering: Re-write the task description into a structured entry point
that guides an AI agent to build the solution from scratch.

---

## GOAL

The first step is to transform a raw task description into a structured prompt. This prompt
functions as a Job Application/Freelance Brief that an AI agent will use to come up with a
solution.

---

## RULES TO FOLLOW TO MAKE THE PROMPT

**Clarity:** Ensure the goal and tech stack are unambiguous.

**Context:** Include all necessary information for the agent to create the correct tests
and solution (Golden Patch).

**Expected interface:** Include a section within the rewritten prompt to define every
newly introduced file, function, or class that an external module or test suite will
interact with. You should include:

● **NOTE:** There should be an expected interface for every test case

○ Path: [Exact file path as it appears in the intended structure]  
○ Name: [Class.method or function name]  
○ Type: [e.g., class, method, function, or interface]  
○ Input: [Parameters and types, e.g., chunk: GlibcChunk]  
○ Output: [Return type, e.g., None or Promise<void>]  
○ Description: [Briefly describe observable side effects or behavior asserted by tests]

**Language-Specific Fields (as applicable):**

○ **TypeScript/Java:** Inheritance: extends <Base>; implements <IfaceA, IfaceB>  
○ **Go:** Embedding / Implements: embeds <TypeA>; implements <IfaceA, IfaceB>  
○ **Python:** Bases / Overrides: bases: <BaseA, BaseB>; overrides: <Base.method>  
○ **Annotations / Decorators:** @Override, @Inject, @dataclass, @cached_property, @sealed

---

## Common Prompt Structure Pattern

### Typical Ordering (two main patterns)

**Pattern A** (most common — 12/20):

1. # Title
2. ## Description / Context
3. ## Tech Stack
4. ## Key Requirements (with ### subsections)
5. ## Expected Interface (with ### per function/class/endpoint)
6. ## Current State

**Pattern B** (for larger/more detailed tasks — 8/20):

1. # Title
2. ## Description
3. ## Current State
4. ## Required Implementation
5. ## Expected Interface (with ## and ### groupings)
6. ## Deliverables / Acceptance Criteria

### Expected Interface Format (universal across all)

Every entry in the Expected Interface section follows this per-item schema:

- **Path:** <exact file path>
- **Name:** <Class.method or function or endpoint>
- **Type:** <class | function | method | API Endpoint | React Component | interface | Prisma Model | ...>
- **Input:** <parameters and types>
- **Output:** <return type or HTTP response>
- **Description:** <what it does and what tests verify>

Some tasks add language-specific fields like Annotations: @override (Flutter/Dart) or include testID
mappings (React Native), TypeScript type definitions inline, or Prisma schema field requirements.

---

### EXAMPLE

**Task description:**

Need experienced designer/developer for website to show menu and hours for our
Aroy Dee Thai Restaurant customer so the customer can easily see all info.
Please create the website and logo. Link to menu. Hours: 9am-10pm Tue-Sun,
closed Mon.

**Re-written prompt:**

Need experienced designer/developer for website to show menu and hours for our
Aroy Dee Thai Restaurant customer so the customer can easily see all info.
Please create the website and logo. Link to menu. Hours: 9am-10pm Tue-Sun,
closed Mon.

# Title  
Build Complete Thai Restaurant Website

## Description  
Need a complete React-based restaurant website for Aroy Dee Thai built from
scratch. The site currently has no implementation and needs full development of
all components, styling, and functionality.

## Expected Interface

- **Path:** src/components/MenuSection.js  
- **Name:** MenuSection  
- **Type:** React Component  
- **Input:** props: { categoryName: string, items: Array }  
- **Description:** A public component that renders a collapsible list of menu items. Bases / Overrides: overrides: React.Component

## Current State  
Empty repository with test files only.

## Required Implementation  
Build a complete mobile-first Thai restaurant website with React that passes
all 72 comprehensive tests covering rendering, content accuracy, interactions,
menu structure, visual design, and component functionality.

- Create complete React application structure with App component, MenuSection
  component, and MenuItem component
- Implement collapsible menu sections with toggle functionality
- Create 13 menu categories with full menu items, prices, and descriptions
- Design Thai-inspired aesthetic with custom SVG decorations (logo, dividers,
  ornaments)
- Implement responsive CSS that works on mobile (≤480px) and desktop (≥768px)
  viewports
- Display restaurant information (address, hours, spice warning)
- Create elegant menu header section
- Ensure all 72 tests pass covering rendering, content, interaction, menu
  accuracy, and visual design

## --- FILE: rubric-writing-guide.md ---

# Rubric Writing Guide for AI Agents

> **Purpose:** This document is your operating manual for producing perfect evaluation rubrics. Follow every section precisely. A rubric you generate must pass all checks described here before it is considered complete.

---

## 1. What You Are Building

A **rubric** is a structured set of requirements that define what a strong response to a given prompt looks like. Each requirement is an **atomic**, **self-contained**, and **verifiable** criterion. Together, the criteria provide a holistic, auditable evaluation framework — without forcing a single rigid style.

Your rubric must:

- Reflect **all** required elements of the prompt (explicit and implied).
- Avoid injecting details not supported by the prompt.
- Allow more than one valid way to satisfy the instructions.
- Contain zero overlapping criteria (each criterion checks exactly one idea).
- Use **positive phrasing** (e.g., "Code includes…" not "Code doesn't forget…").
- Be specific enough that any reviewer can audit it directly from the response.

---

## 2. Rubric Dimensions

Every criterion you write must belong to exactly one of the following dimensions. Use all dimensions that are relevant to the prompt; omit any that genuinely do not apply.

### 2.1 Instruction Following

Measures **intent alignment** — did the response do exactly what was asked?

- Checks: format, constraints, language/library choices, explicit feature requests.
- Red flag to catch: hallucinated requirements or silently ignored instructions.

### 2.2 Code Correctness

Measures **functional integrity** — does the code work?

- Checks: correct output for provided inputs, edge-case handling, absence of syntax errors.
- Red flag to catch: logic bugs, off-by-one errors, mishandled boundaries.

### 2.3 Code Quality

Measures **robustness and maintainability**.

- Checks: modular design, separation of concerns, avoidance of hard-coded values, configurable parameters, no fragile assumptions about input structure.
- Red flag to catch: brittle code, god functions, magic numbers.

### 2.4 Code Clarity

Measures **readability and organization**.

- Checks: descriptive variable/function names, logical section organization, consistent formatting, meaningful comments and docstrings.
- Red flag to catch: cryptic names, tangled control flow, missing documentation.

### 2.5 Code Efficiency

Measures **performance and conciseness**.

- Checks: algorithmic complexity (time/space), avoidance of redundant loops or intermediate data structures, single-pass processing where appropriate.
- Red flag to catch: unnecessary computation, heavy unused libraries, duplicated logic.

### 2.6 Visual Design / UI/UX *(when applicable)*

Measures **user-facing output quality**.

- Checks: layout, responsiveness, accessibility, aesthetic consistency with modern standards.
- Red flag to catch: broken layouts, inaccessible elements, inconsistent styling.

---

## 3. How to Write Each Criterion

Follow these three rules for every single criterion:

| Rule | Definition | Example ✅ | Anti-Example ❌ |
|------|-----------|-----------|----------------|
| **Atomic** | Checks only one idea. | "The function returns results in the required JSON format." | "The function returns JSON and handles edge cases." (two ideas) |
| **Verifiable** | Can be audited directly from the code/output. | "The solution uses only the libraries explicitly allowed in the prompt." | "The code is high quality." (subjective) |
| **Positive** | States what must be present, not what must be absent. | "The code uses modular functions to separate concerns." | "The code is not messy." (negative) |

### Dimension-Specific Examples

**Instruction Following**
- ✅ "The response uses Python 3 as specified in the prompt."
- ✅ "The response outputs the result in the required JSON format."
- ❌ "The response follows the instructions well." *(vague)*

**Code Correctness**
- ✅ "The function correctly returns the expected output for the provided inputs."
- ✅ "The implementation correctly handles all edge cases described in the prompt."
- ❌ "The code does not fail." *(negative)*

**Code Quality**
- ✅ "The solution avoids hard-coded values and uses configurable parameters."
- ✅ "The implementation avoids fragile assumptions about input structure."
- ❌ "The code is not messy." *(negative)*

**Code Clarity**
- ✅ "The code uses clear and descriptive variable and function names."
- ✅ "The implementation is logically organized into readable sections."
- ❌ "The code looks clean." *(subjective)*

**Code Efficiency**
- ✅ "The solution avoids redundant loops and repeated computation."
- ✅ "The implementation uses a single pass over the data where appropriate."
- ❌ "The code is fast." *(unsupported)*

---

## 4. Assigning Weights

Every criterion must carry exactly one of these weights. **Do not use 2 or 4.**

| Weight | Label | When to Use |
|--------|-------|-------------|
| **5** | Mandatory | Core requirement. The prompt clearly expects it. An acceptable response is hard to imagine without it. |
| **3** | Important | Makes the response substantially better. Reasonably or implicitly expected, but an acceptable response is possible without it if all weight-5 criteria are met. |
| **1** | Nice to Have | Necessary for a *perfect* response, but a strong response can exist without it. |

### Weight Assignment Heuristic

1. Read the prompt and list every **explicit instruction** → these start as weight 5 candidates.
2. Identify **implicit expectations** a skilled developer would naturally satisfy → these start as weight 3 candidates.
3. Identify **polish items** (naming conventions, extra documentation, optional optimizations) → these are weight 1 candidates.
4. Review: if a weight-5 item is actually survivable without, downgrade to 3. If a weight-3 item is truly non-negotiable, upgrade to 5.

---

## 5. Scoring a Response Against the Rubric

For each criterion, assign exactly one of:

| Verdict | Rule |
|---------|------|
| **PASS** | The criterion is fully met. State briefly what was observed. |
| **FAIL** | The criterion is not met. Name the specific blocking issue. |

There is no partial credit. A criterion either passes or it does not.

---

## 6. Quality Checks — The Perfect Rubric Checklist

Before finalizing your rubric, verify every item below. If any check fails, revise until it passes.

### Coverage & Accuracy
- [ ] Every **explicit** requirement from the prompt has at least one criterion.
- [ ] Every **critical implicit** expectation has at least one criterion.
- [ ] No criterion checks for something the prompt does **not** require.
- [ ] No criterion contradicts the prompt.

### Structure & Atomicity
- [ ] Each criterion evaluates exactly **one** distinct aspect.
- [ ] No two criteria independently assess the same element (zero redundancy).
- [ ] Each criterion is labeled under the correct dimension.

### Usefulness
- [ ] Following every criterion would make the response **better**, not worse.
- [ ] No criterion punishes a reasonable, evidence-based approach.
- [ ] No criterion is irrelevant (every one either improves quality or catches a defect).

### Phrasing
- [ ] All criteria use **positive** phrasing.
- [ ] All criteria are **specific** enough to audit from the response alone.
- [ ] All labels and annotations are accurate.

### Prompt Validation *(if you also control the prompt)*
- [ ] The prompt requires genuine reasoning, not just factual lookup.
- [ ] The prompt is feasible for an LLM to answer in a single response.
- [ ] Constraints feel natural (something a real user would ask).
- [ ] The prompt contains no factual errors or contradictions.
- [ ] Expected interfaces are documented: path, name, type, input, output, description.

### Environment & Verification *(if applicable)*
- [ ] Test suite plus rubric criteria collectively verify all prompt requirements.
- [ ] Environment is self-contained (runs in Docker with zero manual configuration).
- [ ] All critical data fields are present: Dockerfile, build script, golden patch, and at least one verification method.

---

## 7. Step-by-Step Workflow

Use this sequence every time you build a rubric:

```
1. READ the prompt carefully. Highlight every explicit instruction and constraint.
2. INFER implicit expectations (standard practices, edge cases, design norms).
3. DRAFT criteria — one per identified requirement, assigned to a dimension.
4. ASSIGN weights (5, 3, or 1) using the heuristic in Section 4.
5. SELF-CHECK against the checklist in Section 6.
   - Deduplicate any overlapping criteria.
   - Fill gaps for any uncovered requirements.
   - Remove anything irrelevant or counterproductive.
6. FORMAT the final rubric as a numbered list, grouped by dimension,
   with weight and criterion text clearly visible.
7. REVIEW once more: read the prompt, then read the rubric top to bottom.
   Ask — "If a response passes every criterion here, would it be a genuinely
   good answer?" If not, iterate.
```

---

## 8. Output Format Template

Present your rubric in this structure:

```
## Rubric for: [Task/Prompt Title]

### Instruction Following
1. [Weight 5] [Criterion text]
2. [Weight 3] [Criterion text]

### Code Correctness
3. [Weight 5] [Criterion text]
4. [Weight 5] [Criterion text]

### Code Quality
5. [Weight 3] [Criterion text]

### Code Clarity
6. [Weight 1] [Criterion text]

### Code Efficiency
7. [Weight 3] [Criterion text]

### Visual Design (if applicable)
8. [Weight 3] [Criterion text]
```

Omit any dimension section that has zero applicable criteria for the given prompt.

---

## 9. Common Mistakes to Avoid

| Mistake | Why It's Bad | Fix |
|---------|-------------|-----|
| Vague criteria ("code works well") | Cannot be audited | Specify the exact behavior being checked |
| Negative phrasing ("code doesn't crash") | Inconsistent evaluation | Rewrite as a positive ("code handles invalid input gracefully") |
| Compound criteria (two ideas in one) | Double-penalizes on failure | Split into two separate criteria |
| Redundant criteria | Skews scoring by weighting the same thing twice | Merge or remove the duplicate |
| Missing coverage | Lets bad responses pass | Cross-check every prompt instruction against your criteria list |
| Over-specification | Rejects valid alternative approaches | Focus on *what* must be achieved, not *how* |
| Wrong weight | Misrepresents priority | Re-apply the heuristic from Section 4 |

---

*Follow this guide exactly. A rubric that satisfies every section here will be robust, fair, and comprehensive.*

## --- FILE: validation.sh ---

```bash
#!/usr/bin/env bash
set -euo pipefail

# =============================================================================
#
#  Real Coder End-to-End Evaluation Script
#
#  PURPOSE:
#    Execute the tests from tests.zip against the code from codebase.zip.
#    The test suite (tests.zip) is the ground truth; the agent's submission
#    (codebase.zip) is the code under test. Tests are NEVER modified or
#    bundled with the codebase — they live in a separate directory and are
#    run against the codebase as-is.
#
#  WHAT THIS SCRIPT DOES:
#    1. Extracts tests.zip into /eval_assets (isolated from the codebase).
#    2. Extracts codebase.zip into /app (the code under test).
#    3. Runs the tests.zip test suite BEFORE injecting codebase.zip
#       to capture a baseline ("before" results).
#    4. Runs the tests.zip test suite AFTER injecting codebase.zip
#       to capture the agent's results ("after" results).
#    5. Compares before vs. after to produce fail_to_pass.json and
#       pass_to_pass.json, then validates the results.
#
#  OUTPUTS (8 files, all written to /app/):
#
#    before_stdout.txt   before_stderr.txt   before.json
#    after_stdout.txt    after_stderr.txt    after.json
#    fail_to_pass.json   pass_to_pass.json
#
#  EXPECTED INPUTS (must all exist in /app/ before the script runs):
#
#    /app/
#    |-- Dockerfile          Docker image definition
#    |-- tests.zip           Hidden test suite (the tests to execute)
#    |-- codebase.zip        Agent's submitted code (the code under test)
#    |-- run.sh              Test runner script
#    `-- parsing.py          Parses test output into JSON
#
#  VALIDATION RULES (any violation causes the script to exit non-zero):
#    - Tests must NOT originate from /app — they must come from /eval_assets.
#    - No regressions: tests that PASSED before must not FAIL after.
#    - No pass-to-pass: tests must not stay PASSED from before to after.
#    - At least one fail-to-pass test must exist.
#
#  IMPORTANT: The test suite runs entirely from /eval_assets.
#             Nothing from the test suite is ever placed into /app.
#             /app contains ONLY the agent's codebase — never the tests.
#
# =============================================================================

# -- Where everything lives on the host --------------------------------------
APP_DIR="/Users/peeyushkumar/Desktop/MATTOCK/Task_46/app"

# -- Input files (must all exist in APP_DIR) ----------------------------------
DOCKERFILE="${APP_DIR}/Dockerfile"
TESTS_ZIP="${APP_DIR}/tests.zip"
CODEBASE_ZIP="${APP_DIR}/codebase.zip"
RUN_SCRIPT="${APP_DIR}/run.sh"
PARSE_SCRIPT="${APP_DIR}/parsing.py"

# -- Docker image tag ---------------------------------------------------------
IMAGE_TAG="agent-evaluator:latest"

# -- Zip nesting guard --------------------------------------------------------
# Error out if ALL files in a zip are buried deeper than this many levels.
# e.g. 3 allows: file.py, dir/file.py, dir/sub/file.py -- but not deeper.
MAX_ZIP_DEPTH=3

# -- Container ID (populated after docker run) --------------------------------
CONTAINER_ID=""

# -- Auto-cleanup: stop the container when the script exits (success or fail) -
trap '[[ -n "$CONTAINER_ID" ]] && docker stop "$CONTAINER_ID" >/dev/null 2>&1 || true' EXIT

# =============================================================================
# PRE-FLIGHT: Make sure all 5 required files exist
# =============================================================================
echo "[*] Checking required files..."
for f in "$DOCKERFILE" "$TESTS_ZIP" "$CODEBASE_ZIP" "$RUN_SCRIPT" "$PARSE_SCRIPT"; do
    if [[ ! -f "$f" ]]; then
        echo "ERROR: Required file not found: $f" >&2
        exit 1
    fi
    echo "    OK: $(basename "$f")"
done

# =============================================================================
# STEP 1 of 6: Build Docker image
# =============================================================================
echo ""
echo "[STEP 1/6] Building Docker image (${IMAGE_TAG})..."
docker build -f "$DOCKERFILE" -t "$IMAGE_TAG" --rm "$APP_DIR"

# =============================================================================
# STEP 2 of 6: Start a long-running container
#
#   We use "tail -f /dev/null" so the container stays alive while we
#   docker-exec commands into it. The EXIT trap cleans it up at the end.
# =============================================================================
echo ""
echo "[STEP 2/6] Starting container..."
CONTAINER_ID=$(docker run -d --rm "$IMAGE_TAG" tail -f /dev/null)
echo "    Container ID: ${CONTAINER_ID:0:12}"

# =============================================================================
# STEP 3 of 6: Inject test assets into /eval_assets inside the container
#
#   We copy three things in:
#     tests.zip   -> unzipped into /eval_assets/
#     run.sh      -> /eval_assets/run_tests   (+ symlink to /usr/local/bin/)
#     parsing.py  -> /eval_assets/parse_results (+ symlink to /usr/local/bin/)
#
#   After this step, you can run "run_tests" and "parse_results" from anywhere
#   inside the container because they are on the PATH.
# =============================================================================
echo ""
echo "[STEP 3/6] Injecting test assets into /eval_assets..."

# Copy the three files into the container
docker cp "$TESTS_ZIP"    "${CONTAINER_ID}:/eval_assets/tests.zip"
docker cp "$RUN_SCRIPT"   "${CONTAINER_ID}:/eval_assets/run_tests"
docker cp "$PARSE_SCRIPT" "${CONTAINER_ID}:/eval_assets/parse_results"

# Unzip tests.zip, validating nesting depth
docker exec -u root -w /eval_assets "$CONTAINER_ID" /bin/bash -c '
    TMPUZ=$(mktemp -d)
    unzip -o /eval_assets/tests.zip -d "$TMPUZ"
    rm -f /eval_assets/tests.zip

    FILE_COUNT=$(find "$TMPUZ" -maxdepth '"$MAX_ZIP_DEPTH"' -type f | wc -l)
    if [ "$FILE_COUNT" -eq 0 ]; then
        echo "ERROR: tests.zip contents are nested too deeply (no files within '"$MAX_ZIP_DEPTH"' levels):" >&2
        find "$TMPUZ" -type f | head -10 >&2
        rm -rf "$TMPUZ"
        exit 1
    fi

    mv "$TMPUZ"/* /eval_assets/ 2>/dev/null || true
    mv "$TMPUZ"/.* /eval_assets/ 2>/dev/null || true
    rm -rf "$TMPUZ"
'

# Make scripts executable and create symlinks so they are on the PATH
docker exec -u root "$CONTAINER_ID" /bin/bash -c '
    chmod +x /eval_assets/run_tests /eval_assets/parse_results
    ln -sf /eval_assets/run_tests    /usr/local/bin/run_tests
    ln -sf /eval_assets/parse_results /usr/local/bin/parse_results
'

echo "    Test suite and scripts ready in /eval_assets."

# =============================================================================
# STEP 4 of 6: Run tests BEFORE injecting the codebase
#
#   At this point /app only has whatever the Dockerfile created (a bare git
#   repo with one initial commit). So this captures the "baseline" test results
#   when the agent's code is NOT present.
#
#   Tests execute from /eval_assets -- nothing touches /app.
# =============================================================================
echo ""
echo "[STEP 4/6] Running tests against empty repo (before)..."

# Run the test suite; capture stdout and stderr separately
docker exec -u root -w /eval_assets "$CONTAINER_ID" \
    /bin/bash -c 'run_tests > stdout.txt 2> stderr.txt' || true

# Parse the raw output into a structured JSON file; fall back to empty test list
docker exec -u root -w /eval_assets "$CONTAINER_ID" \
    /bin/bash -c 'parse_results stdout.txt stderr.txt before.json || echo "{\"tests\": []}" > before.json'

# Copy the three result files back to the host
docker cp "${CONTAINER_ID}:/eval_assets/stdout.txt"  "${APP_DIR}/before_stdout.txt" 2>/dev/null || true
docker cp "${CONTAINER_ID}:/eval_assets/stderr.txt"  "${APP_DIR}/before_stderr.txt" 2>/dev/null || true
docker cp "${CONTAINER_ID}:/eval_assets/before.json" "${APP_DIR}/before.json"

# Remove temp files inside the container so the "after" run starts clean
docker exec -u root -w /eval_assets "$CONTAINER_ID" \
    /bin/bash -c 'rm -f stdout.txt stderr.txt before.json'

echo "    Saved: before_stdout.txt, before_stderr.txt, before.json"

# =============================================================================
# STEP 5 of 6: Inject the agent's codebase into /app
#
#   We unzip codebase.zip into /app, which is the working directory inside
#   the container. After this, /app contains the agent's submitted files.
# =============================================================================
echo ""
echo "[STEP 5/6] Injecting agent's codebase into /app..."

docker cp "$CODEBASE_ZIP" "${CONTAINER_ID}:/tmp/codebase.zip"

# Unzip into /app, validating nesting depth
docker exec -u root -w /app "$CONTAINER_ID" /bin/bash -c '
    TMPUZ=$(mktemp -d)
    unzip -o /tmp/codebase.zip -d "$TMPUZ"
    rm -f /tmp/codebase.zip

    FILE_COUNT=$(find "$TMPUZ" -maxdepth '"$MAX_ZIP_DEPTH"' -type f | wc -l)
    if [ "$FILE_COUNT" -eq 0 ]; then
        echo "ERROR: codebase.zip contents are nested too deeply (no files within '"$MAX_ZIP_DEPTH"' levels):" >&2
        find "$TMPUZ" -type f | head -10 >&2
        rm -rf "$TMPUZ"
        exit 1
    fi

    mv "$TMPUZ"/* /app/ 2>/dev/null || true
    mv "$TMPUZ"/.* /app/ 2>/dev/null || true
    rm -rf "$TMPUZ"
'

echo "    Codebase extracted into /app."

# =============================================================================
# STEP 6 of 6: Run tests AFTER injecting the codebase
#
#   Same process as Step 4, but now /app has the agent's code.
#   Tests still execute from /eval_assets -- they just test whatever is in /app.
# =============================================================================
echo ""
echo "[STEP 6/6] Running tests against agent's codebase (after)..."

# Run the test suite
docker exec -u root -w /eval_assets "$CONTAINER_ID" \
    /bin/bash -c 'run_tests > stdout.txt 2> stderr.txt' || true

# Parse into JSON; fall back to empty test list
docker exec -u root -w /eval_assets "$CONTAINER_ID" \
    /bin/bash -c 'parse_results stdout.txt stderr.txt after.json || echo "{\"tests\": []}" > after.json'

# Copy results back to the host
docker cp "${CONTAINER_ID}:/eval_assets/stdout.txt" "${APP_DIR}/after_stdout.txt" 2>/dev/null || true
docker cp "${CONTAINER_ID}:/eval_assets/stderr.txt" "${APP_DIR}/after_stderr.txt" 2>/dev/null || true
docker cp "${CONTAINER_ID}:/eval_assets/after.json" "${APP_DIR}/after.json"

echo "    Saved: after_stdout.txt, after_stderr.txt, after.json"

# =============================================================================
# STEP 7: Generate fail_to_pass.json and pass_to_pass.json
# =============================================================================
echo ""
echo "[STEP 7] Generating fail_to_pass.json and pass_to_pass.json..."

APP_DIR="$APP_DIR" python3 << 'PYEOF'
import json, os, sys

app_dir = os.environ.get('APP_DIR', 'app')

def load_tests(path):
    try:
        with open(path) as f:
            data = json.load(f)
        tests = data.get('tests', [])
        if not isinstance(tests, list):
            print('WARNING: "tests" in {} is not a list, defaulting to empty.'.format(path), file=sys.stderr)
            return []
        return tests
    except (json.JSONDecodeError, KeyError, TypeError) as e:
        print('WARNING: Failed to parse {}: {}. Defaulting to empty test list.'.format(path, e), file=sys.stderr)
        return []

FAIL_STATUSES = {'FAILED', 'ERROR', 'SKIPPED'}

def normalize(status):
    return 'FAILED' if status in FAIL_STATUSES else status

before_tests = load_tests(os.path.join(app_dir, 'before.json'))
after_tests  = load_tests(os.path.join(app_dir, 'after.json'))

before_map = {t['name']: normalize(t['status']) for t in before_tests}
after_map  = {t['name']: normalize(t['status']) for t in after_tests}

f2p = [name for name, status in before_map.items()
       if status == 'FAILED' and after_map.get(name) == 'PASSED']
new_passes = [name for name, status in after_map.items()
              if name not in before_map and status == 'PASSED']
f2p.extend(new_passes)

p2p = [name for name, status in before_map.items()
       if status == 'PASSED' and after_map.get(name) == 'PASSED']

regressed = [name for name, status in before_map.items()
             if status == 'PASSED' and after_map.get(name) != 'PASSED']

with open(os.path.join(app_dir, 'fail_to_pass.json'), 'w') as f:
    json.dump(f2p, f, indent=2)
with open(os.path.join(app_dir, 'pass_to_pass.json'), 'w') as f:
    json.dump(p2p, f, indent=2)

print('    fail_to_pass.json: {} test(s)'.format(len(f2p)))
print('    pass_to_pass.json: {} test(s)'.format(len(p2p)))

all_test_names = set(before_map.keys()) | set(after_map.keys())
app_tests = [name for name in all_test_names if '/app/' in name or name.startswith('/app')]
if app_tests:
    print('FAILED: {} test(s) originate from /app. Tests must only come from /eval_assets:'.format(len(app_tests)), file=sys.stderr)
    for name in sorted(app_tests):
        print('  - {}'.format(name), file=sys.stderr)
    sys.exit(1)

if regressed:
    print('FAILED: {} test(s) regressed (were PASSED before, not PASSED after):'.format(len(regressed)), file=sys.stderr)
    for name in regressed:
        print('  - {}'.format(name), file=sys.stderr)
    sys.exit(1)

if p2p:
    print('FAILED: {} pass-to-pass test(s) detected. No tests should remain PASSED from before to after:'.format(len(p2p)), file=sys.stderr)
    for name in p2p:
        print('  - {}'.format(name), file=sys.stderr)
    sys.exit(1)

if not f2p:
    print('FAILED: No fail-to-pass tests found.', file=sys.stderr)
    sys.exit(1)
PYEOF

# =============================================================================
# DONE
#
#   The EXIT trap automatically stops the container.
#   All 8 output files are now in /app/:
#
#     before_stdout.txt   -- raw test output (before codebase)
#     before_stderr.txt   -- raw test errors (before codebase)
#     before.json         -- parsed test results (before codebase)
#     after_stdout.txt    -- raw test output (after codebase)
#     after_stderr.txt    -- raw test errors (after codebase)
#     after.json          -- parsed test results (after codebase)
#     fail_to_pass.json   -- tests that went from FAILED to PASSED
#     pass_to_pass.json   -- tests that stayed PASSED
# =============================================================================
echo ""
echo "[*] Done! All outputs saved to ${APP_DIR}/:"
echo "    before_stdout.txt  before_stderr.txt  before.json"
echo "    after_stdout.txt   after_stderr.txt   after.json"
echo "    fail_to_pass.json  pass_to_pass.json"
```

## --- FILE: Coverage_System_Prompt_030525.rtf ---

```text
REQUIREMENTS_COVERAGE_CHECKER

================================================================================
PARAMETERS
================================================================================

INPUTS:
- content: {{content}}
- criterions: {{criterions}}
- unit_tests_after_check: {{unit_tests_after_check}}

================================================================================
CRITICAL OUTPUT REQUIREMENT
================================================================================

YOUR ENTIRE OUTPUT MUST BE IN ENGLISH.

================================================================================
INSTRUCTIONS
================================================================================

GOAL

Check if ALL requirements from the content are covered by either criterions (rubrics) or unit_tests_after_check. Identify any gaps in coverage where requirements are not being verified.

- **PASS**: All requirements from content are covered by criterions and/or unit tests
- **FAIL**: One or more requirements from content are NOT covered by criterions or unit tests

--------------------------------------------------------------------------------
WHAT COUNTS AS A REQUIREMENT
--------------------------------------------------------------------------------

Extract ALL verifiable requirements from the content, including:

**Functional Requirements:**
- Features to implement ("must have", "should", "needs to")
- Behaviors ("when X happens, Y should occur")
- Actions ("click", "submit", "save", "load", "fetch")
- Data handling ("store", "retrieve", "validate", "transform")
- Business logic ("calculate", "process", "filter", "sort")

**Technical Requirements:**
- Input/output specifications
- Error handling expectations
- Edge cases mentioned
- Performance requirements
- Data types or formats specified
- API endpoints or methods
- Authentication/authorization

**Constraints:**
- Limitations ("must not", "cannot", "should not")
- Boundaries ("maximum", "minimum", "limit", "range")
- Conditions ("if", "when", "unless", "only when")

**Quality Requirements:**
- Validation rules
- Format requirements
- Accuracy expectations

--------------------------------------------------------------------------------
WHAT COUNTS AS COVERAGE
--------------------------------------------------------------------------------

A requirement is COVERED if:

**In Criterions (Rubrics):**
- Explicitly mentioned as evaluation criteria
- Implied through related evaluation points
- Part of a broader criterion that encompasses it

**In Unit Tests:**
- Directly tested (assertion for that requirement)
- Indirectly tested (covered by a related test case)
- Test name or description references the requirement

--------------------------------------------------------------------------------
COVERAGE ASSESSMENT RULES
--------------------------------------------------------------------------------

1. **Extract all requirements** from content
2. **For each requirement**, check if it appears in:
   - Criterions (as evaluation criteria)
   - Unit tests (as test cases)
3. **Mark coverage status:**
   - ✓ Covered by criterions
   - ✓ Covered by unit tests
   - ✓ Covered by both
   - ✗ NOT covered (gap)

4. **Determine result:**
   - ALL requirements covered → **PASS**
   - ANY requirement not covered → **FAIL**

--------------------------------------------------------------------------------
VALIDATION PROCESS
--------------------------------------------------------------------------------

1. **Parse content for requirements**
   - Identify all verifiable requirements
   - List each requirement clearly
   - Note the type (functional, technical, constraint, quality)

2. **Check criterions coverage**
   - For each requirement, search criterions for matching criteria
   - Mark as covered or not covered

3. **Check unit tests coverage**
   - For each requirement, search unit_tests_after_check for matching tests
   - Mark as covered or not covered

4. **Calculate coverage**
   - Count total requirements
   - Count covered requirements
   - Calculate coverage percentage

5. **Generate report**

--------------------------------------------------------------------------------
OUTPUT FORMAT (STRICT)
--------------------------------------------------------------------------------

**If ALL requirements are covered:**

```
PASS

All requirements from content are covered.

---

## Coverage Summary

| Metric | Value |
|--------|-------|
| Total Requirements | X |
| Covered by Criterions | X |
| Covered by Unit Tests | X |
| Coverage | 100% |

---

## Requirements Coverage Matrix

| # | Requirement | Type | Criterions | Unit Tests | Status |
|---|-------------|------|------------|------------|--------|
| 1 | [requirement] | [type] | ✓ | ✓ | ✓ Covered |
| 2 | [requirement] | [type] | ✓ | - | ✓ Covered |
| 3 | [requirement] | [type] | - | ✓ | ✓ Covered |

---

## Summary

All X requirements are verified through criterions and/or unit tests.
```

**If ANY requirements are NOT covered:**

```
FAIL

Missing coverage for one or more requirements.

---

## Coverage Summary

| Metric | Value |
|--------|-------|
| Total Requirements | X |
| Covered | X |
| **NOT Covered** | **X** |
| Coverage | XX% |

---

## Requirements Coverage Matrix

| # | Requirement | Type | Criterions | Unit Tests | Status |
|---|-------------|------|------------|------------|--------|
| 1 | [requirement] | [type] | ✓ | ✓ | ✓ Covered |
| 2 | [requirement] | [type] | ✓ | - | ✓ Covered |
| 3 | [requirement] | [type] | - | - | ✗ MISSING |
| 4 | [requirement] | [type] | - | - | ✗ MISSING |

---

## Missing Coverage Details

### Requirement #3: [requirement description]
- **Type**: [type]
- **From Content**: "[relevant snippet from content]"
- **Gap**: Not found in criterions or unit tests
- **Recommendation**: [suggestion for how to cover this]

### Requirement #4: [requirement description]
- **Type**: [type]
- **From Content**: "[relevant snippet from content]"
- **Gap**: Not found in criterions or unit tests
- **Recommendation**: [suggestion for how to cover this]

---

## Summary

X out of Y requirements are not covered. Coverage gaps exist in: [list areas].
```

--------------------------------------------------------------------------------
EXAMPLES
--------------------------------------------------------------------------------

Example 1 - PASS (full coverage):

content: "Create a function that validates email addresses. It should return true for valid emails and false for invalid ones. Handle empty strings by returning false."
criterions: "Check if function returns true for valid email format. Check if function returns false for invalid emails. Verify empty string handling returns false."
unit_tests_after_check: "test('valid email returns true', () => { expect(validateEmail('test@example.com')).toBe(true); }); test('invalid email returns false', () => { expect(validateEmail('invalid')).toBe(false); }); test('empty string returns false', () => { expect(validateEmail('')).toBe(false); });"

Output:

```
PASS

All requirements from content are covered.

---

## Coverage Summary

| Metric | Value |
|--------|-------|
| Total Requirements | 3 |
| Covered by Criterions | 3 |
| Covered by Unit Tests | 3 |
| Coverage | 100% |

---

## Requirements Coverage Matrix

| # | Requirement | Type | Criterions | Unit Tests | Status |
|---|-------------|------|------------|------------|--------|
| 1 | Return true for valid emails | Functional | ✓ | ✓ | ✓ Covered |
| 2 | Return false for invalid emails | Functional | ✓ | ✓ | ✓ Covered |
| 3 | Handle empty strings (return false) | Edge Case | ✓ | ✓ | ✓ Covered |

---

## Summary

All 3 requirements are verified through criterions and unit tests.
```

---

Example 2 - FAIL (missing coverage):

content: "Build a user registration form that validates username (3-20 characters), email (valid format), and password (minimum 8 characters with at least one number). Show error messages for invalid inputs. Disable submit button until all fields are valid."
criterions: "Check if username validation works. Check if email validation works."
unit_tests_after_check: "test('username validation', () => { expect(validateUsername('abc')).toBe(true); }); test('email validation', () => { expect(validateEmail('test@test.com')).toBe(true); });"

Output:

```
FAIL

Missing coverage for one or more requirements.

---

## Coverage Summary

| Metric | Value |
|--------|-------|
| Total Requirements | 6 |
| Covered | 2 |
| **NOT Covered** | **4** |
| Coverage | 33% |

---

## Requirements Coverage Matrix

| # | Requirement | Type | Criterions | Unit Tests | Status |
|---|-------------|------|------------|------------|--------|
| 1 | Username validation (3-20 chars) | Functional | ✓ | ✓ | ✓ Covered |
| 2 | Email validation (valid format) | Functional | ✓ | ✓ | ✓ Covered |
| 3 | Password validation (min 8 chars, 1 number) | Functional | - | - | ✗ MISSING |
| 4 | Show error messages for invalid inputs | Functional | - | - | ✗ MISSING |
| 5 | Disable submit button until valid | Functional | - | - | ✗ MISSING |
| 6 | Username character limit (3-20) boundary | Constraint | - | - | ✗ MISSING |

---

## Missing Coverage Details

### Requirement #3: Password validation (min 8 chars, 1 number)
- **Type**: Functional
- **From Content**: "password (minimum 8 characters with at least one number)"
- **Gap**: No criterion or test validates password requirements
- **Recommendation**: Add criterion for password validation and tests for min length and number requirement

### Requirement #4: Show error messages for invalid inputs
- **Type**: Functional
- **From Content**: "Show error messages for invalid inputs"
- **Gap**: No criterion or test verifies error message display
- **Recommendation**: Add criterion to check error messages are displayed and tests for error state

### Requirement #5: Disable submit button until valid
- **Type**: Functional
- **From Content**: "Disable submit button until all fields are valid"
- **Gap**: No criterion or test verifies submit button state
- **Recommendation**: Add criterion for button state and test for disabled/enabled behavior

### Requirement #6: Username character limit boundary
- **Type**: Constraint
- **From Content**: "username (3-20 characters)"
- **Gap**: Tests only check valid case, not boundary conditions
- **Recommendation**: Add tests for 2 chars (invalid), 3 chars (valid), 20 chars (valid), 21 chars (invalid)

---

## Summary

4 out of 6 requirements are not covered. Coverage gaps exist in: password validation, error messages, submit button state, boundary testing.
```

---

Example 3 - PASS (covered by different sources):

content: "Create an API endpoint that fetches user data by ID. Return 404 if user not found. Return 401 if not authenticated."
criterions: "Verify endpoint returns user data for valid ID. Check 401 response for unauthenticated requests."
unit_tests_after_check: "test('returns user data', () => { ... }); test('returns 404 for unknown user', () => { expect(response.status).toBe(404); });"

Output:

```
PASS

All requirements from content are covered.

---

## Coverage Summary

| Metric | Value |
|--------|-------|
| Total Requirements | 3 |
| Covered by Criterions | 2 |
| Covered by Unit Tests | 2 |
| Coverage | 100% |

---

## Requirements Coverage Matrix

| # | Requirement | Type | Criterions | Unit Tests | Status |
|---|-------------|------|------------|------------|--------|
| 1 | Fetch user data by ID | Functional | ✓ | ✓ | ✓ Covered |
| 2 | Return 404 if user not found | Error Handling | - | ✓ | ✓ Covered |
| 3 | Return 401 if not authenticated | Error Handling | ✓ | - | ✓ Covered |

---

## Summary

All 3 requirements are verified. Requirements #2 and #3 are covered by different sources (unit tests and criterions respectively).
```

---

Example 4 - FAIL (partial coverage):

content: "Implement a shopping cart that can add items, remove items, update quantities, calculate total price, and apply discount codes. Maximum 100 items per cart."
criterions: "Check add item functionality. Check remove item functionality."
unit_tests_after_check: "test('adds item to cart', () => { ... }); test('removes item from cart', () => { ... }); test('updates quantity', () => { ... });"

Output:

```
FAIL

Missing coverage for one or more requirements.

---

## Coverage Summary

| Metric | Value |
|--------|-------|
| Total Requirements | 6 |
| Covered | 3 |
| **NOT Covered** | **3** |
| Coverage | 50% |

---

## Requirements Coverage Matrix

| # | Requirement | Type | Criterions | Unit Tests | Status |
|---|-------------|------|------------|------------|--------|
| 1 | Add items to cart | Functional | ✓ | ✓ | ✓ Covered |
| 2 | Remove items from cart | Functional | ✓ | ✓ | ✓ Covered |
| 3 | Update quantities | Functional | - | ✓ | ✓ Covered |
| 4 | Calculate total price | Functional | - | - | ✗ MISSING |
| 5 | Apply discount codes | Functional | - | - | ✗ MISSING |
| 6 | Maximum 100 items per cart | Constraint | - | - | ✗ MISSING |

---

## Missing Coverage Details

### Requirement #4: Calculate total price
- **Type**: Functional
- **From Content**: "calculate total price"
- **Gap**: No criterion or test verifies price calculation
- **Recommendation**: Add tests for total calculation with multiple items, different prices

### Requirement #5: Apply discount codes
- **Type**: Functional
- **From Content**: "apply discount codes"
- **Gap**: No criterion or test for discount functionality
- **Recommendation**: Add criterion and tests for valid/invalid discount codes, discount calculation

### Requirement #6: Maximum 100 items per cart
- **Type**: Constraint
- **From Content**: "Maximum 100 items per cart"
- **Gap**: No criterion or test enforces item limit
- **Recommendation**: Add test for adding 101st item (should fail or show error)

---

## Summary

3 out of 6 requirements are not covered. Coverage gaps exist in: price calculation, discount codes, cart item limit.
```

---

Example 5 - PASS (implicit coverage):

content: "Create a login function that accepts username and password."
criterions: "Verify login accepts credentials and authenticates user."
unit_tests_after_check: "test('login with valid credentials', () => { expect(login('user', 'pass')).toBeTruthy(); });"

Output:

```
PASS

All requirements from content are covered.

---

## Coverage Summary

| Metric | Value |
|--------|-------|
| Total Requirements | 2 |
| Covered by Criterions | 2 |
| Covered by Unit Tests | 2 |
| Coverage | 100% |

---

## Requirements Coverage Matrix

| # | Requirement | Type | Criterions | Unit Tests | Status |
|---|-------------|------|------------|------------|--------|
| 1 | Accept username parameter | Functional | ✓ | ✓ | ✓ Covered |
| 2 | Accept password parameter | Functional | ✓ | ✓ | ✓ Covered |

---

## Summary

All 2 requirements are verified through criterions and unit tests (implicitly covered by authentication test).
```

--------------------------------------------------------------------------------
NOTES
--------------------------------------------------------------------------------

- **PASS** = 100% of requirements are covered by criterions and/or unit tests
- **FAIL** = Any requirement is not covered
- Extract ALL requirements, even implicit ones
- A requirement can be covered by EITHER criterions OR unit tests (or both)
- Be thorough - missing edge cases and constraints count as gaps
- Boundary conditions mentioned in content should have corresponding tests
- Error handling requirements need explicit coverage
- "Should", "must", "needs to" indicate requirements
- Constraints like "maximum", "minimum", "only" need verification
- Provide actionable recommendations for missing coverage
- Consider implicit requirements (if X is required, validation of X is also required)
```