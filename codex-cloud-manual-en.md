# The Codex Cloud Playbook: From a Small Change to a Reviewable Pull Request

[日本語版](./codex-cloud-manual-ja.md) · Independent field guide · November 19, 2026

## What you’ll submit

Imagine you maintain a Markdown editor. A writer asks, “Can I glance at the formatted page, then keep typing where I left off?” Your team agrees to improve the preview shortcut. Someone else will review the change. What would you want them to find when they open GitHub?

> **Draft PR · Return to the editor after previewing a document**
>
> **Why.** Writers switch between writing and previewing several times in a paragraph. An extra click to resume typing breaks that rhythm.
>
> **Where to look.** The preview shortcut handler and the shortcut entry in each language edition of the desktop manual.
>
> **Try it.** Type `one two`, put the caret before `two`, open the preview with `Ctrl+Shift+V`, then use the documented route back to editing. Without clicking, type `new `. The line should read `one new two`.
>
> **Still to check.** Keyboard focus in the target browser. Record the browser, the revision you tried, and what happened.

This is an illustrative PR for a desktop editor, inspired by MD//WORKS. The last line is deliberately open. A reviewer can pick up the work because the author has given them a precise question and a way to answer it.

You’ll build a PR like this in a browser, starting with a GitHub repository and a Codex Cloud task. A *pull request* (PR) proposes changes from a working branch for inclusion in a target branch. Its *diff* shows the lines someone would add, change, or remove. You can follow the exercise as an author, a reviewer, or a pair of classmates sharing those roles.

## 1. Start your first cloud task

**Choose a change you can actually make.** Use a practice repository you can push to, or a fork where you can open a PR against your own default branch. For the shortcut exercise, choose an editor with a working preview and a documented way back to editing. If the shortcut already works, look for a real gap in the manual and make that your task. With only a README, try the smaller exercise below. You’ll need access to Codex Cloud and permission to connect the repository or use an environment that already includes it.

| When you want to… | What to do |
| --- | --- |
| Give future tasks the same tools and setup | Publish a Cloud environment. Its sharing settings control who can use it. |
| Continue work you started yesterday | Reopen the original task. Each new task has its own working files. |
| Invite a colleague to inspect your changes | Push the working branch and open a draft PR on GitHub. |
| Bring an approved change into the target branch | Merge the PR on GitHub after the required checks and reviews. |

