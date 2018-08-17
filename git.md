# Git

### Pull requests search filters

 [https://help.github.com/enterprise/2.10/user/articles/searching-issues-and-pull-requests/](https://help.github.com/enterprise/2.10/user/articles/searching-issues-and-pull-requests/)

**Examples:**

* To view the PRs that were closed with out merging

  ```text
         **is:pr is:unmerged  state:closed**
  ```

* To see PRs that were closed without merging after a specific date
  * is:pr is:unmerged state:closed closed:&gt;2018-04-01

#### Set the Correct Email to GitHub account {#set-the-correct-email-to-github-account}

When you switch between the public github and Intuit github, you may have trouble seeing the correct user associated with the commits. In order to avoid this mismatch, you need to set the correct git user BEFORE you make the commits.

**Command to see the currently configure user**

> git config --global user.email

**Command to get the current git user configure globally**

> git config --global user.email "ann.jose@gmail.com"
>
> git config --global user.email "ann\_jose@intuit.com"

Command to see all local configuration \(can be run only from a git repo\)

> git config --local --list

#### The Best Solution {#the-best-solution}

* Configure the local repos pointing to public GitHub to use Gmail address. Configure global value to be Intuit EMail address
  * > cd ~/dev/GitHub/my-learnings git config --local user.email "ann.jose@gmail.com"
    >
    > git config --global user.email "ann\_jose@intuit.com"

    Result:

    > git config --local user.email ==&gt; ann.jose@gmail.com
    >
    > git config --global user.email ==&gt; ann\_jose@intuit.com

