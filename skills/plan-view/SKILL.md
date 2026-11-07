---
name: plan-view
description: Presents or generates an interactive implementation plan artifact that explains concepts in a simple, concise, easy-to-understand way and mostly uses simple, low-verbosity diagrams to explain workflows and architecture.
---
# Plan-View Skill

Use this skill when the user asks to view, present, or render a Markdown file or implementation plan as an interactive plan artifact, or when invoking `plan-view <path/to/file.md>`.

## Instructions

1. **Identify or Create the Plan**: Extract the Markdown file path provided by the user in the prompt. If the user is asking to generate a new plan with `plan-view`, draft it directly; if viewing an existing file and no path is provided, ask the user for the `.md` file path.

2. **Read the Content**: If an existing `.md` file is specified, read it from the workspace. If a GitHub URL or remote reference is provided, fetch or clone the relevant content first.

3. **Explain Things in a Simple, Easy-to-Understand & Concise Way**: When authoring or updating a plan for `plan-view`:
   - Break down technical concepts, design choices, and workflows into plain, easy-to-understand language.
   - Keep all sections short, direct, and concise using brief bullet points instead of long paragraphs or dense jargon.
   - Highlight only the core problem, key goals, affected files, and clear step-by-step changes.

4. **Mostly Use Simple, Less Verbose Diagrams to Explain Things**:
   - Default to using simple diagrams (e.g., Mermaid flowcharts or sequence diagrams) to visually explain architecture, request/data flows, and component interactions instead of writing long text explanations.
   - Keep every diagram small, clean, and low-verbosity: use a minimal number of nodes (typically 3–6) and short, 2–4 word labels.
   - Never cram long sentences, file paths, method signatures, or code details into diagram nodes or edge labels.

5. **Include Verified Links & Citations for Authenticity**:
   - Wherever needed, ground your suggestions, root-cause explanations, and architectural comparisons with accurate, clickable links and citations (e.g., exact source files and line ranges, Code Search links, CLs, bugs, or reference docs) to demonstrate authenticity.
   - Always verify file paths, line numbers, and IDs before linking—never guess or invent citations.
   - For GitHub repositories, link to the actual file URLs (e.g., `https://github.com/owner/repo/blob/branch/path/to/file#L10-L20`).
   - For local workspaces, use `file:///` links with line ranges (e.g., `[filename](file:///path/to/file#L10-L20)`).

6. **Stage as Interactive Artifact**: Write/stage the Markdown file content as an Artifact in the session artifacts directory (`<appDataDir>/brain/<conversation-id>/...`) using `write_file` with:
   - **ArtifactMetadata**:
     - `UserFacing`: true
     - `RequestFeedback`: true
     - `Summary`: "Interactive Implementation Plan view for [filename]"

7. **Feedback Loop**: When the user submits inline comments or general feedback in the viewer, apply the requested modifications back to the original file in the workspace and update the artifact.

## Source Compatibility

This skill works with plans from any source:
- **Local files**: Workspace `.md` files read directly.
- **GitHub**: Plans referencing GitHub repos — include proper GitHub links to files, PRs, issues, and commits.
- **Other VCS / platforms**: Adapt link formats to the relevant platform (GitLab, Bitbucket, Azure DevOps, etc.).
- **Generated plans**: New plans drafted from scratch based on user requirements.

