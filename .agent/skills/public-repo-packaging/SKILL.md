---
name: public-repo-packaging
description: >-
  Safe packaging checklist before publishing this repo or committing: git status,
  denylist vs allowlist, confirm file list. Use before any public push or release commit.
---

# Public repo packaging

## When to use

- Before **publishing** the repository or pushing to a **public** remote.
- Before any commit intended for the **public** branch when data/model leakage must be avoided.

## Checklist

1. Run `git status` and review **staged** and **unstaged** paths.
2. Verify nothing matches the **denylist** (see below). If it does, unstage (`git restore --staged <path>`) and fix `.gitignore` if needed.
3. Confirm only **allowlist** categories are staged for a public commit.
4. Re-read the final list of files that will be included (`git diff --cached --name-only`) and confirm it is acceptable.

## Allowlist (typical public-safe artifacts)

- `*.ipynb`
- `evaluate_model.py` (if present)
- `README.md`
- `*evaluation*.md`, `*vyhodnoceni*.md`
- `.gitignore`
- `.cursor/rules/*`
- `.agent/skills/public-repo-packaging/SKILL.md`

## Denylist

Same as `.gitignore` in this project, including at minimum:

- `*.csv`, `*.zip`, `*.gz`, `*.7z`, `*.parquet`, `*.feather`
- `*.pkl`, `*.joblib`, `*.onnx`, `*.pt`, `*.h5`
- `*.db`, `*.sqlite`
- `.env`, `*.key`, `*.pem`, `*.secrets*`
- Directories: `data/`, `datasets/`, `raw/`, `exports/`, `venv/`, `.venv/`, `__pycache__/`
