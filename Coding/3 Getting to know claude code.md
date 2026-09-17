# Managing Your Claude Code Session
- **Open and chat**: Launch the agent in your terminal and type messages like any chat app
- **Multi-line input**: Use Shift+Enter to write complex, multi-line prompts
	- ```/terminal-setup``` to enable
- **Check limits**: Run `/usage` to see your remaining allowance
- **Inspect context**: Run `/context` to visualize what's filling your context window
- **Reset**: Run `/clear` to start with a fresh context
- **Interrupt**: Press Escape to stop the agent mid-run, then redirect it
# Prompting in the Terminal
- **Reference files** using `@` to pull specific files into [context](https://www.aihero.dev/ai-coding-dictionary/context)
- **Stash prompts** with `Ctrl+S` to save half-written prompts and rehydrate them later
- **Paste images** from your clipboard to include screenshots and visuals in your prompts

## Visualising Your Context Window
```/context```
- **[System prompt](https://www.aihero.dev/ai-coding-dictionary/system-prompt) tokens**: Instructions given to the agent
- **Skills tokens**: Custom [skills](https://www.aihero.dev/ai-coding-dictionary/skill) you've added
- **Message tokens**: Conversation history
- **Context window size**: The total [token](https://www.aihero.dev/ai-coding-dictionary/token) capacity (for example, Claude 3.5 Opus has 1 million tokens)

## Time Travelling

| Option                                         | What It Does                                                           |
| ---------------------------------------------- | ---------------------------------------------------------------------- |
| **Restore the code and the conversation**      | Rewind your entire session to the point before this code edit was made |
| **Restore the conversation but keep the code** | Keep your current code state while reverting the conversation          |
| **Restore the code but keep the conversation** | Keep your conversation history while reverting the code                |
