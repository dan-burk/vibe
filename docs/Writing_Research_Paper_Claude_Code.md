[Home](./)

# Writing a Research Paper with Claude Code

Write research papers using Claude Code as an assistant for research, brainstorming, planning, drafting, and editing. See an [example paper](./example_paper.md) created using this workflow.

## Key Concepts

- **Workflow** - Research → Brainstorm → Focused Research → Outline → Draft → Revise manually → Polish with AI → Add Abstract → Improve Title → Check references → Proofread with AI
- **AI assistant** - Human makes key decisions while AI does the tedious work
- **Claude Code** - Agentic AI system that searches the web, organizes research, and drafts content through simple requests
- **slash command** - A customized, detailed prompt that can be reused in Claude Code

## What You'll Need

- Claude Code installed ([Windows guide](./Install_CLAUDE_Code_Win.md) | [Mac guide](./Install_Claude_Code_MacOS.md))
- VS Code installed ([download](https://code.visualstudio.com/))
- Terminal access
- 20-30 minutes

## Step 1: Set Up Project and Start Claude Code

First, start a terminal window and navigate to a user folder.

**Windows (WSL Ubuntu):**

Start the **Ubuntu** app using the Windows **Start** button, and then search for Ubuntu. In the terminal:

```bash
cd /mnt/c/Users/YOUR_USERNAME/Documents
```
Replace `YOUR_USERNAME` with your actual Windows username. (To find it, type `whoami` in the terminal—it shows after the backslash.)

**Mac:**
Start a terminal window, and then:

```bash
cd ~/Documents
```

**Running VS Code inside Docker:**
Start a terminal by clicking **Terminal → New Terminal** from the main menu. Then:
```bash
cd ~
```

For all platforms, create a new project folder for your research paper and start Claude Code:

```bash
mkdir ai_research
cd ai_research
claude
```

Claude Code is ready.

## Step 2: Initial Research

Ask Claude to research your topic:

```
I'm writing a ~1,000 word research paper on AI adoption in the workplace.
Search for recent data (2023-2025) on:
- Productivity gains from AI tools
- Job displacement concerns and statistics
- Real-world case studies from companies

Requirements:
- Prioritize peer-reviewed research and credible industry reports
- Avoid anecdotes and opinion pieces
- List each source with a 1-3 sentence summary
- Group sources by topic

Save as general_research.md
```

Claude searches the web and organizes findings. Review `general_research.md` in your text editor. Ask for a summary:

```
Give me a brief summary.
```

## Step 3: Read the Sources
Read through the research document and click through to the original sources to verify the information. You can use any text editor such as NotePad on Windows or TextEdit on Mac. We recommend **VS Code**:
1. Go to File → **Open Folder** → navigate to the `ai_research` folder
2. Click `general_research.md` in the Explorer panel on the left
3. Preview the formatted document: **Ctrl + Shift + V** (Windows/Linux) or **Cmd + Shift + V** (Mac)
4. Click the source links to read the original articles and studies

## Step 4: Brainstorm Your Angle

Ask Claude to help brainstorm:

```
Based on this research, suggest 3-4 angles I could take for this paper.
```

Review the angles and pick the one that interests you most.

## Step 5: Focused Research

Now that you have your angle, ask Claude for targeted research:

```
I want to focus on [your chosen angle]. Search for more specific data
and examples that support this perspective. Save as focused_research.md
```

Claude finds targeted information.

## Step 6: Create Your Plan

Ask Claude to create an outline based on your chosen angle:

```
Give me 3 options for a brief outline for my paper based on the focused
research and my chosen angle. Use bullet points for the narrative flow.
Save as outlines.md
```

Review the outline and ask Claude to adjust as needed (e.g., "Make section 2 focus more on case studies" or "Add a section on limitations"). 

## Step 7: Draft the Paper

Select your outline and ask Claude to write the full draft:

```
I like outline #2 [your chosen option].

Write a ~1,000 word research paper based on the outline and research.

Structure:
- Introduction: Hook, context, thesis statement
- Body: 2-3 sections with arguments, statistics, and examples
- Conclusion: Summary and implications

Style:
- Clear, concise sentences (15-20 words average)
- Active voice, analytical tone
- Statistics woven into prose (no bullet lists)
- Smooth transitions between paragraphs

Citations:
- Use numbered references [1], [2], etc. after claims
- Include 5-15 references
- Add a References section at the end

Save as paper.md
```

Claude writes the draft.

## Step 8: Revise Manually

Open `paper.md` in your text editor. Read through carefully and make your own revisions:
- Add your personal voice and insights
- Adjust arguments to match your thinking
- Fix any awkward phrasing
- Ensure citations are accurate

Save your changes in the editor.

## Step 9: Polish with AI

Ask Claude to improve specific sections:

```
Make the introduction more engaging with a compelling hook.
```

```
Strengthen the conclusion with a clear call to action. Do not increase its overall length.
```

Review Claude's changes.

## Step 10: Add an Abstract

Ask Claude to add a short executive summary at the beginning:

```
Add an abstract at the beginning of the paper. Write 2-3 short sentences
that summarize the paper.
```

Claude will add the abstract. Review and edit to ensure it accurately captures your paper's essence.

## Step 11: Improve Title

Ask Claude to give you a few options for the title:

```
Give me a few options for the title. Make it more appealing.
```

Select a title. Add your own touch:

```
I like option #2 [your choice]. Edit the file.
```

## Step 12: Check References (Optional)
Ask Claude to verify your citations are consistent and complete:
```
Check all references in my paper:
- Verify each citation number [1], [2], etc. has a matching reference
- Verify each reference in the list is actually cited in the paper
- Check that author names and titles are consistent
- Verify the cited data and examples appear in the source
```

Note: Claude can only verify publicly accessible sources. For paywalled articles, manually check that your citations match what you read.

## Step 13: Proofread with AI

Ask Claude to do a final proofread:

```
Do a final proofread of the paper:
- Fix any spelling and grammar errors
- Ensure consistent formatting throughout
- Check flow and transition
```

Review Claude's changes.

**Export to Word:** In VS Code, open the markdown preview with **Ctrl + Shift + V** (Windows/Linux) or **Cmd + Shift + V** (Mac). Click inside the preview pane, press **Ctrl + A** (or **Cmd + A** on Mac) to select all, then **Ctrl + C** (or **Cmd + C**) to copy. Paste into Microsoft Word—the formatting will be retained.

## Step 14: Create a Slash Command for Future Papers

Save this workflow as a reusable slash command for your next research paper:

```
Create a slash command called /research-paper that guides me through
this entire workflow. Save it so I can use it for future research papers on various topics.
```

Claude will create a custom slash command in your `.claude/commands/` folder. It is a Markdown file containing a prompt. You can start your next research paper by simply typing `/research-paper [your topic]`!

## Step 15: Get Feedback

LLMs have no memory. For each response, we have to send all our previous conversations in the chat session for context. As the interaction gets longer, we need to be aware of the length of the context. If it is unrelated, or we can provide a cleaner context, we will benefit from a fresh start.

Clear Claude's memory to get feedback on your paper. Type:

```
/clear
```

This removes all conversation history, so Claude will read your paper with fresh eyes. Now ask for feedback:

```
Read paper.md and give me honest feedback. 
```

Claude will critique your paper without being influenced by having written it. Make any final revisions based on the feedback.


## The Complete Workflow

1. **Research** - Claude searches for general information on your topic
2. **Read Sources** - Review the research in VS Code
3. **Brainstorm** - Pick your angle/perspective
4. **Focused Research** - Claude finds targeted data for your chosen angle
5. **Plan** - Claude creates outline options based on your perspective
6. **Draft** - Claude writes the full paper with references
7. **Revise Manually** - You add your voice and make changes
8. **Polish with AI** - Claude improves specific sections
9. **Add Abstract** - Claude creates executive summary
10. **Improve Title** - Claude suggests title options, you customize
11. **Check References** - (Optional) Claude verifies all citations
12. **Proofread with AI** - Claude fixes errors and improves flow
13. **Create Slash Command** - Save the workflow for future papers
14. **Get Fresh Feedback** - Clear memory for unbiased critique

## Next Steps

- **Format:** Give me the paper in LaTex format. 

Now that you have the `/research-paper` slash command, try writing more papers:
- **Technology:** `/research-paper "Impact of social media on teen mental health"`
- **Business:** `/research-paper "Remote work productivity"`
- **Science:** `/research-paper "CRISPR gene editing ethics"`

The slash command will guide you through the entire workflow automatically! Don't forget to clear the memory when you are switching topics.

## Troubleshooting

- **Claude search results seem outdated:** Specify "search for 2024-2025 data on [topic]"
- **Draft is too long/short:** Tell Claude: "Make this approximately 1,000 words"
- **Can't find files:** In terminal, type `ls` to list all files in current folder

## What You Can Ask Claude

- `search for more recent statistics on [topic]` - Find newer data
- `summarize the key arguments in this paper` - Get overview
- `make the conclusion more persuasive` - Improve specific sections
- `cite all sources in APA format` - Format references

Claude handles research and writing through natural language—no commands to memorize!

Created by [Steven Ge](https://www.linkedin.com/in/steven-ge-ab016947/) on December 9, 2025.
