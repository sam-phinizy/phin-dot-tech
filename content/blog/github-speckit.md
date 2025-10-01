---
title: spec-kit
tags:
  - programming
  - blog
  - ai
  - the-slow-inevitable-decline
publish: true
---

Lately I've been playing around with using Github's [SpecKit](https://github.com/github/spec-kit) a framework for getting started with "spec driven development". Which if you're not trying to be fancy is just: writing out what you're going to do before you do it. What SpecKit does is provide dedicated instructions and slash commands to your AI agent of choice to have a dedicated process for generating these docs. It'll generate out a specification, a plan and a set of tasks and then guide the AI through implementation. I've found it's really great at doing this, and for me this is one of the best features of AI: helping to automate some of the toilsome work.

This concept isn't new and there is definitely prior art, some examples include:
- [Kiro](https://kiro.dev/) by AWS - This is yet another Visual Studio Code fork that focuses on building specs and implementing them.
- [Traycer](https://traycer.ai/) - A VSCode extension that helps build out specifications and plans.
- [Task Master](https://www.task-master.dev/) - A CLI tool to act as a project manager. I've not used it and it seems like it does more then just specs but I could be wrong.

What SpecKit does that these tools don't from my limited exposure is it works within your current coding agent/tool. If you're a Claude Code user you're all set, Cursor the same, Copilot it's got you... This is the killer feature for me. With the Cambrian explosion of AI tools and the frankly rather overwhelming pace of new development it's nice that this adapts to the ecosystem you've set up. Personally I prefer Claude Code and have built up a nice little ecosystem of tools/functionality that I use with it. 

# Trying it out

## Step One - Installation

Getting started with SpecKit is super easy. Install the specify tool using [uv](https://docs.astral.sh/uv/): 
```shell
uv tool install specify-cli --from git+https://github.com/github/spec-kit.git
```

This will install a `specify` command which you can use to initialize and check on projects. While this isn't necessary and you can manually install by copying the templates to your project folder that seems like it's a lot of labor. Embrace the slack.

## Step Two - Using

Speckit gives you five major commands:
- `/constitution` this sets up the core directives of your application. This is where you put in UX requirements, development guidelines etc. Think of it as the common reference point between all of your specs. It creates a markdown file here `.specify/memory/constitution.md` in your repo.
- `/specify` The backbone of the app. This is where you write a specification for a feature you're working on. As the docs say you should focus more on the what and the why and not on the how. Don't pick tech stacks or solutions etc. That can be done either by going "up" a level to your `consitution` or later on with the `/plan` command. This will generate a folder called something like `specs/001-my-cool-idea` in the root of your directory.
- `/plan` This is where you choose your tech stack, libraries etc. I'll be honest sometimes in a well structured pre-existing project I just roll the dice and don't give it any specific planning instructions. So far that's only burned me about 10% of the time. It creates a `plan.md` in your specs folder. 
- `/clarify` This is optional but if the agent has questions about any ambiguity it'll prompt you with a multiple choice question about potential solutions. You can ideate those solutions and then choose the one you want.
- `/tasks` This breaks up the work into chunks for the agent to do. Creates a `tasks.md` file. Whats nice is that it's relatively fine grained and the implement command will go through check them off
- `/implement` Tells the agent to start implementing. It goes through task by task and implements them. Once thing I've noticed at least with Claude Code is that it's smart enough to farm it out to sub-agents where it makes sense to. 


The thing is you can just rip through this and type `/specify` then `/plan` then `/tasks` and then `/implement` if you want. You'll get something, but where the magic lies for me is that it generates each file and I can edit/change things before the final implementation. So the agent becomes more then just an over-eager junior with an excellent memory but it also becomes a bit of a partner in helping you get the _what_ and the _why_ on paper. 