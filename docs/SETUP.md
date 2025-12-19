# Vibe Review 10-Panel: Claude Code Setup Guide
*Created: 2025-12-19*

This guide explains how to install and configure Vibe Review as a slash command in Claude Code.

---

## Prerequisites

1. **Claude Code** installed and configured
   - Get Claude Code at: https://claude.ai/code
   - Follow Anthropic's installation instructions

2. **Playwright MCP** (recommended for URL evaluation)
   - Enables browser automation for screenshot capture
   - Without Playwright, URL targets will use code analysis only

---

## Installation Methods

### Method 1: Clone Repository (Recommended)

```bash
# 1. Clone the vibe-review-10-panel repository
git clone https://github.com/YOUR_ORG/vibe-review-10-panel.git

# 2. Navigate to your project
cd /path/to/your-project

# 3. Create .claude/commands directory if it doesn't exist
mkdir -p .claude/commands

# 4. Copy the slash command
cp /path/to/vibe-review-10-panel/.claude/commands/vibe-review.md .claude/commands/
```

### Method 2: Manual Installation

1. Create the commands directory in your project:
   ```bash
   mkdir -p .claude/commands
   ```

2. Create the file `.claude/commands/vibe-review.md`

3. Copy the contents from the [slash command file](../.claude/commands/vibe-review.md)

### Method 3: User-Level Installation (Available in All Projects)

To make Vibe Review available across ALL your projects:

```bash
# Create user-level commands directory
mkdir -p ~/.claude/commands

# Copy the slash command
cp /path/to/vibe-review-10-panel/.claude/commands/vibe-review.md ~/.claude/commands/
```

**Note**: User-level commands are available in every project without copying.

---

## How Claude Code Discovers Slash Commands

Claude Code automatically discovers slash commands from these locations:

1. **Project-level**: `.claude/commands/` in your project root
2. **User-level**: `~/.claude/commands/` in your home directory

When you type `/` in Claude Code, it lists all available commands from both locations.

### Command File Requirements

- Must be a `.md` (markdown) file
- Filename becomes the command name (e.g., `vibe-review.md` → `/vibe-review`)
- File content becomes the prompt that Claude executes

---

## Verification

After installation, verify the command is available:

1. Open Claude Code in your project directory
2. Type `/vibe-review` - it should appear in autocomplete
3. Run a test evaluation:
   ```
   /vibe-review http://localhost:3000 dev
   ```

---

## Playwright MCP Setup (Optional but Recommended)

For full browser automation capability when evaluating URLs:

### 1. Install Playwright MCP

Follow the Playwright MCP installation guide for Claude Code.

### 2. Configure MCP Settings

Add to your Claude Code MCP configuration:

```json
{
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": ["@anthropic/mcp-playwright"]
    }
  }
}
```

### 3. Verify Playwright

When running `/vibe-review` on a URL, Claude will:
- Navigate to the URL
- Take screenshots
- Capture accessibility tree
- Evaluate performance metrics

Without Playwright, Claude will analyze the URL target using available code files only.

---

## Configuration Options

### Customizing Judge Weights

You can modify the behavioral vectors in your local copy of `vibe-review.md`:

```markdown
| **Security Specialist** | Auth, API Protection | strictness=0.95, paranoia=0.95 |
```

Adjust values (0.0 to 1.0) to change judge sensitivity.

### Adding Custom Evaluation Profiles

Add new rows to the Context-Aware Evaluation Profiles table:

```markdown
| `custom` | 0.8 | 0.7 | 0.9 | 0.6 | 0.7 | 0.6 | 0.5 | 0.6 | Custom profile description |
```

### Excluding Judges

To skip certain judges, add a note in the slash command or comment out rows in the judge table.

---

## Troubleshooting

### Command Not Found

If `/vibe-review` doesn't appear:

1. Verify file location: `.claude/commands/vibe-review.md`
2. Check file permissions: `chmod 644 .claude/commands/vibe-review.md`
3. Restart Claude Code

### Playwright Errors

If browser automation fails:

1. Verify Playwright MCP is installed
2. Check MCP configuration
3. Try with a codebase path instead of URL

### Output File Not Created

If the report file isn't generated:

1. Check Claude has write permissions to project directory
2. Verify the TARGET is accessible
3. Check for error messages in Claude's response

---

## Team Deployment

### For Teams Using GitHub

1. Add `.claude/commands/` to your repository
2. Include `vibe-review.md` in the commit
3. Team members get the command automatically when they clone

### Version Control Best Practices

```bash
# Add to .gitignore to exclude output files (optional)
*-vibe-review.md

# Or track them for team visibility
# (remove from .gitignore)
```

### Standardizing Across Projects

Create an organization-level commands repository:

```
your-org-claude-commands/
├── .claude/
│   └── commands/
│       ├── vibe-review.md
│       ├── code-review.md
│       └── other-commands.md
└── README.md
```

Team members symlink or copy to their projects.

---

## Next Steps

- Read [METHODOLOGY.md](METHODOLOGY.md) for full evaluation methodology
- See [JUDGES.md](JUDGES.md) for deep dive on each judge
- Check [EXAMPLE_OUTPUT.md](EXAMPLE_OUTPUT.md) for sample reports
- Learn about [SUSTAINABILITY.md](SUSTAINABILITY.md) for green software principles