**Prepare the environment.** In ChatGPT on the web or desktop, start a task and choose **Work in → Cloud**. If your project already has a published environment, select it. For a new setup, open **Select environment → Create environment**, choose the repository, connect GitHub if prompted, and select **Get started**. Read the setup report. If the project uses a test runner, check that setup could actually run it. Resolve any missing tools, save the configuration, choose **Publish**, then **Start a new task**. [Cloud environment setup](https://learn.chatgpt.com/docs/environments/cloud-environments)

**Give Codex an observable outcome.** Adapt the prompt below to your repository. Naming the starting behavior matters, particularly in an editor that cycles through several preview modes.

```text
Read the applicable AGENTS.md instructions, the preview handler, and the
desktop manuals. Identify the current shortcut sequence and how a writer
returns to editing. Check whether Ctrl+Shift+V already has a binding.

Goal: A keyboard user can open preview, return to the document, and keep
typing at the original caret position without clicking.

Keep the editor's existing preview modes and menu commands. Reuse the
current route back to editing. If the proposed shortcut conflicts with
another command, report the conflict before changing the binding.

Make the smallest change needed. Update the affected English and Japanese
desktop instructions to describe the behavior you implemented. If the
behavior already works, change only instructions that are out of date.

Run the relevant project checks. Show the diff, the commands and results,
and any browser checks that still need a person. Stop before opening a PR.
```

**README-only exercise.** Ask Codex to add a “Try it” paragraph to the README using an example already supported by the project. Have it identify the source for the example, run the example if possible, and report the result. In the next sections, use “Can a reader follow this paragraph?” as your acceptance criterion. This path works for a research group or writing class with no application code to maintain.

Once the cloud task is running, you can close your laptop and return to it later. A physical keyboard or a particular browser may still matter for acceptance testing. In that case, try the PR revision on the device your readers use. [Codex Cloud overview](https://learn.chatgpt.com/docs/cloud)

## 2. Read the diff and check the evidence

Begin with the list of changed files. For the preview exercise you might expect a shortcut handler, a focused test, and two manual entries. If a dependency file or an unrelated translation also changed, open that diff and ask what required it. Then read the changed lines alongside the original request.

The table below is a **review worksheet**. Fill in the last column from your own run. A code inspection, an automated test, and a hands-on check answer different questions.

| Acceptance criterion | Evidence to look for | Result from this run |
| --- | --- | --- |
| The shortcut opens the intended preview | A test or observation that starts in the editor and reaches the expected view | Record the command or steps and the observed view. |
| Typing resumes at the original caret | The “one new two” check on the PR revision | Record browser and outcome, or “pending browser check.” |
| Both desktop manuals describe the same interaction | The two edited passages agree with the implemented key sequence and return path | Name the sections checked and any discrepancy. |

Suppose the automated checks pass, but the test only asserts that a preview panel is visible. That gives you evidence for the first row. A handler could still leave keyboard focus on a toolbar button when the writer returns. Keep the second row open. In the **same task**, ask:

> Which check exercises typing after returning from preview? Show me the assertion and its result. If the existing tests only cover panel visibility, tell me exactly what to try in the browser.

A failed check belongs in the PR too. Give the command, the failure, and whether it also occurs on the starting revision if you verified that. When the environment cannot run a check, name the missing prerequisite so a colleague can finish it. [OpenAI’s worked example of reviewing test evidence](https://learn.chatgpt.com/use-cases/issue-to-tested-pr)

## 3. Open a draft PR for review

When the diff matches your request, use the task’s PR action or ask Codex in the same task:

> Open a draft pull request from this working branch into the agreed target branch. Include the reason for the change, the checks we ran, their results, and the remaining keyboard check. Leave the merge to the reviewer. Return the PR link.

If the integration can push a branch but cannot open the PR, open that branch in GitHub, choose **Compare & pull request**, verify the base repository and branch, and select **Create draft pull request** from the creation dropdown. For a class exercise in a fork, double-check that the base points to the class or personal fork.

Open the PR link yourself. Read **Files changed** and compare the PR description with the evidence you collected. Then give your reviewer one focused request: “Please try typing immediately after returning from preview in the browser you normally use.” A draft is a useful place for that early feedback. When the remaining work is resolved, select **Ready for review**, obtain the approvals and CI results your repository requires, and have an authorized maintainer merge. [GitHub’s guide to draft PRs](https://docs.github.com/en/pull-requests/how-tos/create-pull-requests/changing-the-stage-of-a-pull-request)

## 4. Give Codex your team’s instructions

After the first PR, notice which instructions you would give the next contributor. “Use this particular shortcut” belongs in the issue. “Update the user guide whenever a keyboard interaction changes” belongs in the repository.

Add a small section to the root `AGENTS.md` in a follow-up PR, or extend an existing section. Use the actual filenames and check commands for your project. For an editor with two desktop manuals, the standing instructions might read:

```markdown
## Changes to keyboard interactions

- When a user-facing shortcut changes, update the affected entries in
  manual.md (English) and manual-ja.md (Japanese) in the same PR.
- Copy key combinations and menu labels from the implementation.
- In the PR, identify the checks you ran and their results. For a keyboard
  check that needs a person, give the starting view, keys, and expected result.
```

Ask a teammate to read those lines. Could they use them to review the next shortcut change, even if they never saw this task? Keep the rules that help them decide. Codex reads applicable project instructions when it starts work, so a fresh task on the updated branch is a good place to try the rule. [How Codex reads AGENTS.md](https://learn.chatgpt.com/docs/agent-configuration/agents-md)

## 5. Keep code and multilingual docs in sync

Reopen the two manual passages in your preview PR. Starting from the English instructions, write down what view the user starts in, what they press, what they see, and how they get back. Repeat with the Japanese instructions. Both paths should take a reader through the same interaction. Each author can choose wording that sounds natural in their language.

For example, “Press the shortcut again to return to editing” gives the wrong instruction if the second press opens a larger preview. Someone who compares only the key names could approve both translations and miss the problem. Walk through the documented sequence once against the PR revision and record what each press does.

When a feature changes, include the affected manuals in the feature PR so the reviewer can inspect behavior and wording together. If a released feature already works and only one translation has drifted, a small documentation PR is easier to review. In projects that also ship an iPad guide, check which platforms the change affects before editing device-specific instructions.

## Field reference: Resume work and troubleshoot setup

| What you see | What to check or do |
| --- | --- |
| You want to pick up on another device | Sign in to the same account and reopen the original cloud task. On mobile, choose an existing environment for new work. Create environments on web or desktop. |
| A teammate cannot see your edits | Share the GitHub branch or draft PR with the teammate and confirm their repository access. A shared environment supplies a starting setup for separate tasks. |
| Your repository is missing from the picker | Check the connected GitHub account, the integration’s repository access, and your own permissions for that repository. |
| Setup cannot fetch a dependency | Find the failing command and destination host in the setup report. Check the environment’s allowed hosts and the package registry credentials separately. |
| A new tool works during setup but is missing in your task | Under **Settings → Codex Cloud → Environments**, edit the environment, test the setup, save, and choose **Republish**. Start a fresh task to verify the tool. |
| You need to keep work for a later session | Commit and push the working branch. By default, saved VM state can be recovered for up to seven days from the most recent turn start or task resumption. This window applies to the VM state. |

Republish when the **setup for future tasks** needs to change, such as a new runtime or dependency installation step. For an ordinary edit to a manual, use the repository’s usual PR workflow. [OpenAI’s environment and saved-state reference](https://learn.chatgpt.com/docs/environments/cloud-environments)

## Pair exercise: Hand off the PR

One person prepares the draft PR. The other opens **only the PR link**, reads the diff, and tries the requested check on that revision. For the README exercise, the reviewer follows the new paragraph and records the first point where they have to guess.

The reviewer leaves one comment answering three questions: What changed? What evidence can I verify? What, if anything, still stands between this PR and a merge? If the reviewer needs the original chat to answer, add the missing steps or evidence to the PR description. The next person who opens it will have what they need.
