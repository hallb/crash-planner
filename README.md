# crash-planner

Planning and milestone tracking for the Bird Murmuration Simulator (crash) project.

## Structure

- **crash-planner** (this repo): Planning state, milestones, issues — lives in `.mdp/`
- **crash**: Application code — requirements, solution design, implementation

Planning artifacts stay in crash-planner to avoid branch confusion with the main application repo.

## Markdown Projects (mdp)

The `.mdp/` directory follows the [Markdown Projects](https://www.markdownprojects.com/) convention: issues and milestones as plain markdown files with YAML frontmatter.

### Using the mdp CLI

The mdp CLI requires [Bun](https://bun.sh/). Install Bun, then:

```bash
# Install dependencies (includes markdown-projects)
npm install

# Run mdp via bunx (Bun runs the TypeScript CLI)
bunx mdp project get
bunx mdp milestone list
bunx mdp issue list
```

**Troubleshooting:** If `bun` or `bunx` is not found, ensure `~/.bun/bin` is in your PATH. The Bun installer adds this to `~/.bashrc`; run `source ~/.bashrc` or open a new terminal. You can also use `npm run mdp -- milestone list` — the `script/mdp` wrapper adds Bun to PATH automatically.

If Bun is not installed, you can still edit `.mdp/` files directly — they are plain markdown.

## Workflow

1. **plan-milestone** (skill): Break a milestone into issues, suggest bug inclusion, scope check
2. **execute-milestone** (skill): Implement issues in crash repo on `feature/{milestone-id}` branch
3. **refactor-phases** (skill): Restructure milestones to canonical shape

Rules and skills live in `crash/.cursor/`.
