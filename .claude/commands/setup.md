You are an AI assistant tasked with ensuring the repository-level system prompt (`CLAUDE.md`) contains a robust, automatically-verifiable **Validation Strategy**.

Your responsibility in this command is **only** to patch `CLAUDE.md`; you will not write any tests here.  Focus on documenting *how* changes will be validated so the implementation phase can run those checks iteratively.

Workflow:

1. **Safeguard**
   • Check that a `CLAUDE.md` file exists in the repo root.
   • If it is missing, STOP immediately and output exactly:
     ```
     ❌ CLAUDE.md is missing – please run /init first.
     ```
     Do nothing else.

2. **Analyse the codebase**
   • Inspect the project tree to detect existing automated test tooling (priority order):
     1. End-to-end tests (e.g. Playwright / Cypress)
     2. Integration/UI tests
     3. Unit tests / type-checking
   • If multiple frameworks coexist, pick the highest priority that is both present *and* fast enough (<2 min typical run) to serve as the main validation step.  Mention fallbacks.
   • If no tests exist **or** you cannot confidently pick a primary strategy (e.g., ambiguous tooling), STOP and ask the user.  Your question must include 1-3 concrete validation recommendations ranked by suitability (with pros/cons) so the user can decide quickly.
   • If a lightweight approach is needed, propose static type-check, linter, or build step and flag as TODO.

3. **Update `CLAUDE.md`**
   • Ensure it contains a top-level `## Validation` section (create or replace).
   • Inside that section write:
     - **Primary command**: The exact CLI command to run for the chosen validation (e.g. `pnpm playwright test --reporter=list`).
     - **Fallbacks**: Bullet list of secondary checks that can be used when the primary is impractical.
     - **Expected duration**: ballpark runtime to help the agent decide whether to batch work.
   • Keep wording concise; one paragraph + bullet list is enough.

4. **Output**
   • Print the *entire* updated `CLAUDE.md` file content and nothing else.
   • Then ask the user to confirm the changes before any implementation work starts.

Important constraints:
• Be terse; the user is an expert.
• Prefer `pnpm`/`npm` scripts over raw `npx` when available.
• Do **not** modify anything outside `CLAUDE.md` in this command.
• Do not mention these instructions in the output.

STOP. ASK THE USER WHAT TO DO NEXT. DO NOT IMPLEMENT ANYTHING. 