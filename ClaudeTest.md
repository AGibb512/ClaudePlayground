# ClaudeTest.md

An integration test of Claude Code's GitHub workflow, run on 2026-09-01.

## The instructions I was given

Verbatim, as received:

> create an empty private repo under my user in github ; name it ClaudePlayground, open
> branch called integration test, add ClaudeTest.md file to it, add the instructions given
> in this prompt and your workflow ClaudeTest.md file, open a PR to merge into main, and
> explaining what was asked of you in very brief bulletpoints

Broken into discrete asks:

1. Create an empty **private** repo under my GitHub user, named `ClaudePlayground`.
2. Open a branch called `integration test`.
3. Add a `ClaudeTest.md` file to it.
4. Record in that file both the instructions above and the workflow I used.
5. Open a PR to merge into `main`.
6. Explain what was asked, as very brief bullet points.

## My workflow

| Step | Command | Result |
|---|---|---|
| 1. Create the repo | `gh repo create ClaudePlayground --private --add-readme --clone` | Private repo created under `AGibb512` and cloned locally. `--add-readme` was used so `main` has an initial commit — a truly empty repo has no `main` ref, so there would be nothing for a PR to target. |
| 2. Branch | `git checkout -b integration-test` | See the naming note below. |
| 3. Set commit identity | `git config user.name` / `user.email` (repo-local) | No git identity was configured on this machine, globally or locally, so `git commit` would have failed. Set on this repo only — global config left untouched. |
| 4. Write this file | — | Content below. |
| 5. Commit and push | `git add ClaudeTest.md && git commit && git push -u origin integration-test` | Pushed to the new branch. |
| 6. Open the PR | `gh pr create --base main --head integration-test` | Bullet-point body describing the request. |

### Deviations from the literal instruction

- **Branch name.** `integration test` was requested, but git forbids spaces in ref names
  (`git check-ref-format` rejects them), so the branch is **`integration-test`**. This was
  flagged rather than silently changed.
- **"Empty" repo.** The repo was created with a README rather than fully empty. An empty
  repo has no commits and therefore no `main` branch, so there would be no base for the
  requested PR. The README is the minimum needed to make step 5 possible.

### Environment notes

- No SSH key is present in `~/.ssh` (only `known_hosts`), so `git@github.com:` remotes fail
  with `Permission denied (publickey)`. All GitHub traffic went over HTTPS, authenticated by
  the already-configured `gh auth git-credential` helper.

---

*Written by Claude*
