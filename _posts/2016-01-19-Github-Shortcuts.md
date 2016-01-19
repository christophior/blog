---
title:  Github shortcuts
date:   2016-01-19
description: quick post about some shortcuts to make daily tasks a bit more efficient
---

Happy Monday everybody! I've really been lacking with the blog posts so I thought I would start this beautiful Monday off with a quick post detailing a quick tip for the day and hopefully after a couple of these i'll start writing more regularly. 

One thing I really believe helps with working efficiently each and every day is having a good setup to be able to do everyday tasks as quickly as possible. Just like every other dev out there I am constantly on my terminal using git and checking out code, switching branches, etcetera. 

Today I just wanted to give everyone a look at some of my git shortcuts ('aliases') and explain maybe 1 or 2 that could really help make things a bit easier for you.

Here's a gist of my .gitconfig (which is usually found in your home directory, '~/.gitconfig') 
https://gist.github.com/christophior/e010ad6777513863ceb7

A pretty interesting shortcut that I have on here that I usually like sharing with people is my **pr** shortcut. This shortcut helps with pulling down pull requests really quickly to test out the changes locally before merging them in.	

```
pr  = "!f() { git fetch -fu ${2:-origin} refs/pull/$1/head:pr/$1 && git checkout pr/$1; }; f"
  
pr-clean = "!git for-each-ref refs/heads/pr/* --format='%(refname)' | while read ref ; do branch=${ref#refs/heads/} ; git branch -D $branch ; done"
```
  
In the code above for the **pr** shortcut we are using origin as the main remote where the PRs are being submitted but you can change that depending on your setup (I usually have upstream as the core repo and origin as my personal fork where I work on features, fixes, etc.). In this case my shortcut would look like:
  
```
pr  = "!f() { git fetch -fu ${2:-upstream} refs/pull/$1/head:pr/$1 && git checkout pr/$1; }; f"
```

## using the pr shortcut

Okay so straight to the point, so once you have the two shortcuts from above in your .gitconfig (since it's nice to have both) all you need to do is get the number of a pull request; for example this PR would be #2 (https://github.com/christophior/JSONConfigurablePersonalSite/pull/2) and run the following:

```
$ git pr 2
From github.com:christophior/JSONConfigurablePersonalSite
* [new ref]         refs/pull/2/head -> pr/2
Switched to branch 'pr/2'
```

I have included the output in the snippet as well, as you can see you have a new branch where you're currently in and you're ready to test out the PR! 

Once you're done all you need to do is switch to a different branch and run **git pr-clean** and you're done, pr-clean will go through your branches and remove any pr branches that you have locally.

```
$ git co develop
Switched to branch 'develop'
Your branch is up-to-date with 'origin/master'.

$ git pr-clean
Deleted branch pr/2 (was 912f69a).
```

That's all folks, let me know how this first blog post went. What should I improve? Should I continue writing posts? Why have I yet to still shower when it's already 9:30am? The world may never know.

Have a good week folks!

## edit: Sorry guys I forgot today was Tuesday, my head's somewhere else. Have a good Tuesday yo!

  
	
	