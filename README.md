# How to Create a Claude Code and Gemini CLI Collaboration
Original: https://www.leveragesoftware.group/blog/claude-code-and-gemini-cli-collaboration/


Claude Code is excellent. Gemini CLI is also excellent. Know what’s better? Claude Code and Gemini collaborating on a problem.

Since Claude Code custom commands was released, I’ve gone crazy creating little helpers. And I think this was the best one I’ve done.

```bash
I want you to collaborate with the Gemini AI on the task defined in the `<task></task>` element below. If the tag is empty, the first thing you should do is ask me what the task is.

## Calling Gemini

Use the command line interface with the `-p` flag and Gemini will return it's response to you, eg `gemini -p "YOUR PROMPT"`

Gemini will have no context, so you will need to provide it everything it needs to know about the problem. If you want it to know about files, give it the full path to the file instead of the file contents. Same for directories.

## Collaboration

### Step 1
- You should use subagents to:
    - create your initial output for this task
    - ask Gemini for its initial output for this task

### Step 2
- You should then integrate Gemini's answer into your own
    - Look at Gemini's response for anything that you may have missed

### Step 3
- Tell Gemini the task and context again, but this time ask it to critique your response, passing it your response
- Integrate Gemini's suggestions into your own response

<task>$ARGUMENTS</task>
```

I made this a user command so it’s available in every project. You can do that by creating the file ~/.claude/commands/gemini.md and pasting the previous markdown into that file.

If you only want it for a specific project, you can add it to that projects ./.claude/commands/gemini.md.

DON’T FORGET to restart your Claude Code instance (/quit) so it will pick up the new command.

Then just call it like this:

/gemini pull github issue #1234 including comments and create a plan in ./1234.md to implement the issue

/gemini pull github PR #1235 and do a thorough code review

That’s it!
