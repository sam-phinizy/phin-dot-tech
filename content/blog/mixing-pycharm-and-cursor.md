---
title: Using PyCharm With Cursor
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
- **Refactoring**: Yes Cursor/VSCode has it. No it's not as good.

That being said, nothing I've tried in PyCharm comes close to the elegance of Cursor's AI-powered code completion and chat/composer mode. I've tried a few other AI services such as Cody or Codeium but haven't found them comparable.

So why choose? I use both!

## Cursor
First thing I did was make Cursor more like PyCharm by using a variety of extensions:

- [Jet Brains Icons](https://marketplace.visualstudio.com/items?itemName=marlongerson.jetbrains-icons) This gives all the files in the Cursor File tree Icons reminiscent of the icons in PyCharm.
- [Shift Shift](https://marketplace.visualstudio.com/items?itemName=ahgood.shift-shift)This is probably the biggest one. It binds double tapping `shift` and `control` to PyCharm-esque commands.
- [Auto Docstring](https://marketplace.visualstudio.com/items?itemName=njpwerner.autodocstring) Lets me get a skeleton of a doc string wicked quickly.

Next I set up a task in Cursor that will open the currently active file in PyCharm and move the cursor to the same line

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

Then I can just hit `cmd+shift+p` and run the task and it will open the file in PyCharm. Note: This requires having PyCharm set up to be runnable by the `pycharm` command in your terminal.

## PyCharm

First to make PyCharm more PyCharm like I install PyCharm.

Then in PyCharm I set up an external tool that will open the current file in Cursor. To do this:
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

## Epilogue

Hopefully this makes it easier for folks who love PyCharm to still be able to leverage Cursor's AI abilities while still keeping the productivity of using a full fledged IDE. And hopefully Jetbrains catches up in the AI market. 