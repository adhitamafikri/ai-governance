# AGENTS.md

## Working Principles

### **Think, Don't Just Follow:**

You're a capable AI agent. These are principles to guide your thinking, not rules to constrain you. Adapt to what you discover.

### **Code is Reality, Docs are Intentions:**

- Verify everything against actual code/config/behavior
- When docs conflict with reality, trust reality and update docs
- Recent git commits show what actually changed

### **Discovery Pattern:**

1. What already exists? (scripts/, notes/, project docs)
2. How was this solved before? (search codebase)
3. What's the current state? (git log, running processes)
4. What does the project say? (README, configs)
5. Now act based on what you learned

### **Autonomy with Safety:**

- Experiment and figure things out, but don't break production
- Test locally before touching anything shared
- Understand impact before making changes
- When uncertain about safety, ask

------------------------------------------------------------------------------------------------

## Source of Truth Hierarchy

1. **Actual code** - What the system actually does
2. **Live environment** - Production behavior
3. **Recent git commits** - What changed recently
4. **Environment config** - .env files
5. **This AGENTS.md and notes** - Intended design

**Workflow:**

- Read notes for context
- Verify against actual code
- When conflict, trust code
- Update notes to match reality

------------------------------------------------------------------------------------------------

## Investigation Protocol

### **Phase 1: Understand**

1. What fails? (collect exact error messages)
2. Which components/services affected?
3. What changed recently? (`git log --oneline -10`)
4. Is it isolated to one area or systemic?

### **Phase 2: Investigate**

Discover the tech stack first, then investigate appropriate layer:

- Web apps: Browser DevTools, network tab, console logs
- APIs/Services: Application logs, test with curl/Postman
- Databases: Connection status, query logs, schema inspection
- Infrastructure: Service status, resource usage, container logs

### **Phase 3: Fix**

1. Fix in local codebase (never directly on servers)
2. Test fix thoroughly in local environment
3. Verify complete fix (not just symptoms)
4. Update relevant documentation (notes/ or project docs)

------------------------------------------------------------------------------------------------

## Workspace Structure

**Directory Layout:**

- `playgrounds/` - All project repositories (each subdirectory is a separate git repo)
- `notes/` - Documentation and knowledge base (YYYY-MM-DD-slug.md format)
- `guides/` - Operation-specific rules and procedures (optional, but mandatory when present)
- `scripts/` - Automation scripts and utilities
- `tmp/` - Temporary context files (screenshots, data samples, conversations)
<!-- - `.env` - Workspace-level credentials -->

**Discovery Commands:**

When you need to understand the workspace, use:

<bash>
# See all projects
ls -la playgrounds/
# Check what each project is (look for package.json, go.mod, requirements.txt, etc)
find playgrounds/ -name "package.json" -o -name "go.mod" -o -name "requirements.txt"
# Find recent notes for context
ls -lt notes/ | head -20
# Check available scripts
ls -la scripts/
</bash>

**Key Principles:**

- Workspace root is NOT a git repository
- Each project in playgrounds/ is its own git repo with own dependencies
- Notes use YYYY-MM-DD-slug.md convention (get date: `date +%Y-%m-%d`)
- ALWAYS update existing notes rather than creating duplicates
- Project-specific documentation lives in the project's README, not here

------------------------------------------------------------------------------------------------

## Core Principles

**Source of Truth Hierarchy:**

1. Running code and actual behavior (what the system does)
2. Actual configuration files (.env, configs as they exist)
3. Recent git commits (what changed recently)
4. Documentation and notes (intended design, but verify!)
When docs/notes and code conflict → trust code, update docs.

**Discovery Before Action:**

Before doing anything:

- Check if tools already exist (scripts/, notes/, project docs)
- Search for similar implementations (how was this solved before?)
- Understand context (what depends on this? what does this depend on?)
- Read project-specific docs (README, CONTRIBUTING, etc.)
Don't assume. Don't guess. Discover, then act.

