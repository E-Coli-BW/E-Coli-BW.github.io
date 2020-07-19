---
layout: post
title:  "Git common operations"
date:   2020-07-19 00:15:07 -0400
tags: git notes
categories: [git,notes]
---

I've been using Git for a while and apart from the simple "git add .", "git commit -m "blablabla" " and "git push", sometime I do need some other commands aside from these most common ones. Usually I would just google it and copy paste it. However, I found myself doing the same thing quite a lot recently and reckon I do need a deeper understanding on git-related concepts. That's the motivation of this post.


1. Centralized Version Control vs Distributed Version control

    Git is distribured version control, by distributed, we mean each collaborator has its own repo, whereas in centralized vc, you only have one grand repo.

    ![central](/assets/gitConcepts/centralized-vc.png)
    ![distributed](/assets/gitConcepts/distributed-vc.png)

2. fork vs clone

    * To fork is to make a copy of the original repo to your own **repo**

    * To clone is to make a copy of the repo(does not matter if it's your forked one or an original one of yours/others) to your **local machine**

    ![fork](/assets/gitConcepts/fork.png)
    ![clone](/assets/gitConcepts/clone.png)

3. upstream vs origin

    These two are actually just naming conventions for different **remotes**. A remote is just the repo sitting on Github **server**, not the **local** files you have in your laptop.

    Now, what's the difference between these two default **remote**?

    upstream: the **original** repo
    origin: the **forked** repo you are working on

    Now, what if you are the owner and you did not fork anything?
    Then that repo is both the origin(your own fork) **and** the upstream(your own original repo)
    ![upstreams and origin](/assets/gitConcepts/upstreams_and_origin.png)

    **side note**: when you do git fetch, you are fetching from origin(your own repo) by default. To fetch the **original** repo, you need to do git fetch upstream.

4. pull, fetch and merge

    In short: 

    **pull = fetch + merge**

    * merge: as the name suggests, try to combine the two into one, you can think of it as doing a union set operation where it would combine the things in the two repo. However, if in set A and set B they both have a chunk that has the same name but different contents -> conflict!

    * fetch: simply means get sth. from the specified destination, not doing the combine stuff

    Now, when you do pull, it's basically saying: I'm gonna fetch the remote you specified, then do a merge with your local files.

5. How to undo git pull?

    Every now and then, I find myself messed up with the local branch and pulled from the remote but later found out I still prefer the local one. To reset after I wrongly pulled from origin, do

    * git reset --hard HEAD@{1}

    This will discard the result of the git pull I did previously.

6. pull request

    You can push the changes directly into your own repo of course, or if you have the right to push to upstream you can also push directly into upstream. However, a better and safer approach would be send a pull request to the upstream and wait for them to review and approve(ie merge) the changes you made.

    The above explaination also explains why it is called "pull request" : You **request** the repo you wish to make changes into to **pull** your stuff and thus making that change.(merging your changes)

7. rebase vs reset

    In part 5 above, we undo a pull by resetting the head to the previous commit.
    according to [official doc](https://git-scm.com/docs/git-reset)

    * git-reset - Reset current HEAD to the specified state

    from the doc, we see that reset works with **references**, that means, your commit history(and thus the objects relate to commit is **unchanged**). 

    Now take a look at rebase:

    according to [official doc](https://git-scm.com/docs/git-rebase)

    * git-rebase - Reapply commits on top of another base tip

    from the doc, rebase is **actually changing the commit history**

    **in short**

    * git reset --hard {commit-id}: uses a commit in local history

    * git rebase origin/{branch-name}: uses latest commit in the branch(repo)


    **when to use reset?**

    You work on local branch and you messsed up sth but you mistakenly **commit** that -> use **reset**(reusing a local commit)


    **when to use rebase?**

    You simply wish to use the commit your colleauge pushed to the origin(upstream) and **discard your own work** -> use rebase which will **base** your colleague's work(the commit you chose) **on top of your current commit**


    **note**: both reset and rebase **will delete local changes**, so be careful about it

    Personally, I only use rebase when I definitely wish to replace the messy local files with the good old remote branch, and use reset when I have a good old commit of **my own** and I need that commit back.


refs:

1. [pull,fetch vs rebase](https://stackoverflow.com/questions/3357122/git-pull-vs-git-fetch-vs-git-rebase)
2. [git basic concept](https://thepilcrow.net/explaining-basic-concepts-git-and-github/)
3. [origin vs upstream](https://stackoverflow.com/questions/9257533/what-is-the-difference-between-origin-and-upstream-on-github)
4. [how git merge works](https://stackoverflow.com/questions/14961255/how-does-git-merge-work-in-details)
5. [what it means when you fetch and merge](https://stackoverflow.com/questions/3419658/understanding-git-fetch-then-merge)
6. [git rebasing](https://www.atlassian.com/git/tutorials/rewriting-history/git-rebase#:~:text=What%20is%20git%20rebase%3F&text=From%20a%20content%20perspective%2C%20rebasing,them%20to%20the%20specified%20base.)
7. [rebase vs reset](https://stackoverflow.com/questions/11225293/what-is-the-difference-between-git-reset-vs-git-rebase)
