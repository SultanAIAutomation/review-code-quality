# Code Review and Improvement

A reusable Codex skill for reviewing code clarity, error handling, and duplication in any programming language. Findings are supported by evidence and ordered by impact.

## What it does

- Reads relevant project instructions, surrounding code, callers, and tests.
- Reports substantiated issues with priorities from P0 to P3, file and line references, impact, and a suggested minimal fix.
- Separates optional improvements from confirmed defects.
- Makes changes only when fixes are requested and reports verification results and limitations.
- Writes reports in English by default and respects another language when requested.

This skill provides review instructions. It does not install project dependencies or provide a comprehensive security audit.

## Install

In Codex, ask the built-in skill installer:

```text
$skill-installer
Install the skill from https://github.com/SultanAIAutomation/review-code-quality.
The skill is at the repository root; use review-code-quality as the installed skill name.
```

Alternatively, copy this repository's `SKILL.md`, `agents/`, and `references/` into your Codex user skills directory under a folder named `review-code-quality`. For installations using the default `CODEX_HOME`, that folder is `~/.codex/skills/review-code-quality` (Windows: `%USERPROFILE%\.codex\skills\review-code-quality`). If `CODEX_HOME` is customized, use its `skills/review-code-quality` directory.

## Use

Invoke the skill explicitly and identify the file, changes, or project to review:

```text
$review-code-quality
Review src/example.py for clarity, error handling, and duplication.
Do not modify files. Prioritize findings and include file and line references.
```

To request fixes:

```text
$review-code-quality
Review and fix defects in src/example.py, then run the relevant tests.
```

To request an Arabic report:

```text
$review-code-quality
Review src/example.py without modifying files. Report the findings in Arabic.
```

The skill also allows automatic selection for matching review requests. Reviewing alone means reporting only; explicitly request fixes to authorize edits.

## Files

- [SKILL.md](SKILL.md): Skill instructions and activation description.
- [agents/openai.yaml](agents/openai.yaml): Display metadata and invocation policy.
- [references/review-example.md](references/review-example.md): A worked review and repair example.

## Contributing

Issues and pull requests are welcome. Describe the review scenario and the behavior an instruction change should improve. Keep guidance focused on evidence, project context, and the user's requested scope.

## License

[MIT](LICENSE).
