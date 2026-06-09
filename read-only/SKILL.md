---
name: read-only
description: Instruction set to restrict Antigravity model execution to read-only capabilities, prohibiting writing files, executing modifying terminal commands, or making state mutations.
---
# Antigravity Read-Only Skill

This skill enforces a strict read-only execution mode on the Antigravity agent.

## Core Rules

1. **No Writes or Edits**: Do not call `write_to_file`, `replace_file_content`, or `multi_replace_file_content` to create or modify code, scripts, configs, or project files.
2. **Safe Terminal Commands**: You may run informational terminal commands (e.g., viewing logs, check status, check configurations, git diff/status). Never run commands that install packages, compile/build code, start servers, or write to disk.
3. **No Project State Mutation**: Do not alter external settings, configurations, databases, or systems.
4. **Use Read Tools**: Eagerly use reading tools such as `view_file`, `list_dir`, `grep_search`, `read_url_content` to inspect files and extract information.
