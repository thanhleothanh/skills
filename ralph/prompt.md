# ISSUES

Local `.issues/` folders are provided at root folder. Parse the issues files inside to understand the open issues/tasks.

# EXPLORATION

Explore the knownledge about how to work on the issues are in local `.docs/contexts/` and `.docs/adrs/` folders. Parse the ADR and CONTEXT files to understand more about the contexts of the issues/tasks/features and the systems as a whole.

Explore the repo more if needed.

# WHAT TO DO

Act as a principal software engineer, work on the AFK issues only, not the HITL ones.

Review also the most recent 5 commits you've added so far (not commits added by other peoples, cause they might be about other features) to understand what work has been done.

If all AFK tasks are complete, output <promise>NO MORE TASKS</promise>.

# TASK SELECTION

Pick the next task. Prioritize tasks in this order:

1. Critical bugfixes

2. Development infrastructure

Getting development infrastructure like the domain models and domain models logic and unit tests for those, the important precursor to building features.

# FEEDBACK LOOP

1. Use `/tdd` to develop the issues/tasks

2. Polish and refactor the new or changed code with `/refactor`

3. Check:
  - If the task is complete, move the issue file to `.issues/done/`.

  - If the task is not complete, add a note to the issue file with what was done.

  - If all tasks are complete, do nothing

  - Run the `mvn clean package` to check the build and tests. Only commit if build success and no tests fail, otherwise check and fix

# COMMIT

Make a git commit. The commit message must:

1. Include key decisions made
2. Include files changed
3. Blockers or notes for next iteration

# FINAL RULE

ONLY WORK ON A SINGLE TASK.
