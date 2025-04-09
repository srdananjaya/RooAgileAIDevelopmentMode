# Roo-Code Custom Modes Configuration for Agile AI Development (`.roomodes`)

## Introduction

This `.roomodes` file contains custom mode configurations for the [Roo-Code](https://github.com/RooVetGit/Roo-Code) extension in Visual Studio Code. This configuration is specifically designed to implement and automate the **Agile AI-driven development** workflow by providing a suite of AI "agents" with specific roles and tasks, as well as orchestration modes to manage the workflow.

When this file is placed in your project's root directory, Roo-Code will load these modes, allowing you or another AI (via orchestration) to leverage these specialized agents within the software development lifecycle.

## Purpose of This Configuration

The main goals of this custom mode set are to:

1.  **Simulate an Agile AI Team:** Provide separate AI agents for each key role in the Agile process (Business Analyst, Project Manager, Architect, Product Owner, Scrum Master, Developer).
2.  **Automate Workflow:** Offer mechanisms (via the `boomerang` or `agileaiorchestrator` modes) to manage the flow of tasks and data between roles automatically or semi-automatically.
3.  **Enhance Consistency & Efficiency:** Ensure specific tasks like requirements analysis, architecture design, backlog creation, and code implementation are handled by AI specifically instructed for those roles.
4.  **Project-Specific AI Behavior Adaptation:** Configure AI behavior specifically for the needs of this project.

## File Location

Ensure this `.roomodes` file is placed in the **root directory** of your project.

## Defined Modes Overview

This file defines the following custom modes:

1.  **`boomerang` (Flexible Orchestrator):**
    * Acts as a strategic workflow orchestrator.
    * Designed to break down complex tasks into sub-tasks and delegate them to other specialized modes (`agile...` or others) using the `new_task` tool.
    * Manages the workflow based on results that "boomerang" back from sub-tasks.
    * Has limited tool access (read files, edit Markdown) as its focus is on delegation.

2.  **`agileba` (Agile Business Analyst):**
    * Focuses on clarifying initial ideas, defining users, value propositions, and MVP features.
    * Main output: Initial requirements document (e.g., `requirements.md`).
    * Tool access limited to reading/writing Markdown files.

3.  **`agilepm` (Agile Project Manager):**
    * Takes BA's output, performs (simulated) research, details features, defines non-functional requirements, and creates the Product Requirements Document (PRD).
    * Main output: PRD (e.g., `prd.md`).
    * Has browser access for simulated research.

4.  **`agilearchitect` (Agile Architect):**
    * Analyzes the PRD, designs system architecture, selects the technology stack, and defines main components.
    * Main output: Architecture Design Document (e.g., `architecture.md`).
    * Tool access limited to reading/writing Markdown files.

5.  **`agilepo` (Agile Product Owner):**
    * Takes the PRD and Architecture Design to create a detailed, prioritized, and sequenced Product Backlog.
    * Main output: Product Backlog (e.g., `backlog.md`).
    * Tool access limited to reading/writing Markdown files.

6.  **`agilescrummaster` (Agile Scrum Master):**
    * Takes prioritized items from the Backlog, breaks them down if needed, and defines clear Acceptance Criteria (AC) for the Developer Agent.
    * Main output: Sprint-ready User Story (e.g., `story-XXX.md`).
    * Tool access limited to reading/writing Markdown files.

7.  **`agiledeveloperagent` (Agile Developer Agent):**
    * Takes a detailed User Story from the Scrum Master and implements it by writing code, following the defined architecture and standards, and writing unit tests.
    * Has full access to file read/write and command execution (`command`) tools.

8.  **`agileaiorchestrator` (Fixed Sequence Orchestrator):**
    * Acts as a specialized orchestrator designed to run a *fixed sequence* of the Agile AI workflow: BA -> PM -> Arch -> PO -> SM -> Dev (for the first backlog item).
    * Explicitly instructed to delegate tasks to each mode sequentially using `new_task` and manage passing output file paths between steps.
    * Only has file read access (as it just needs to read output paths from sub-tasks).

## How to Use These Modes

There are several ways to utilize these modes:

1.  **Manual Workflow:**
    * You manually select the appropriate mode for each stage.
    * Start with `agileba` and provide your initial idea.
    * Once `agileba` produces its output (e.g., `requirements.md`), copy the file path or content.
    * Switch to the `agilepm` mode and provide the output from `agileba` as input.
    * Continue this process manually through `agilearchitect`, `agilepo`, `agilescrummaster`, down to `agiledeveloperagent`.
    * This method gives you full control but requires manual intervention at each step.

2.  **Orchestrated Workflow (Option A - Flexible with `boomerang`):**
    * Start with the `boomerang` mode.
    * Provide an initial prompt describing the complex task or project you want to accomplish.
    * The `boomerang` mode (based on its instructions) should attempt to break the task into sub-tasks and delegate them to the most appropriate `agile...` modes using `new_task`.
    * You will need to monitor the process and potentially provide additional guidance to `boomerang` if needed.

3.  **Orchestrated Workflow (Option B - Fixed Sequence with `agileaiorchestrator`):**
    * Start with the `agileaiorchestrator` mode.
    * Provide an initial prompt containing your project idea or problem statement.
    * This mode *should* automatically execute the entire sequence BA -> PM -> ... -> Developer Agent (for the first backlog item) by delegating tasks and passing file paths between steps.
    * This method is the most automated for the predefined path but offers less flexibility if you want to deviate from the sequence.

## File Format Notes

* This file uses JSON format.
* The main structure is an object with a `customModes` key, whose value is an array (list) of objects.
* Each object in the array defines one custom mode with properties like `slug`, `name`, `roleDefinition`, `customInstructions`, and `groups` (for tool access).

## Prerequisites

* The Roo-Code extension must be installed in your VS Code.
* Roo-Code must be configured with an AI provider (like OpenAI, Anthropic, Google Gemini, etc.) and a valid API Key.

## Tips

* Start with the Manual Workflow or the `agileaiorchestrator` to understand how each mode works and what output it produces.
* Ensure the initial input you provide (especially to `agileba` or `agileaiorchestrator`) is reasonably clear.
* Remember that Roo-Code uses a BYOK (Bring Your Own Key) model, so using these modes will consume your API tokens, which may incur costs.
* Validate the JSON syntax of this `.roomodes` file before use to prevent errors when Roo-Code tries to load it.

## Troubleshooting

* If the custom modes don't appear in Roo-Code, ensure the `.roomodes` file is in the project's root directory and named correctly.
* Check the JSON syntax carefully for missing/extra commas, mismatched brackets/braces, etc.

---

Hopefully, this English version of the README is helpful for explaining your specific `.roomodes` configuration!
