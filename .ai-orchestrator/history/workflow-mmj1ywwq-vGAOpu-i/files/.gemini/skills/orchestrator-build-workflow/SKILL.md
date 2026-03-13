---
name: orchestrator-build-workflow
description: Implement a feature end-to-end
---

# Workflow Skill

Use the selected learning document, its prompt, and imported sources to draft or extend the pedagogical support end-to-end.

When to use this skill:
- Use it when the request needs the rédiger le support workflow.
- Keep the role chain explicit instead of blending exploration, implementation, review, and testing together.

Execution loop:
- Read the generated context pack and relevant files first.
- Work in short iterations with concrete evidence from files or command output.
- Stop after a role-specific result and hand off if another role is more appropriate.

Preset priorities:
- Validate the plan quickly, then move toward a minimal end-to-end implementation milestone.
- Keep verification focused and explicit before stopping.

Completion criteria:
- Stop once the requested path is implemented and verified with the smallest relevant checks.
- Call out any remaining risks or intentionally deferred work.

Avoid:
- Do not expand scope into unrelated cleanup or architecture changes.
- Do not stop at partial implementation when a narrow end-to-end slice is achievable.

Roles prepared for this workflow:
- architect
- implementer
- reviewer
- tester

Workflow signals:
- Correction_TD2.md
- Logiciel_sur_cours.md
- TD_Substitutions.md

Read .ai-context.md first.
Useful commands: none.
