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
- **Enter rewind mode** - Press `Escape` twice to zoom through all checkpoints
- **Choose what to restore** - Pick whether to rewind code, conversation, or both
- **Persist sessions locally** - Quit and resume without losing progress
- **Multiple resume methods** - Use `--continue`, `/resume`, or the UUID command

## Running Bash Commands
| Goal                                | Approach               | Shortcut                    |
| ----------------------------------- | ---------------------- | --------------------------- |
| Agent needs to see the output       | Use bash mode          | `!` prefix                  |
| Long-running process (dev servers)  | Background with Ctrl-B | After `!` command           |
| Command should be hidden from agent | Suspend the agent      | Ctrl-Z, then `fg` to return |
## Permissions
- To share permissions with team rename `settings.local.json` to `settings.json` 
- Auto mode is easier – agent itself decides if safe
	- The `settings.json` file is still really useful with auto mode. The agent checks `settings.json` first, before running the command through the classifier. This means you can speed up common operations and not have to worry about the classifier by just having something in `settings.json`.
	- Anthropic no longer charges for the classifier token overhead in Auto mode 