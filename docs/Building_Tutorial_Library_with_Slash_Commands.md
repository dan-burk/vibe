# How I Automated Documentation with reusable prompts

In December 2025, I set out to create a comprehensive tutorial library for Claude Code. My goal: hands-on, focused tutorials that walk complete beginners through real tasks step by step. No theory dumps. No comprehensive reference manuals. Just "do this, then this, then this" until you've accomplished something concrete.

What started as a few documentation files quickly evolved into a multi-language learning platform with over 100 tutorial documents. The secret? I didn't write them all manually. Instead, I built a set of custom slash commands (reusable prompts, essentially) that transformed Claude Code into an automated documentation factory—one that consistently produces tutorials in my hands-on, step-by-step style.

## The Challenge

Creating tutorials is time-consuming. Each one requires research for current best practices, structured beginner-friendly writing, consistent formatting, technical accuracy validation, translation into multiple languages, and ongoing maintenance as tools evolve. Doing this manually for 20+ tutorials in 3+ languages would take weeks.

## The Solution: From Manual Process to Automated Slash Commands

The key insight: **automate proven workflows, not theoretical ones**.

I didn't sit down and design slash commands from scratch. Instead, I created the first few tutorials manually through interactive prompting with Claude, refined the process through iteration, then asked Claude to codify the working process into a slash command.

This is exactly the pattern described in my [research paper tutorial](./Writing_Research_Paper_Claude_Code.md): go through the workflow manually, then in the final step, ask Claude to save it as a reusable command.

The result was five specialized slash commands that handled the entire tutorial lifecycle.

### [`/tutorial`](./assets/commands/tutorial.md) - The Tutorial Generator

Born from creating several tutorials interactively, this command captures the proven workflow. It follows a rigorous three-phase approach.

First, Claude searches the web for current information before writing anything—no more outdated version numbers or deprecated installation methods. Then, before writing a single word, Claude presents a plan: what it learned from research, recommended approach for beginners, and outline of major steps. Only after I approve does Claude write the tutorial following strict formatting rules: home link at top, engaging hook, key concepts, step-by-step instructions with action verbs, troubleshooting section, and creation date.

The command enforces consistent structure across all tutorials. Every tutorial feels like it came from the same author—because they followed the same systematic process. I generated 20+ tutorials covering topics from basic Git operations to advanced Docker workflows, all with consistent quality and structure.

### [`/review-tutorial`](./assets/commands/review-tutorial.md) - The Quality Control Bot

After generating tutorials, quality matters. This slash command performs comprehensive review against 40+ quality criteria covering content quality, formatting standards, beginner-friendliness, technical accuracy, and writing quality.

The command presents findings in a structured report, then applies fixes after approval. I used this to batch-polish multiple tutorials at once, applying consistent improvements across the entire library. Uniform quality across all tutorials without manually reviewing each one multiple times.

### [`/translate-chinese`](./assets/commands/translate-chinese.md) & [`/translate-spanish`](./assets/commands/translate-spanish.md) - The Localization Engine

Interestingly, the Japanese translations came first—and without a slash command. I simply asked Claude Code to translate all the tutorials to Japanese in one prompt. Claude automatically spawned 8 subagents running in parallel, each handling different tutorials simultaneously. The results were excellent, which gave me confidence to formalize the process into slash commands for Chinese and Spanish.

For Chinese and Spanish, I discovered Claude's remarkable ability to write prompts. I simply asked Claude to create a slash command for translating tutorials—without giving any specific guidelines. Claude generated comprehensive commands on its own, adding detailed rules for what to translate, what to keep in English, language-specific formatting, and quality checklists. The AI wrote better prompts than I would have.

With the slash commands ready, I asked Claude Code to translate all 25 tutorials using subagents. The entire translation—50 new files across two languages—took only 15 minutes.

These translation commands handle the complexity of technical translation. Instructional text, section headings, and explanations get translated. Code blocks, commands, technical terms like Git and Docker, file paths, and URLs stay in English. The commands include language-specific rules: Simplified Chinese characters with proper punctuation for Chinese, formal "usted" form with proper accent marks for Spanish. Each translation command also performs a quality review checklist before saving, ensuring natural phrasing rather than word-for-word translation.

The result: 81 translated tutorial files across Chinese, Spanish, and Japanese directories—all maintaining consistent quality and structure.

### [`/review-translation`](./assets/commands/review-translation.md) - The Translation Maintenance Tool

Tutorials evolve. Commands change. New sections get added. This command keeps translations in sync by reading both the English original and target language translation side-by-side, identifying missing sections, outdated content, and structural differences.

Even if translations are up-to-date, it checks translation accuracy, language quality, and formatting consistency. Then it presents findings, gets approval, and applies updates. When I updated English tutorials, I could quickly propagate changes to all translations.

## Scaling with Subagents

For truly parallel work, I used Claude's subagent feature. When polishing Japanese translations, I launched multiple review agents simultaneously, processing 19 files with coordinated improvements.

The combination of slash commands for structured workflows and subagents for parallelization created a documentation pipeline that scaled far beyond what manual effort could achieve.

## The Results

In less than two weeks, I created 20+ English tutorials covering beginner to intermediate topics, 81 translated tutorials across 3 languages, consistent quality through automated review processes, and maintainable documentation with sync tools for translations.

All tutorials follow the same structure, writing style, and formatting conventions—because they were generated by the same systematic process.

## Key Lessons

**Start manual, then automate.** Don't write slash commands from scratch. Do the task manually first, refine the process, then ask Claude to save it as a command. The `/tutorial` command works because it codifies a workflow I'd already validated through creating real tutorials.

**Structure commands as multi-phase workflows.** Don't just tell Claude what to do—tell it how to think through the problem. The research → plan → approve → execute structure prevented countless issues.

**Build quality control into the process.** The `/review-tutorial` and `/review-translation` commands weren't afterthoughts—they were core parts of the workflow. Automated generation without automated quality control leads to inconsistent output.

**Make commands collaborative, not autonomous.** Every slash command includes approval steps. This kept me in control while eliminating repetitive work. Claude handled the tedious parts; I made the strategic decisions.

## Conclusion

Building this tutorial library taught me that automation isn't about removing humans from the process—it's about amplifying human judgment. I didn't write 100+ tutorials manually, but every single one reflects my standards, my structure, and my approval.

Slash commands transformed Claude Code from a helpful assistant into a documentation factory that works at my direction, maintains my standards, and scales to whatever size project I need.

If you have repetitive documentation tasks, don't keep doing them manually. Build the slash command once, then deploy it dozens or hundreds of times.

That's the power of systematic automation.

---

*Want to see the slash commands I built? Check out the [commands folder](./assets/commands/). The full tutorial library is available at the [project documentation site](https://github.com/gexijin/vibe/tree/main/docs).*

Created by [Steven Ge](https://www.linkedin.com/in/steven-ge-ab016947/) on December 15, 2025.

---

**P.S.** This blog post was itself drafted by Claude Code through iterative prompting:
1. "Review my commit history and write a blog post about how I used slash commands to automate."
2. "Reflect that the /tutorial command evolved from manual interactive prompting first."
3. "Emphasize my tutorial style: hands-on, focused, step-by-step."
4. "Add that Japanese translations came first without slash commands, and Claude used 8 subagents in parallel."
5. "Add that Claude wrote the translation slash commands without specific guidelines, and 25 tutorials were translated in 15 minutes."
6. "Link to the saved commands in docs/assets/commands."
7. "Rewrite with fewer bullet points."
8. "Summarize our interaction at every turn. Add a P.S. about how this blog was generated."
