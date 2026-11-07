# AI Skills Repository

This repository contains custom skills for Antigravity agents to toggle between different execution modes:

- **[read-only](skills/read-only/SKILL.md)**: Configures the agent to run in a safe, read-only mode where modifications to code and the environment are prohibited.
- **[action](skills/action/SKILL.md)**: Configures the agent to run in action/write mode, allowing files to be edited and system modifying commands to be executed.
- **[context-usage](skills/context-usage/SKILL.md)**: Instruction set to analyze and report the percentage of the context window currently used inside the active chat window/conversation.
- **[plan-view](skills/plan-view/SKILL.md)**: Presents or generates an interactive implementation plan artifact that explains concepts in a simple, concise, easy-to-understand way and mostly uses simple, low-verbosity diagrams to explain workflows and architecture.
- **[generate-video](skills/generate-video/SKILL.md)**: Instruction set to generate animated videos from comic images using the Google Veo / Gemini API.
- **[video-content-creator](skills/video-content-creator/SKILL.md)**: Orchestrates the creation of an AI video content bundle, including a structured outline, voiceover script, image/visual prompts, metadata, and an optional functional codebase demo.
