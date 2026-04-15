# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A collection of scheduled Claude agent routines. Each routine is a self-contained directory with two files:

- `prompt.md` — instructions for the Claude agent (the *how*)
- `config.yaml` — user-editable settings that control behavior (the *what*)

Routines are run via `claude --print` or scheduled with `/schedule`.

## Running a routine manually

```bash
claude --print < <routine_name>/prompt.md
```

## Scheduling a routine

```
/schedule daily at 8am <routine_name>
```

## Adding a new routine

1. Create a subdirectory with a short, descriptive name.
2. Add `prompt.md`: start with a one-line role statement, number the steps, reference `config.yaml` for user-configurable settings, specify output format.
3. Add `config.yaml`: sensible defaults for all configurable parameters; define every key the prompt references.
4. Document the routine in `README.md` under the **Routines** section.

## Architecture

Prompts are self-contained instructions — they must tell the agent where to find config (e.g., "read `config.yaml` in this directory") and what to do with it. Config files hold only data; all logic lives in the prompt. Keep these two concerns strictly separated.
