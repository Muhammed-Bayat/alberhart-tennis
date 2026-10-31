# Qoder Exam Plan — Fast, Credit-Efficient Version


## Workflow at a glance

| Stage | What happens | Who decides what comes next? |
| --- | --- | --- |
| **1 — Plan** | Read entire specification, identify mandatory requirements and rank optional batches once | **You** approve the plan |
| **2 — Working base** | Build base, create README, run app and tests | **You** smoke-test; Qoder commits/pushes **after approval** |
| **3 — Finalise optional queue** | **Once only:** adjust provisional batch ranking to the actual working base | **You** approve the order |
| **4 — First batch** | Implement **highest-ranked viable** batch, test, leave app running | **You** smoke-test; Qoder commits/pushes **after approval** |
| **4 — Next batches** | Say **“Implement the next batch”**; no repeat of the full Step 3 or Step 4 | Same smoke-test and Git approval rule |
| **5 — Final audit** | Freeze features and check the complete submission | Only fix submission-critical problems |

---

## 1. Plan the Entire Test First

**Use once:** At the beginning, before any implementation. **Goal:** A complete but concise plan and a **provisional ranked batch list**.

```text
We are completing a Software Design Project test with a strict 6-hour total time limit, though we can leave as soon as we are done.

This repository starts empty.

Read the ENTIRE original test specification before modifying any files.

Your objective is to maximise marks while producing a simple, reliable application that can be cloned and run on another machine. Work as quickly and credit-efficiently as possible without sacrificing mandatory requirements or essential verification.

Before writing code, analyse the brief and give me:

## Mandatory/base requirements

- Every requirement needed for the base submission.
- Anything that appears likely to be checked automatically.
- Required technologies, filenames, ports, scripts, database setup, Docker requirements, repository structure and submission rules.

## Optional features

For every optional feature identify:

- marks available
- implementation effort: LOW / MEDIUM / HIGH
- implementation risk: LOW / MEDIUM / HIGH
- estimated standalone effort
- estimated incremental effort if related prerequisite/shared features are already implemented
- which parts of the system it affects
- frontend impact
- backend impact
- database/schema impact
- configuration/infrastructure impact
- dependencies
- whether implementing it makes another feature substantially easier
- what shared infrastructure/code it unlocks for later features

## Feature batching and ranked priority list

Group optional features into sensible batches where features:

- touch the same parts of the codebase
- share implementation work
- are individually low/medium risk
- can be tested together efficiently

For every batch identify:

- included features and total marks
- approximate combined effort and risk
- relevant shared work and dependencies
- likely regression impact
- how implementing the batch changes the cost of later batches

Do NOT group unrelated high-risk features together simply to increase the marks per batch.

Create ONE PROVISIONAL RANKED LIST of optional feature batches (Batch 1, Batch 2, Batch 3, etc.) in recommended implementation order.

Rank primarily by marks gained relative to incremental effort and regression risk, while accounting for prerequisites and useful shared work. Prefer several cheap, related marks over a single risky feature when that is a better return.

Clearly identify which batches may not be worth implementing.

This ranked list will be reused later. Do NOT plan to fully reanalyse every remaining feature after each batch. We will finalise the list once after the base is working, then work down it. Only briefly reconsider the order if an important dependency, unexpected complexity, or major regression risk changes the economics.

## Architecture

Recommend the simplest architecture that satisfies the brief.

Prefer:
- simple conventional technologies
- few dependencies
- minimal configuration
- easy debugging
- easy fresh-clone setup
- watch/hot-reload development commands where appropriate

Avoid:
- unnecessary frameworks or services
- overengineering and premature abstractions
- anything that adds complexity without earning marks

## Implementation strategy

Create an implementation order that:

1. gets the mandatory/base application working end-to-end as early as possible
2. protects that working submission before optional features
3. implements optional marks in the ranked feature batches
4. leaves sufficient time for final verification, a fresh-clone check, and final submission

## Efficiency and verification

- Be fast and economical with tool calls and context use; give concise, decision-useful reports.
- Do not compromise meaningful verification.
- Prefer targeted checks during development and broader regression checks at batch boundaries.
- Minimise unnecessary terminal waiting and duplicate server starts.
- Reuse running servers, prefer hot reload, and restart only when genuinely required.
- Prefer short readiness/health checks over fixed sleep delays.
- Diagnose blocked or unusually slow commands instead of waiting indefinitely.
- Do not repeatedly revisit decisions that are already settled.

Do NOT impose rigid per-stage time budgets. The total exam limit is 6 hours, so prioritise reliable marks and speed throughout.

If a requirement is ambiguous or risky, point it out succinctly.

Do NOT modify files yet.

STOP after presenting the mandatory requirements, simple architecture, and ranked optional-batch plan. Wait for my review.
```

