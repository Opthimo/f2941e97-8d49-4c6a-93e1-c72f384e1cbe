<!---
{
  "depends_on": ["https://github.com/STEMgraph/2f4d1f4f-a53b-485e-a290-2da6b69353b2"],
  "author": ["Tabea Röthemeyer","Stephan Bökelmann"],
  "first_used": "2025-04-12",
  "keywords": ["git", "stash", "context-switch"]
}
--->

# Git: Context Switching with `git stash`

## 1) Introduction
In the everyday work of a programmer, it's common to be interrupted or to want to switch context. Maybe you're halfway through implementing a new feature when a bug report comes in and you must fix it on the main branch. But your current work is not finished yet and can't be committed. What now?

That's where `git stash` comes into play. It allows you to save (or *stash*) your current changes away, return to a clean working directory, and restore them later when you're ready.

The command `git stash` creates a temporary, hidden commit with the current changes in your working directory and staging area. When you’re ready to return to your work, `git stash pop` restores those changes and removes them from the stash list.

You can think of it as a clipboard for unfinished work — not permanent, but very handy!

### 1.1) Further Readings and Other Sources
- [Git Stash in the official documentation](https://git-scm.com/book/en/v2/Git-Tools-Stashing-and-Cleaning)
- YouTube: [Git Stash Explained](https://www.youtube.com/watch?v=KLEDKgMmbBI)

## 2) Tasks
1. **Create a new Git repository**: As always, start fresh. Open a terminal, go to your home directory (`cd`), create a new directory and initialize a Git repository there.
2. **Create a new file and make a commit**: Add some dummy text to a file named `notes.txt`. Use the following command if you want to fill it quickly:
```sh
wget -qO- "https://baconipsum.com/api/?type=meat-and-filler&paras=2&format=text" > notes.txt
```
Stage and commit the file.

3. **Make changes without committing**: Open `notes.txt` and change a few lines. Do **not** commit them yet. Just save the file.
4. **Check Git status**: Confirm that your working directory has changes with:
```sh
git status
```
It should show the modified file.

5. **Stash your changes**: Now save your current work using:
```sh
git stash
```
This command will save the changes and revert your working directory to the last commit.

6. **Inspect your stash**: Run `git stash list` to see what was stashed. Use:
```sh
git stash show -p
```
to see the differences stored in your latest stash.

7. **Switch branches**: Create and switch to a new branch where you could theoretically fix some bug:
```sh
git checkout -b bugfix
```
Make some unrelated change (e.g., add a new file or log your fix in `bugfix.txt`) and commit it.

8. **Return to your original work**: Switch back to the default branch. Use `git stash pop` to retrieve your previously stashed changes:
```sh
git checkout main
git stash pop
```
Inspect `notes.txt` and confirm that your old work is back. 

9. **Stash with a message** *(Optional)*: Try this variant:
```sh
git stash push -m "WIP: editing notes.txt"
```
This way, it becomes easier to know what the stash contains later.

## 3) Questions
1. What happens if you have multiple stashes? How can you reapply a specific one?
2. What is the difference between `git stash pop` and `git stash apply`?
3. Can you stash untracked files? What about ignored files? Try it and find out!

## 4) Advice
`git stash` is not a replacement for commits. It’s meant for temporary work, like pausing a task to fix something urgent. It’s a perfect tool for switching tasks, experimenting, or cleaning up your workspace without losing progress. Keep in mind that stashes can be lost if not handled with care — they are not as permanent as commits and can be dropped accidentally. Always check `git stash list` before you trust it’s still there!