You are an expert at understanding codebases and writing comprehensive instructions for code agents (llms that write code in an agentic way).

Your task is to enhance the system prompt for the agent, which is in `CLAUDE.md`.

Follow the steps to prepare the project for the code agent.

# 1. Prerequisites
First, check if CLAUDE.md exists in the project root. If it doesn't exist, stop immediately and inform the user: "CLAUDE.md not found. Please run /init first to initialize the project configuration."
If the file exists, read it to get an overview of the project.

# 2. Validation Strategy
Determine the validation strategy for the project. The Code Agent should work iteratively, so the validation strategy should be quick to run.
Sort the validation strategies from quickest to most comprehensive.

If there is no tooling for validation, you should make an educated suggestion and add them to the project, AFTER asking the user for confirmation or input. Think about the solution first.

Hints:
- NextJs build command automatically runs lint
- Don't write bullshit tests like only asserting visibility of a component. Write tests from a user perspective. Like interacting with elements.

# 3. Workflow
Add a new section to CLAUDE.md titled "## Workflow".
It should describe an iterative workflow based on the validation strategy you selected.
Usually the code agent will divide instructions into smaller chunks and then work on them in order. It should run quick validation steps after each chunk. And then run the full validation suite after the whole task is done.

Example workflow for a web app:
1. Planning
2. Implementation of small chunk
3. Validate small chunk (repeat for all chunks)
   1. Run lint
   2. If the functionality is not covered by tests, write tests
   3. Run relevant tests
4. Finished complete task
   1. Run full validation suite

Highlight the importance of tests, because the agent likes to avoid them otherwise.

STOP HERE. Ask the user for confirmation or input and ONLY THEN update CLAUDE.md