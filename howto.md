---
description: '#git, #nextjs, #react'
---

# How To Guides

## How to add an environment variable in a React/NextJS app

* create a file named `.env` in the root folder of your web app (not inside `src` or `app`, instead in the top level folder)
* add the variable in the file
  * in a React app, the name of the environment variable should start with `REACT` , eg: `REACT_MY_KEY=my-value`
  * in a NextJS app, it should start with `NEXT_PUBLIC_`, eg: `NEXT_PUBLIC_MY_KEY=my-value`
* restart the dev server. This is very important - otherwise the new env variable won't be available to the runtime

## How to add a local git repo to GitHub

* go into your folder and say `git init`
* add a `.gitignore` file if you don't have one.
* add the files to the local repo `git add .`
* commit the first set `git commit -m "initial commit`
* name the main branch as "main" `git branch -M main`
* Go to https://github.com and create a new repo.
  * to avoid mistakes, do NOT initialize the repo with README, gitignore and license files. You can add these later.
* Add a remote pointing to the new github repo - `git remote add origin https://github.com/annjose/movie-mosaic.git`
* Push the local to remote - `git push -u origin main` Reference - https://docs.github.com/en/migrations/importing-source-code/using-the-command-line-to-import-source-code/adding-locally-hosted-code-to-github

## How to rewrite git commit history

Situation: You have a git repo (public/private) and you want to change the contents or the commit message of a specific commit. Example: On 5 Jan 2024, you accidentally checked-in the API token for an API (TMDB API) t your public github repo annjose/learn-react and you want to remove that token (i.e delete the line from the file in that commit)

Solution

* read this reference [Git - Rewriting History (git-scm.com)](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History)
* I also asked ChatGPT to give a solution and it gave a concise answer. Pairing that with the git documentation really helped.
* one thing that was not clear in the article above is that **when** to run the command `git commit --amend` - before making the changes in the file or after. The answer is after.
* also, the article seem to indicate that in the command `git rebase -i <commit-sha>`, you should give the SHA of the commit that you want to modify. But in reality, if you do that, it shows the commits AFTER that commit. So you should either give the SHA of the commit that appears _before_ the rogue commit (i.e. the rogue commit's parent) or give `HEAD~2`, `HEAD~3` etc.
* Basically here is how you do it
  * do `git log` and find the rogue commit you want to modify
  * note the SHA of the _parent_ commit of this rogue commit, eg: `f342b1`
  * run the command (in terminal or VS Code terminal) - `git rebase -i f342b1`
  * the terminal will open a vim-like editor and show the commits from the parent commit down to the latest commit in the repo
  * locate the rogue commit in this list and change the first word in that line from `pick` to `edit` (you may have to type `i` to switch to INSERT mode)
  * run `Esc` to exit the INSERT mode and then do `wq` to save the file and exit. If you want to exit without saving, you should do `q!`
  * At any point, if you want to abort this rebase operation, you can do `git rebase --abort`
  * make the changes in the files (remember - git is in a state that it has time-traveled to that rogue commit)
  * after making the changes (modify file, or rename file etc.), stage the changes (VS Code Source Control panel or the command `git add .`)
  * Run your application (app/NodeJS project) and confirm that the new changes are working fine.
  * Now you can commit the new changes by running `git commit --amend` (all the staged changes will be added to the rogue commit now)
  * Now continue with the rebase `git rebase --continue` to change any other commits that were marked with `edit`
  * If there are no more commits marked with `edit`, the terminal will appear normal.
  * when you do `git status` now, it will show that there are x number of changes on local main and the same x number of changes on remote main.
  * So we should push the local changes to remote _forcefully_ by running `git push origin main --force`
  * Now the repo is in good shape. Go to guthub page and confirm that the rogue commit is fixed now

## How to amend the last commit

Situation: You want to amend the last commit you made in a repo Solution

* article reference
* if you want to amend _only the commit message_, do `git commit --amend` The terminal will show a vim-like editor with the commit message at the top. You can update the message (use `i` to go into INSERT mode)
* If you want to amend the _content of the commit_, then _before doing git commit --amend_, make the changes in the local files, then stage them (`git add .`) and then do `git commit --amend`. It will bring up the vim-like editor and show the commit message at the top. You can leave it as is or edit it. Save and Exit (`wq`)
* If you want to amend _only the content and not the commit message_, you can run the command `git commit --amend --no-edit`- it will commit the staged changes without bringing up the vim editor to update the commit message.
* Push the changes to remote (origin) forcefully `git push origin main --force`. (in GitHub desktop app, use the option 'Force push origin' at the top)
