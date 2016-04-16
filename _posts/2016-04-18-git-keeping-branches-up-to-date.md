---
layout: post
title:  "Git: Keeping branches up to date"
date:   2016-04-18
categories: git branching
---

**This article was originally posted as part of [my old
 blog](https://techfortytwo.wordpress.com) on July 30, 2013.**

I have been using git for one and a half years now and I love it. It
seems to support almost any workflow you can think of. I thought that
I will share the top-level work flow that has been working quite well
for me.

At work, we have a central "official" repo that every one on the team
is supposed to push to and pull from. 

We need to keep our local repository up to date with the central repo
and in the same spirit, keep the local feature branches in sync with
the local master. To take concrete examples: 

    # Get the repo
    $ git clone
    # Create a branch for some work
    $ git checkout -b issue12345
    # Commit few times
    
At this point, I would like to sync my master with central repo and in
turn, sync the branch "issue12345" with local master. One way of doing
that would be this: 

    $ git checkout master
    $ git pull
    $ git checkout issue12345
    $ git merge master
    
This will work but has a downside. When ever merge is done, git
creates what is called a merge commit with a default comment like
"Merge remote branch origin/master". This commit would be part of
history and shows up in "git log". But apart from indicating that
merge happened at that point (and keeping the history of merged
branch), it is largely useless and adds considerable noise to the "git
log" output. Just do "git log" and see how many of these messages show
up, effectively drowning valid commits. 

What we want is something similar to "svn update" which just updates
the local working copy and this can be achieved by using git's
"rebase" command. Here is an example: 

    # Sync with remote repo
    $ git pull --rebase origin master
    
This works similar to "git pull" except that a merge commit is not
created. You shouldn't see any conflicts here because your master
branch shouldn't really contain any local changes (they should all be
in other branches). Now to sync a local branch with local master: 

    $ git checkout issue12345
    $ git rebase master
    
A "rebase" here literally means moving the base (the commit where the
branch was created) to the latest commit in master branch so that it
effectively appears as though you created the branch "issue12345" from
master just now. 

I know that there is an almost unending discussion online about "rebase
vs merge" but the above workflow has been working pretty well and in
fact, several other people have adapted the same workflow without any
issues.

Another important requirement to keep the commit history clean and
concise is that the commits in a branch should be squashed before
merging with the master. Usually, I make several small commits in a
day and most of them are there only as a checkpoint. They make no
sense in the long run. So when I am done with the work on a branch, I
use interactive rebase (`git rebase -i`) to combine commits into one or
few commits and also take this opportunity to write a detailed commit
message. 

In conclusion, git supports many different methodologies but it is
important to stick to a simple work flow that keeps the commit history
clean and concise. 
