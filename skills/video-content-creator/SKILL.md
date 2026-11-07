---
name: video-content-creator
description: Orchestrates the creation of an AI video content bundle, including a structured outline, voiceover script, image/visual prompts, metadata, and an optional functional codebase demo.
---
# Video Content Creator Skill

Use this skill to systematically produce complete video tutorial assets (scripts, outlines, prompts, metadata, and optional demos) using the generator pipeline in the user's active workspace.

## Expected Inputs
- **`topic`** (Required): The primary subject of the video tutorial.
- **`brainstorming_notes`** (Required): Raw concepts, code snippets, or key points to include in the video.
- **`audience`** (Optional): Target audience (default: "General Developers").
- **`platform`** (Optional): Target platform, e.g., "YouTube" or "Udemy" (default: "YouTube").
- **`style_tone`** (Optional): Voice and tone instructions (default: "Simple, concise, using real-world layman analogies").
- **`generate_demo`** (Optional): Boolean flag indicating whether to generate a functional codebase demo.
- **`demos_repo_path`** (Optional): Destination folder/repository path for the generated demo.

## Execution Workflow

1. **Verify Python Environment**: Ensure dependencies in [requirements.txt](file:///c:/Users/aksha/prj/ai-video-content-creator/requirements.txt) are installed in the workspace directory.
2. **Obtain GEMINI_API_KEY**: Ensure the `GEMINI_API_KEY` environment variable is available.
3. **Execute Content Pipeline**: Run the generator script using the input parameters.
   - Run the command:
     ```bash
     python src/main.py --topic "<topic>" --audience "<audience>" --platform "<platform>" --style "<style_tone>" --notes "<brainstorming_notes>"
     ```
   - If a code demo is requested, append the `--demo` flag and optionally `--demos-dir "<demos_repo_path>"`.
4. **Locate Outputs**: 
   - The generated content bundle is saved as a markdown file under `output/<topic-slug>/<topic-slug>.md`.
   - Any generated asset files (like slide/concept images) are placed in the same `output/<topic-slug>/` directory.
   - If requested, the generated codebase demo is stored under the specified `--demos-dir` path (defaults to the `../my-demos` repository directory).