**Process Management Principles:**

- Check if something is already running (avoid conflicts)
- Understand dependencies (what needs to start first?)
- Use bounded commands (don't hang with infinite streams)
- Verify completion (did it actually work?)
Figure out the HOW based on the project's tech stack.

------------------------------------------------------------------------------------------------

## Tech Stack Discovery

**Don't assume tech stack - discover it:**

- Check package.json for Node.js projects
- Look for go.mod for Go projects
- Find requirements.txt for Python projects
- Read project README for specifics

**Common Patterns in This Workspace:**

- Hot reload: Changes auto-restart (PM2, nodemon, Next.js dev mode)
- Containerization: Most projects use Docker
- CI/CD: Check for .github/workflows/, .woodpecker.yml, or similar
- Package managers: Check what project uses (npm, bun, pip, go mod)

**Process Management:**

- Development: Usually hot reload (don't restart unnecessarily)
- Production: Typically Docker containers
- Always check if service is already running before starting

------------------------------------------------------------------------------------------------

## General Workflow Principles

**Before Starting Work:**

1. Check if services are already running (avoid conflicts)
2. Read project's README for specific startup instructions
3. Check notes/ for any known issues or dependencies
4. Look for project-specific docs (CONTRIBUTING.md, etc.)

**Making Changes:**

1. Research existing implementation (Grep for similar features)
2. Follow established patterns in that project
3. Test locally first (check project's test commands)
4. Update project docs if you introduce new patterns

**General Practices:**

- Never edit code directly on servers (use version control)
- Test in isolated environment first
- Check project's CI/CD setup (look for .github/, .woodpecker.yml, etc.)
- Coordinate with deployment process (documented in project or notes/)

------------------------------------------------------------------------------------------------

## Credentials

**Check in order:**

1. Workspace `.env` (root) - Shared credentials
2. Project `.env` (playgrounds/project/) - Project-specific
3. Global (~/.config, ~/.ssh) - System-wide

**Usage:**

<bash>
# Source workspace .env first
source /path/to/workspace/.env && {command}
# Example: Database access
source .env && psql -h $DB_HOST -U $DB_USER -d $DB_NAME
</bash>

------------------------------------------------------------------------------------------------

## Workspace Conventions

**Research Before Implementing:**
Before adding any feature:

1. Search for similar implementations: `grep -r "feature_name" playgrounds/`
2. Read relevant notes for context: `ls notes/ | grep -i "topic"`
3. Check project's own README and docs
4. Follow established patterns in that project

**Multi-Project Coordination:**
When changes affect multiple projects:

- Identify all affected repos first
- Update related projects together
- Test integration points
- Document cross-repo dependencies in notes/

**Service Dependencies:**
If projects depend on each other  (check notes/ or project docs):

- Start services in correct order
- Verify dependencies are running before starting dependents
- Check ports and connections

**Specialized Guides:**
If `guides/` directory exists:

- These are RULES for specific complex operations
- Check `ls guides/` for available operation guides
- Read relevant guide COMPLETELY before starting work
- Follow guide procedures exactly (they contain safety checks and required steps)
- Guides override general instructions when applicable

------------------------------------------------------------------------------------------------

## Quick Context Gathering

### Workspace Level

<bash>
- ls -la playgrounds/ # All projects
- ls -lt notes/ | head -10 # Recent notes
- cat AGENTS.md | head -100 # Workspace docs
</bash>

### Frontend Project Level

<bash>
- cat README.md | head -50 # Project overview
- git log --oneline -10 # Recent changes
- cat package.json | grep -A 15 '"scripts"' # Available commands
</bash>

### Backend Project Level

<bash>
- cat README.md | head -50 # Project overview
- git log --oneline -10 # Recent changes
</bash>

### Infrastructure Level

<bash>
- find playgrounds/ -name "Dockerfile" # All Docker configs
</bash>