---

## 2. Build the Working Base

**Use once:** After approving Step 1. **Goal:** Fully working mandatory app, accurate README, running servers, short smoke test. **No Git until you approve the smoke test.**

```text
Implement ONLY the mandatory/base requirements from the original specification, following our agreed simple architecture.

Do not implement optional features yet.

The goal is a complete, working end-to-end baseline as quickly and safely as possible.

## Implementation rules

- Follow the agreed architecture and prioritise the requirements that earn mandatory marks.
- Avoid unnecessary dependencies, unrelated refactoring and non-required features.
- Use proper configuration instead of machine-specific paths.
- Keep fresh-clone reproducibility in mind.
- After initial orientation, read ONLY files relevant to the current change unless broader inspection is necessary to diagnose a problem.
- Avoid repeated full-repository analysis, unnecessary explanation and repeated checks that provide no new information.
- Use quick targeted build/test/type-check checks as you work, and verify actual functionality.
- Fix real build/runtime failures with the smallest reasonable changes rather than assuming the app works.

## README and reproducibility (MANDATORY)

Create README.md in the repository as part of this base implementation.

Document:
- prerequisites and dependency installation
- exact setup and start commands for a fresh clone
- required ports and URLs
- environment variables and .env.example where appropriate
- database setup, migrations or seed steps if required
- commands for relevant tests

Keep the README accurate to the implementation. Do not commit secrets, local .env files or machine-specific paths.

## Terminal and server management — YOU handle EVERYTHING

I will NOT run terminal commands or keep frontend, backend or database servers open separately.

You are responsible for dependency installation, ALL services and terminal commands, automated checks, and Git after my approval.

- Start required development processes yourself and leave the app running when you hand control back to me, using persistent terminals or managed background processes where supported.
- Reuse existing running servers; do not launch duplicates.
- Prefer watch/hot reload and avoid unnecessary restarts.
- Restart only when configuration, dependencies, environment, database, or a non-watched process genuinely requires it.
- Prefer short readiness/health checks (e.g. curl) to fixed sleep delays.
- Avoid commands that block indefinitely; diagnose stuck processes promptly.
- If your environment cannot keep the app running after your turn, report this accurately instead of claiming it is running.

Where relevant, verify:
- frontend → backend
- backend → database

## Definition of a working base

Do not stop simply because the files exist. Verify that:

- dependencies install successfully
- applicable builds pass
- the app starts successfully and is accessible
- the mandatory functionality works end-to-end
- there are no obvious runtime failures
- required data persists, where applicable
- the README accurately documents the working setup

Perform as much FAST automated verification as practical, including relevant:
- builds, tests, type checks and linting
- API requests and database checks
- provided automarker or validation checks

Do not repeatedly restart services or run full regression suites after tiny changes. Use targeted checks during implementation and appropriate integrated verification before handing it over.

## Manual smoke-test gate — NO COMMIT OR PUSH YET

When the base is working, keep the application running and give me only:

1. The exact URL(s) to open. The app must ALREADY be running if the environment supports it; do not ask me to start it.
2. The SHORTEST manual smoke test: exactly what to click, enter or do.
3. Exactly what I should expect to see, including what proves the mandatory functionality works.
4. A brief summary of automated checks passed and anything still unverified.

Then STOP and WAIT for my explicit confirmation that I personally tested the base and it PASSED.

CRITICAL:
- Do NOT stage changes for a commit, commit, or push before my approval.
- Passing automated tests is NOT permission to commit or push.
- Do NOT implement optional features yet.
- If I find a problem, diagnose it, make the smallest fix, rerun appropriate checks, and give me an updated smoke test. Continue waiting for approval.

## Git — ONLY after my explicit smoke-test approval

When I say the base smoke test PASSED, you must perform all Git work yourself.

Inspect the changes first and ensure secrets, local .env files and unnecessary generated files are excluded. Then run:

    git add .
    git commit -m "Working base implementation"
    git push

Verify the commit and push really succeeded. If Git or the remote is misconfigured or a command fails, explain the exact blocker without claiming success.

After the successful push (or reporting the blocker), STOP. Do not begin Step 3 or any optional work until I instruct you.
```

