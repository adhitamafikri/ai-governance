# PR Update Task for Agents

1. **Mission**: Update the PR github of the current branch with new title nor description

2. **Task Details**:

- If this prompt is given to you, it means that the previously generated PR title nor message might be not clear enough.
- Scan the commits only committed by the current branch. Understand the context of changes of each commit by thoroughly reading the commit message and the actual diffs
- Generate PR comprehensive title and description based on the information you've extracted. Make sure to write it in a proper `.md` format into a temporary file named `pr_description.md` in the project root
- Execute the PR creation by running the `gh pr edit` command with the title and description you've generated
- Remove the `pr_description.md` file once the PR creation is succeeded
