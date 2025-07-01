You are an AI assistant tasked with executing an already-approved implementation plan.

Before you begin, verify that `CLAUDE.md` includes a `## Validation` section with a *Primary command*. If not, STOP and ask the user to run `/update-claude`.

Your sole objective in this prompt is to implement every unchecked todo item in tasks/todo.md and deliver the finished work.

Workflow for this implementation phase:

1. Read `tasks/todo.md`; if it does not exist (e.g., the plan phase was skipped), create it with the skeleton shown in the plan command, then proceed.

2. Identify all todo items that are still unchecked ("[ ]"). Each item includes a Validation sub-bullet specifying the automatic validation step (e.g., specific e2e test). If a task contains nested acceptance criteria checkboxes, you should check those off individually as you satisfy them.

3. For each unchecked item:
   a. Make the necessary code changes, tests, or documentation updates to satisfy the item, and **run only the task's specified Validation step(s)** until they pass.
   b. Keep changes minimal and focused; avoid unrelated refactors unless strictly required.
   c. After completing the work for that item, update the todo list by:
      - Changing "[ ]" to "[x]"
      - Adding a one-clause note describing what was done

4. After **all** checklist items are complete, run the project's **full validation suite** (e.g., the *Primary command* in `CLAUDE.md`).
   - If the suite fails, stop and ask the user for guidance. Do NOT auto-fix blindly.

5. When all items are complete, append a **Review** section to the todo list that includes:
   - A concise summary of the changes made
   - Any challenges encountered and how you resolved them
   - Suggestions for future improvements

6. Produce a final output that contains:
   - The full, updated tasks/todo.md file
   - A brief confirmation message that implementation is complete and any next steps

Important constraints:
- Do NOT change anything that is not part of the plan. If new work surfaces, add it to the todos in a "optional" section and let the user decide if it should be implemented.
- Follow existing code style, type preferences (prefer "type" over "interface", no "any"), and prettier configuration.
- Be terse but thorough in explanations.
- Before finishing, remove any scratch / debug files that were created during implementation.

Your final output should only include the updated tasks/todo.md file and the confirmation message. Do not include any intermediate steps, code changes, or test results in the final output.