---

## 3. Finalise the Feature-Batch Priority List

**Use once:** After the base passes your manual smoke test and has been pushed. **Goal:** A final ranked queue, not another exhaustive planning exercise.

```text
The mandatory/base application is working, has passed my manual smoke test, and has been committed and pushed.

Do NOT modify any files yet.

Use the PROVISIONAL ranked optional-feature-batch list from Step 1. Do NOT start the analysis again from scratch and do NOT reread unrelated source files.

Briefly compare that list with the CURRENT working base and check only what might have changed:

- whether any planned batch is already partially implemented
- whether shared infrastructure in the base makes a batch cheaper
- prerequisite or dependency changes
- unexpected regression or implementation risk
- whether any batch is clearly poor value for its marks

Produce ONE FINAL, ORDERED FEATURE-BATCH QUEUE (Batch 1, Batch 2, etc.).

For each batch give a concise summary:
- features and total marks
- estimated incremental effort and risk
- important dependencies/shared work
- why it has that position in the queue

Prioritise high marks with low/medium incremental effort and risk. Account for features that unlock cheaper subsequent batches. Flag batches that are probably not worth doing.

Do NOT implement anything yet.

STOP after the final ranked list and wait for me to approve the order.

IMPORTANT FOR LATER: After the queue is approved, do NOT repeat this full Step 3 after every batch. Work down the list. Only make a SHORT reassessment if an important dependency, unexpected implementation difficulty, or major regression risk changes priorities.
```

---

## 4. Implement the First Selected Feature Batch

**Use once:** After you approve Step 3. This full prompt establishes the implementation, smoke-test and Git rules for **all future batches**.

```text
Implement ONLY the NEXT HIGHEST-RANKED VIABLE FEATURE BATCH from our approved final queue, starting with Batch 1.

Use the exact feature requirements from the original test specification and the approved batch plan already in this conversation. I should NOT need to paste the requirements again.

Preserving the current working application is more important than architectural improvements. We are under a 6-hour overall time limit, so work as fast and credit-efficiently as possible without sacrificing meaningful verification.

## Before making changes

Briefly identify:
- the existing parts of the app this batch will touch
- shared implementation between its features
- the most likely regression risk

Do not reanalyse unrelated optional features or repeat the full Step 3 comparison.

## Implementation rules

- Implement only this batch and meet its exact requirements.
- Preserve all previously working functionality.
- Follow the existing architecture.
- Make the smallest reasonable changes.
- Do not perform unrelated refactoring or redesign working components.
- Do not replace libraries/frameworks or add dependencies unless needed.
- After identifying the relevant area, read only the relevant files unless broader inspection is necessary to diagnose an issue.
- Avoid repeated repository-wide analysis and unnecessary lengthy explanations.
- Update README.md if this batch changes setup, ports, environment variables, database steps, or documented user functionality.
- If a low-value optional feature becomes unexpectedly difficult, stop and briefly compare its remaining marks against the time, credit cost and regression risk; recommend skipping it if it is no longer worthwhile. Do not silently abandon requirements or jeopardise the working app.

## Terminal and server management — YOU handle EVERYTHING

I will NOT manually start, stop or manage terminals or servers.

- Manage all required frontend/backend/database services and commands yourself.
- Reuse running dev servers wherever possible; do not start duplicates.
- Use hot reload/watch mode where available and restart only when necessary.
- Use quick health/readiness checks instead of fixed waits.
- Diagnose stuck commands rather than waiting indefinitely.
- Keep the application running for my smoke test if your environment supports it; report any limitation accurately.

## Automated verification

During implementation, use quick TARGETED tests and checks rather than repeatedly running an expensive full suite.

At the end of the batch:
1. Run relevant builds, tests and type checks.
2. Verify each feature in the batch.
3. Check important previously working behaviours for regressions.
4. Fix regressions introduced by this batch using minimal changes.
5. Run relevant API, database or automarker checks where applicable.

Do not skip essential verification merely to save credits.

## Manual smoke-test gate — NO COMMIT OR PUSH YET

When this batch works, keep the app running and give me:

1. The exact URL(s) to open; the app should ALREADY be running if supported.
2. The SHORTEST manual smoke test covering EACH new feature: exactly what to click, enter or do.
3. The expected visible result for each test.
4. One or two important existing behaviours to recheck, and their expected results.
5. Anything unverified or any environment limitation.

Then STOP and WAIT for my explicit confirmation that the ENTIRE batch PASSED my manual smoke test.

CRITICAL:
- Do NOT stage changes for a commit, commit or push before I approve.
- Do NOT treat automated test success as manual approval.
- Do NOT start the next batch automatically.
- If I find a problem, make the smallest appropriate fix, run focused checks and give me an updated smoke test. Wait for approval again.

## Git — ONLY after my explicit smoke-test approval

When I explicitly say the entire batch PASSED, handle Git yourself.

Inspect the changes and exclude secrets, local .env files and unnecessary generated files. Then run:

    git add .
    git commit -m "Add <feature batch>"
    git push

Replace <feature batch> with a concise accurate batch description. Verify the commit and push succeeded. If they fail, report the exact blocker.

After pushing, STOP. Do not automatically start the next batch.

## Future batches

Keep following these same implementation, verification, running-server, manual approval and Git rules for every later batch. Once the current batch is approved and pushed, I will simply say "Implement the next batch". Select the next highest-ranked viable batch from the existing approved queue; do not rerun Step 3 unless a major change justifies a brief reassessment.
```

