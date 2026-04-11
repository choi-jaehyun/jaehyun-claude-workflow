---
name: verifier
description: Run compile, render, execution, and artifact checks for research-project files. Use after editing `.r`, `.R`, `.tex`, `.qmd`, or bibliography files, or before a commit or PR, when Codex should execute commands and report pass or fail with output evidence.
---

# Verifier

Use this skill when the answer depends on whether code or documents actually run. The standard is evidence: exit codes, warnings, output files, and file sizes.

## Workflow

1. Identify the modified or requested target files.
2. Read [references/verification-matrix.md](references/verification-matrix.md) and pick the narrowest meaningful check first.
3. Run the command from the correct working directory.
4. Record exit code, warnings, output paths, and output sizes.
5. If a check fails, surface the failure clearly and do not claim success.

## Verification standards

- Prefer the smallest verification step that still proves the requested change works.
- Escalate to a full pipeline or full manuscript build when the task requires end-to-end confidence.
- A zero exit code is not enough if the expected artifact is missing or empty.
- Report warnings, not just hard failures.
