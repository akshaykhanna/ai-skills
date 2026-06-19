---
name: context-usage
description: Instruction set to analyze and report the percentage of the context window currently used inside the active chat window/conversation.
---
# Antigravity Context Usage Skill

This skill provides instructions on how to measure, calculate, and report the current context window usage for the active conversation session.

## Core Rules

1. **Locate Conversation Logs**: Find the `transcript.jsonl` file in the current conversation's logs directory.
   - Path template: `C:\Users\aksha\.gemini\antigravity-ide\brain\<conversation-id>\.system_generated\logs\transcript.jsonl`
   - Use the active `Conversation ID` provided in the conversation metadata.

2. **Retrieve File Metrics**: Check the file size of `transcript.jsonl` using terminal commands or directory listings.
   - Example command: `Get-Item "C:\Users\aksha\.gemini\antigravity-ide\brain\<conversation-id>\.system_generated\logs\transcript.jsonl"`

3. **Estimate Token Usage**:
   - Use a heuristic to convert file size/characters to tokens:
     - 1 Token ≈ 4 characters (including spaces/formatting).
     - Or calculate directly from file size: 1 KB of JSON/text is approximately 250 tokens.
   - Compare this against the model's maximum context limit (e.g., 1,048,576 tokens for standard Gemini Flash, or 2,097,152 tokens for Pro/Flash experimental).

4. **Report Findings**: Present the information to the user in a clean, professional table format, including:
   - **Active Model Name**
   - **Log File Size** (in KB/MB)
   - **Estimated Tokens Used**
   - **Total Context Limit**
   - **Percentage Used** (e.g., `12.5%`)
   - **Remaining Capacity**

5. **Provide Recommendations**: If the context usage is high (e.g., > 70%), warn the user and recommend starting a new chat or summarizing the current work to prevent performance degradation or truncation.