### Later batches — short repeat prompt

**Use after the previous batch passed your manual test and Qoder successfully pushed it.** You do **not** need to paste the full Step 4 again.

```text
Implement the next highest-ranked viable feature batch from our approved queue.

Follow ALL the implementation, terminal/server, verification, smoke-test and Git approval rules established in Step 4. Do not rerun the full Step 3 analysis or reread unrelated files. Use the smallest safe changes, preserve the working app and minimise unnecessary time/credit usage.

Keep the app running and give me its URL and the shortest manual smoke test with expected results. STOP before any commit or push and wait until I explicitly confirm the smoke test PASSED.

Only after my approval, commit and push the completed batch yourself, then STOP. Do not start another batch automatically.
```

**Ultra-short alternative (same chat, where Step 4 rules remain in context):** `Implement the next batch.`

---

## 5. Final Audit and Submission Check

**Use when:** You are finished with optional batches or the remaining time makes further optional work unwise. **Goal:** Freeze features and secure marks already earned.

```text
Stop implementing new features.

Re-read the ORIGINAL test specification from beginning to end. Audit the CURRENT repository against every requirement.

For each requirement report one of:

PASS — implemented and verified
FAIL — implemented but currently incorrect
MISSING — not implemented
NOT VERIFIED — appears implemented but has not actually been tested

Pay special attention to anything likely to be automatically marked.

## Submission and fresh-clone audit

Assume the marker will:
1. clone the repository onto another machine
2. follow README.md
3. run the documented commands
4. test the application

Check for:
- build and startup failures
- missing dependencies or dependencies installed only globally
- missing lock files
- wrong ports and frontend/backend connectivity problems
- database connectivity and missing setup/migrations
- required environment variables and .env.example where appropriate
- hardcoded machine-specific paths or incorrect localhost use
- missing/untracked required files or required files incorrectly ignored
- accidentally committed secrets
- inaccurate or missing README instructions
- broken tests and automarker checks
- Docker networking/build issues, if Docker is required

Run relevant tests, builds, type checks, validation scripts and provided automarker checks. Full verification is appropriate now, but avoid pointless repetition of checks whose results cannot have changed.

Fix ONLY issues affecting:
- mandatory marks
- already implemented features
- startup and runtime correctness
- tests/automarker
- fresh-clone reproducibility
- submission correctness

Do NOT add optional features, perform cosmetic refactoring, redesign the architecture or upgrade dependencies unnecessarily.

You (the agent) must handle all terminal commands, service management, tests and fresh-clone verification. Do not ask me to run terminal commands. If the environment prevents a true isolated fresh-clone check, say so clearly and identify what remains unverified.

If final fixes change the application, leave it running and provide a short manual smoke test for the affected behaviour. STOP and wait for my explicit approval BEFORE committing or pushing those final fixes. Once approved, inspect changes, exclude secrets/unnecessary files, commit with an accurate message, push and confirm success.

Finally give me:
1. a concise PASS / FAIL / MISSING / NOT VERIFIED summary
2. the result of the actual fresh-clone/reproducibility check and anything unverified
3. Git status and confirmation of whether all approved changes were successfully pushed
4. any remaining submission-critical action

After this, treat the codebase as frozen except for critical submission fixes.
```

