---
name: minh
description: "Browse and launch the user's available skills from a clickable, drill-down menu. Use when the user types /minh or asks to see, browse, pick from, or be reminded of their skills (e.g. 'show my skills', 'skill menu', 'what skills do I have', 'which skill should I use'). Presents category chips, then skills within a category, then a skill's description with a Launch/Back choice; on Launch, invokes that skill."
---

# minh — Skill Browser

A clickable, drill-down menu for discovering and launching skills. The user has many skills and does not want to remember names. Surface them as tappable option chips via the `AskUserQuestion` tool, narrowing category → skill → launch.

## Ground truth: what skills exist

Do **not** hardcode a skill list. Use the authoritative list of skills available in the **current session** — the ones listed as available to the `Skill` tool in this conversation's context (the "available skills" system reminder). This auto-adapts: project-scoped skills (e.g. `resume-tailor` inside `career-ops`) appear only when the session is in that project, and vanish elsewhere.

Each entry has a name (possibly namespaced, like `anthropic-skills:pdf` or `excalidraw:excalidraw`) and a one-line description. In menus, show the **short name** (the part after the last `:`). When launching, pass the **full name** to the `Skill` tool.

### Exclude noise
Leave these out of the menu (internal/example/authoring plumbing the user does not pick day to day): `minh` itself, and any skill whose name matches `example-*`, `*-development`, `plugin-structure`, `plugin-settings`, `mcp-integration`, `build-mcp*`, `build-mcpb`, `configure`, `access`, `playground`, `writing-rules`, `solo`, `siege`. If in doubt, keep a skill rather than hide it.

## Categories

Group the available skills into these buckets. Match by the mapping below; place any available skill not listed into the best-fit bucket by its description. Any skill that is clearly project-local (not one of the known personal/Anthropic/plugin skills) goes under **This Project**. Omit any category that ends up empty.

| Category | Skills (match by name; others by description) |
| --- | --- |
| 🛠 Workflow | grilling, build-from-plan, discovery, commit-pr, show-me, run, loop, schedule |
| ✍️ Writing & Editing | humanizer, writing-session, docs, import-memory |
| 📄 Files & Formats | pdf, docx, pptx, xlsx, google-workspace |
| 🎨 Visual & Design | slideshow, poster-design, excalidraw, dataviz, artifact-design, artifact-diagramming, artifact-capabilities, frontend-design |
| 🔎 Research & Browser | deep-research, chrome-browser, built-in-browser, computer-use, morning |
| 🔐 Security & Review | wireshark-analysis, security-review, code-review, simplify, claude-security |
| ⚙️ Claude Code Setup | update-config, keybindings-help, fewer-permission-prompts, plugin-authoring, init, claude-api, skill-creator |
| 📁 This Project | any project-local skill available only because of the current directory |

## The 4-chip rule (pagination)

`AskUserQuestion` shows **at most 4 options**. Whenever a level has more than 4 entries, show 3 entries plus a 4th option **"➡️ More…"**; when chosen, ask again with the next page. The user can always type a skill or category name directly (the tool's free-text fallback), so a "Back" option is optional — include **"⬅️ Back"** as an option on sub-menus when a slot is free.

## Flow

1. **Category menu.** Build the non-empty categories (with their emoji labels). Call `AskUserQuestion` with one question, header `Skills`, options = the categories (paginating per the 4-chip rule). Each option's `description` = a short phrase plus the count, e.g. "Editing, PRDs, docs — 4 skills".

2. **Skill menu.** After a category is chosen, call `AskUserQuestion` again, header = the category's short name, options = the skills in it (short name as label, its one-line description as the option description; paginate per the 4-chip rule; include "⬅️ Back" to return to the category menu if a slot is free).

3. **Detail + confirm.** After a skill is chosen, call `AskUserQuestion` with header = the skill's short name, a `question` containing the skill's full description, and exactly two options: **"🚀 Launch"** and **"⬅️ Back"**.

4. **Launch.** If Launch is chosen, invoke that skill via the `Skill` tool using its **full** name. If the skill needs input (e.g. text to humanize, a target to review), let the skill prompt for it as normal. If Back is chosen, return to the skill menu for that category.

## Style

- Keep chat prose to almost nothing — the menu *is* the interface. A one-line lead such as "Here are your skills:" before the first menu is enough.
- Never invent skills that are not in the current session's available list.
- If the user names a skill or category directly (by voice or typing) instead of tapping, honor it and jump to that level.
- If, unusually, no skills are available to list, say so plainly in one line instead of showing an empty menu.
