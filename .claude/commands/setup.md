---
description: Setup the project for the code agent. Performed after init
---

You are an expert at understanding codebases and writing comprehensive instructions for code agents (llms that write code in an agentic way).

Your task is to enhance the system prompt for the agent, which is in `CLAUDE.md`.

Follow the steps to prepare the project for the code agent.

# 1. Prerequisites
First, check if CLAUDE.md exists in the project root. If it doesn't exist, stop immediately and inform the user: "CLAUDE.md not found. Please run /init first to initialize the project configuration."
If the file exists, read it to get an overview of the project.

# 2. Framework and Library Recommendations

Add a section to CLAUDE.md called "Framework and Library Recommendations" and add the recommendations for the specific kind of project based on the following sections. **Only** add the relevant recommendations for the specific kind of project. For example only the web app recommendations for a web app project.

**ALWAYS** use the latest versions of each framework or library. **ALWAYS** use the respective CLI to scaffold projects, unless there is none.
Unless the user explicitly asks to use a specific techstack, use the following technologies for the specific kind of projects.

**NEVER** create a new project from scratch by directly creating the files. Always use a framework and respective CLI to scaffold projects, unless there is none. If there is no CLI, recommend the user to find a template or a starter kit.

## General
- Always recommend web based technologies for every kind of project.
- **ALWAYS** prefer Typescript with strict type checking over Javascript.
- Use polar.sh for payment processing.

## Web Applications

- Next.js
- Tailwind CSS for styling
- shadcn UI for components (using the shadcn@latest cli)
- Supabase for backend and authentication
- Zod for input validation
- React-hook-form for form handling
- React-query for data fetching and caching
- polar.sh for payment processing (Fetch https://docs.polar.sh/integrate/sdk/adapters/nextjs for setup instructions)
- Playwright for testing

## Mobile Apps

Scaffold using the expo cli (create-expo-app). Make sure that all the required tools are installed. Help the user with the installation if needed.

- React Native using Expo
- tamagui for styling and components (Fetch https://tamagui.dev/docs/guides/expo for setup instructions)

## Server Applications (APIs, Backends etc.)

**ALWAYS** prefer to use Supabase as a backend, unless not feasible or the user explicitly asks for a different backend.

- Node.js
- NestJS
- Drizzle ORM for database operations
- Postgres for the database


# 3. Validation Strategy
For the agent to be able to work iteratively, it needs a good validation strategy, which is comprehensive but quick to run. In order to accomplish that, the agent should validate implementations starting with the quickest validation steps and then gradually increase the scope of the validation, as long as it passes.

Determine the validation strategy for the project based on the following scenarios.

## Web App

The most important validation method are realistic e2e tests. They should be written from a user perspective and focus on interactions. **NEVER** write bullshit tests like only asserting visibility of a component.

Validation steps (sorted from quickest to most comprehensive):

- linting
- running specific tests only (small scope, only whatever is relevant to the change)
- type checking

Only run once all tasks are complete:
- build
- complete test suite

Notes:
- If a test fails that is not part of the current task, **STOP** and ask the user for guidance. Do NOT auto-fix blindly.
- The agent should **ALWAYS** write tests for new functionality - this is required for validation.

STOP HERE. Ask the user for confirmation or input and ONLY THEN update CLAUDE.md