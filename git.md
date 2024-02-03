# 🔀 Git

### Good Articles

* Simple list of git commands - [https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* Git Rebase - [https://jeffkreeftmeijer.com/git-rebase/](https://jeffkreeftmeijer.com/git-rebase/)

### How to Use Pull requests search filters

&#x20;Source: [https://help.github.com/enterprise/2.10/user/articles/searching-issues-and-pull-requests/](https://help.github.com/enterprise/2.10/user/articles/searching-issues-and-pull-requests/)

*   To view the PRs that were closed with out merging

    `is:pr is:unmerged state:closed`
*   To see PRs that were closed without merging after a specific date

    `is:pr is:unmerged state:closed closed:>2018-04-01`

## How to Set the Correct Email to GitHub account

When you switch between the public github and Intuit github, you may have trouble seeing the correct user associated with the commits. In order to avoid this mismatch, you need to set the correct git user BEFORE you make the commits.

**Command to see the currently configure user**

```sh
git config --global user.email
```

Replace `user.email` with your actual email address like so: `git config --global user.email "your_email@example.com"`.

**Command to see all local configuration (can be run only from a git repo)**

```sh
git config --local --list
```

### The Best Solution <a href="#the-best-solution" id="the-best-solution"></a>

Configure the local repos pointing to public GitHub to use Gmail address. Configure global value to be corporate email address. (Or the other way around)

```sh
cd ~/dev/GitHub/my-learnings git config --local user.email <your-pers-email>
git config --global user.email <your-corp-email>
```

#### Result:

```sh
git config --local user.email ==> your-pers-email
git config --global user.email ==> your-corp-email
```
