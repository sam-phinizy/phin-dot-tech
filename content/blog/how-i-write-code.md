---
title: Using PyCharm and Cursor to write code
tags:
  - programming
  - blog
publish: true
---

My software development workflow has changed with the rise of AI-powered code editors. Like many others, I've jumped on the Cursor bandwagon. While I love the quality of code that Cursor generates, I still find myself going back to my old mainstay, PyCharm. I've struggled to adapt to Cursor's VSCode-style interface.

Here are the specific features that keep drawing me back to PyCharm:

- **Code base navigation:** Cursor just can't match PyCharm's symbol search and jumping capabilities
- **Test running:** For some reason, I can't quite get comfortable with Cursor's test runner
- **Python Console/Debugging:** The debugger and console in Cursor just don't feel quite right to me
- **Modal/pop-out results:** PyCharm's approach to features like Search or Find Usages just clicks with me better

That being said, nothing I've tried in PyCharm comes close to the elegance of Cursor's AI-powered code completion and chat/composer mode. So why choose? I use both!

My solution is to set up commands in each editor that will open the current file at the cursor position in the other editor. In Cursor, I've set up a User Task that opens the current file in PyCharm:

```json
{
    "version": "2.0.0",
    "tasks": [
        {
            "label": "Open in PyCharm",
            "type": "shell",
            "command": "pycharm --line ${lineNumber} ${file} ",
            "problemMatcher": []
        }
    ]
}
```

Then I can just hit `cmd+shift+p` and run the task and it will open the file in PyCharm.

In PyCharm I set up an external tool that will open the current file in Cursor. To do this:
1. Open Preferences
2. Go to `Tools > External Tools`
3. Click on the `+` sign.
4. You'll see a screen like this:
![[Pasted image 20241118205638.png]]

You can then put these values in the fields:
- Name: `Open in Cursor`
- Program: `cursor`
- Arguments: `--goto $FilePath$:$LineNumber$:$ColumnNumber$`
- Working Directory: `$ProjectFileDir$`

Then you can use the PyCharm 'Find Action' command to run 'Open in Cursor'.  You can have peanut butter in your chocolate!