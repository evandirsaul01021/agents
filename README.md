# Agent Skill Kit

A collection of reusable skills for AI coding agents.
Share, discover, and compose skills that make your agent smarter.

Compatible with [SkillsMP](https://skillsmp.com) | Claude Code | Codex CLI | ChatGPT

This project follows the official [Anthropic Agent Skills Specification](https://github.com/anthropics/skills) and is registered as a Claude Code plugin marketplace.

## How It Works

Skills are defined as `SKILL.md` files — structured markdown documents that AI agents automatically recognize and execute. Each skill encodes a specific workflow (e.g., conducting a requirements interview and producing a specification document), turning a multi-step process into a single command.

- **Agent-native**: Skills are plain markdown with frontmatter metadata. Any agent that reads files can pick them up.
- **Self-contained**: Each skill lives in its own directory with everything it needs — instructions, examples, and output templates.
- **Composable**: Skills are independent units. Use one at a time or chain them together for complex workflows.

## Skills

| Skill | Description | Status |
| --- | --- | --- |
| [spec-interview](skills/spec-interview/SKILL.md) | Transforms vague requirements into actionable specifications (`SPEC.md`) through structured multi-round interviews | ✅ |
| [release-notes](skills/release-notes/SKILL.md) | Analyzes git history to generate structured release notes (`RELEASE_NOTES.md`) with categorized changes and contributors | ✅ |

> ✅ Ready | 🚧 In Progress | 📋 Planned

## Agents

Agents are autonomous task executors that can be invoked via the Task tool in Claude Code. They are defined in `.claude/agents/` directory.

| Agent | Description | Tools | Status |
| --- | --- | --- | --- |
| [load-test](.claude/agents/load-test.md) | k6 load test execution and automated report generation with performance metrics | Bash, Read, Write, Glob | ✅ |

**Usage:**
```
"Run API load test"
"Execute k6 performance test"
```

**Trigger Keywords:** load test, performance test, k6, stress test

**Usage:**
```
/spec-interview
```

The skill will automatically discover requirement files (`SPEC.md`, `PRD.md`, `REQUIREMENTS.md`, etc.) in your project and begin the interview process.

## Installation

```bash
# 1. Clone the repository
git clone https://github.com/kangminhyuk1111/agent-skill-kit.git

# 2. Copy the skills you want into your project
cp -r agent-skill-kit/skills/spec-interview /your-project/skills/

# 3. Invoke the skill from your agent
/spec-interview
```

Alternatively, clone the entire repository and symlink individual skill directories into your projects as needed.

## Contributing

New skill contributions are welcome. To add a skill:

1. Create a new directory under `skills/`:
   ```
   skills/
   └── your-skill-name/
       └── SKILL.md
   ```

2. Write your `SKILL.md` with the following structure:
   ```markdown
   ---
   name: your-skill-name
   description: A short one-line description of what the skill does.
   ---

   # Skill Title

   ## Overview
   What the skill does and when to use it.

   ## Instructions
   Step-by-step instructions the agent will follow.

   ## Examples
   Input/output examples demonstrating the skill.

   ## Guidelines
   Best practices and constraints.
   ```

3. Register the skill in `.claude-plugin/marketplace.json` by adding it to the appropriate plugin group:
   ```json
   {
     "name": "your-plugin-group",
     "description": "Group description",
     "source": "./",
     "strict": false,
     "skills": [
       "./skills/your-skill-name"
     ]
   }
   ```

4. Submit a pull request.

## License

Apache 2.0
