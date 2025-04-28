---
tags:
  - tutorial
---

Useful links:
- [Git For Dummies YouTube video](https://www.youtube.com/watch?v=mJ-qvsxPHpY)
- [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)

Git and Github are two different things! Unix systems like Linux and Macbooks already have Git, but it must be installed on Windows.

*Git is a memory card for code*

- Just like a video game, you save your progress as you go so that you can *respawn* once you die (nobody was injured in the making of this documentation, maybe)

# Commands
- Initialize a folder with Git

	- `git innit` *install a memory card*

- Choose files to save your progress (staging)

	- `git add file.txt` save a file

	- `git add .` save everything

- Save changes (commit)

	- `git commit -m 'adding files to the repository'`  

- Check saves

	- `git log`

- Load a save

	- Copy the hash from the save log

		- `git checkout [hashcode-here]`


Github = Bitbucket = Gitlab = Website for Git for sharing with others

- `push` is uploading commits to Github repository
- `pull` is downloading updates to a repository from Github

[[Setup a Github Repository]]
# Branches
- A save file for another character/player without affecting the original save!
## Pull Request
- Here is my `branch` with my changes. What do you think?
## Merging
- good changes were made, saved, and committed to a branch--let's merge it into main

| Merge Type   |                 Diagram                 |
| ------------ | :-------------------------------------: |
| Merge        |       ![[git-merge-diagram.png]]        |
| Fast-Forward | ![[git-fast-forward-merge-diagram.png]] |
| Squash       |    ![[git-squash-merge-diagram.png]]    |
| Rebase       |    ![[git-rebase-merge-diagram.png]]    |

*Diagrams from https://lukemerrett.com/different-merge-types-in-git/* 

# Commits
 #underconstruction
[[Resources/Development Environment/Conventional Commits]]
[[Semantic Versioning 2.0.0]]
## Reverting commits

> [!NOTE] [Stack Overflow Discussion](https://stackoverflow.com/questions/42729198/how-can-i-revert-collaborators-changes-in-his-commits-and-keep-my-changes-in-my)
  >We'll use `git log` to determine which commits he did. It's up to you to determine which commit to "stop" at, though.
>
>
>First, `git log` to pull a listing of all of the commits that they've done on a specific branch:
>
>
> `git log --graph --author="Tom" --oneline --decorate --pretty <branch>`
> From that, you can get a list of all of Tom's commits.
>
> Now, you can use `git revert` to specify a range of commits to revert. Suppose that the last commit he did was `ffffff`, and the first he did was `aaaaaa`, you'd write this:
>
>
>`git revert aaaaaa^..ffffff`

Then, to exit the VIM editor in the terminal:
```
type `esc` then `:wq`
```
