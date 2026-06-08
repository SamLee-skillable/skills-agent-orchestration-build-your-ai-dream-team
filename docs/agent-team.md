# Agent team

For Mona's Project Pulse dashboard, I will orchestrate this custom team from **GitHub Copilot CLI running in a Codespace**.

| Agent | Target model | Responsibility | Agent definition |
| --- | --- | --- | --- |
| Orchestrator | Claude Opus 4.7 (copilot) | Coordinates the full delivery flow by getting a plan, sequencing phases, delegating scoped work to specialists, and integrating outcomes. | `.github/agents/orchestrator.agent.md` |
| Planner | Claude Opus 4.7 (copilot) | Produces the implementation plan: repository research, ordered steps, file ownership, dependencies, parallel/sequential work, edge cases, and validation expectations. | `.github/agents/planner.agent.md` |
| Designer | Gemini 3.1 Pro (copilot) | Owns dashboard UX/UI quality: accessibility, information hierarchy, interaction flow, responsive layout, and polished Project Pulse visual styling. | `.github/agents/designer.agent.md` |
| Coder | GPT-5.5 (copilot) | Implements code and bug fixes from orchestrated tasks with clear structure, explicit errors, deterministic behavior, and runnable-app support when assigned. | `.github/agents/coder.agent.md` |