---

## Tiny Emergency Prompts

These are standalone prompts for common problems. They do **not** override the manual smoke-test approval requirement for Git.

### Qoder is going in circles

```text
Stop changing things. Tell me what definitely works, what definitely fails, and the smallest path back to a stable working submission.
```

### There is an error

```text
Use the actual error output. Diagnose the root cause first, then make the smallest possible fix. Do not refactor unrelated code.
```

### A batch broke something

```text
This worked before the last batch. Find the regression and restore the previous working behaviour without redesigning the app.
```

### A feature/batch is taking too long

```text
We are under time pressure. Re-read the exact requirements and find the simplest valid implementation. If this batch is no longer worth the marks versus risk, tell me to abandon it.
```

### Nearly out of time

```text
We are nearly out of time. Protect already-secured marks. Recommend whether to fix the current issue, abandon it, or move immediately to final submission checks.
```

### Qoder starts overengineering

```text
Do not redesign or refactor. Keep the current architecture and make only the minimum changes needed to satisfy the requirements.
```

### Qoder keeps restarting servers

```text
Minimise server restart overhead. Reuse the already-running development server when possible and rely on hot reload/watch mode. Only restart a service when genuinely required. Avoid repeated kill/sleep/start cycles.
```

### Qoder uses long fixed sleeps

```text
Avoid unnecessary fixed sleep delays. Prefer a short readiness or health check and continue as soon as the service is actually ready.
```

### Terminal command looks stuck

```text
This command appears to be taking too long. Do not wait indefinitely. Determine whether it is a long-running process, blocked command, or genuine build/test task, then use the fastest safe alternative.
```

### Want a quick manual test

```text
Give me the shortest possible smoke test for the ALREADY RUNNING application: what URL to open, exactly what to click/do, and what I should expect to see. Do not ask me to run terminal commands.
```

### Verify before continuing

```text
Stop adding features. Use quick automated checks against the current running application and tell me what definitely works before we continue.
```

### Want the next best batch fast

```text
Which remaining batch gives the best total marks for the least time and regression risk based on the CURRENT codebase? Use our approved ranked queue; do not repeat the full Step 3 analysis.
```

### Risky feature is tempting

```text
Compare this feature against the remaining low-risk features by marks, effort, dependencies, and regression risk. Tell me whether it is actually worth attempting now.
```

### About to submit

```text
Freeze functionality. No new features or refactoring. Only fix issues that could lose marks or cause the project to fail after a fresh clone.
```

### Qoder is using too much time or credit

```text
Prioritise speed and credit efficiency. Stop unnecessary analysis, repeated file reading, excessive testing and unrelated changes. Focus on the smallest reliable implementation that earns the required marks. Keep essential verification and the smoke-test approval gate.
```

### Next batch may not be worth doing

```text
Briefly reassess only the next batch against remaining time, incremental effort, regression risk and available marks. If it is no longer worthwhile, recommend skipping it and taking the next viable batch or moving to the final audit. Do not rerun the entire feature analysis.
```

---

**Core rule:** Plan the optional queue once, implement from the top, personally smoke-test every milestone, and let Qoder commit/push **only after approval**. Keep the system simple, running, and reproducible.
