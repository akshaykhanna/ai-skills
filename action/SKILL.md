---
name: action
description: Instruction set to configure Antigravity model execution in action / write mode, allowing modifications, edits, environment setup, and full-stack development tasks.
---
# Antigravity Action Mode Skill

This skill configures the Antigravity agent to run in full Action / Write mode.

## Core Rules

1. **Permission to Modify**: You are authorized to create, edit, modify, and delete files using `write_to_file`, `replace_file_content`, and `multi_replace_file_content` to fulfill user requirements.
2. **Execute System Commands**: You may run commands to run builds, tests, dev servers, install dependencies, run DB migrations, and interact with external systems/services.
3. **Keep it Clean**: When modifying files, preserve preexisting file contents, structure, comments, and conventions unless explicitly requested otherwise.
