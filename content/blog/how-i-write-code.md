---
title: Using PyCharm and Cursor to write code
tags:
  - programming
  - blog
---

So with the advent of fancy AI code editors etc how I develop software has changed. Like most other's I've jumped on the Cursor bandwagon. While I love the quality of the code that Cursor generates I still go back to my old mainstay of PyCharm. It's been hard to get used to the VSCode style itnerface that Cursor has. More specifically these are some of the things that keep bringing me back to PyCharm:

- Navigatign the code base. Cursor has nothing on PyCharm's symbol search and jumping.
- Test running. I'm not sure why but I just can't get the hang of the test runner in Cursor.
- Python Console/Debugging: Somethign about the Cursor debugger and console just doesn't sit right with me.
- The modal/pop-out results for things like Search or Find Usages. Just.. clicks with me better.

That being said nothing I've tried in PyCharm has had the elegance of Cursor's AI powered code completion and chat/composer mode. So I use both!

How I do this is by having a command in each that will open the current file at the cursor position in the other editor. In Cursor I set up a User Task that will open the current file in PyCharm:

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

Put that in your `.vscode/tasks.json` file in project folder. Then you can `command-shit-p` and run the task.

To set up a simiiar a command in PyCharm you can use [External Tools](https://www.jetbrains.com/help/pycharm/configuring-third-party-tools.html). Go to `Tools > External Tools` in PyCharm. Click 