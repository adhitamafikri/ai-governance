# PR Creation Task for Agents

1. **Mission**: Create a github PR for the current branch with proper title and description

2. **Task Details**:

- Scan the commits only committed by the current branch. Understand the context of changes of each commit by thoroughly reading the commit message and the actual diffs
- Generate comprehensive PR title and description based on the information you've extracted. Make sure to write it in a proper `.md` format into a temporary file named `pr_description.md` in the project root
- Execute the PR creation by running the `gh pr create` command with the title and description you've generated
- Remove the `pr_description.md` file once the PR creation is succeeded
