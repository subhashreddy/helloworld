# helloworld
first repo 
trying to edit the files and leaerning github.

How to use maven.!!!

Maven Git Convention
This document describes how developers should use Git. The Maven project is in the process of migrating some of its components from svn to git.

Git migration
Information on the migration is here: https://cwiki.apache.org/confluence/display/MAVEN/Git+Migration

Git Configuration
For contributors who are not committers
Apache git repositories are at <<git://git.apache.org>>. However, the ASF uses clones on github.com to make it easier for people to contribute changes via pull requests.

To contribute to a Maven component that is maintained in git, please follow these steps:

create a JIRA for bug or improvement that you wish to work on. The Maven project uses JIRA to organize and track our work, and in particular to keep track of which changes are included in which releases.
Make a fork of the offical ASF clone from github.com. For example, https://github.com/apache/maven-scm.
Make a branch named after your JIRA. This is not required, but it makes it easier for Maven commiters to keep track of your contribution.
Make your changes. As always, unit or integration tests make it much easier for us to accept your changes.
Make a pull request to pull your changes to the offical clone. Add a link to your pull request to the JIRA. Committers will take it from here.
For committers
Committers may, of course, commit directly to the ASF repositories. For complex changes, you may find it valuable to make a pull request at github to make it easier to collaborate with others.

Commit Message Template
Commits should be focused on one issue at a time, because that makes it easier for others to review the commit.

A commit message should use this template:

[ISSUE-1] <<Summary field from JIRA>>
Submitted by: <<Name of non-committer>>
 
o Comments
Where:

ISSUE-1 can be omitted if there was no relevant JIRA issue, though you are strongly encouraged to create one for significant changes.
Submitted by only needs to be specified when a patch is being applied for a non-committer.
Comments some optional words about the solution.
eg:
[MNG-1456] Added the foo to the bar
Submitted by: Baz Bazman
 
o Applied without change
Apply User Patch
To keep the history of contributions clear, The committer should usually apply the patch without any major modifications, and then create his or her own commits for further modifications. However, committers should never commit code to a live branch which is not suitable to release. If a contribution requires significant work to make it useful, commit it to a branch, fix it up, and merge the branch.

If the user created a pull request, the committer is responsible for closing that pull request. You do this by adding a note to a commit message:

  Closes #NNN.
where NNN is the number of the pull request.

Edit Commit Message
to edit last commit comment:
$ git commit --amend -m "new comment"
Workflow
Workflow for svn folks is something like :

 $ git pull
 $ hack hack hack
 $ git push
 // fails, because someone else has already pushed to master
 $ git pull
 // this creates some merges
 $ git push
A more quiet workflow :

$ git pull
$ hack hack hack
$ git push
// fails, because someone else has already pushed to master
$ git fetch
// this moves 'origin/master'
$ git rebase origin/master
// this reapplies your local changes on top of origin/master
$ git push
Other useful Git commands while developing
If you've done a chunk of work and you would like ditch your changes and start from scratch use this command to revert to the original checkout:

$ git checkout .
TODO .gitignore

power-git checkout
This checkout is typical for highly experienced git users, and may serve as inspiration for others; as usual the best way to learn is by doing. Sample shown for maven-surefire

Go to https://github.com/apache/maven-surefire and fork surefire to your own github account.

Starting with nothing (no existing clone)

git clone https://github.com/<youraccount>/maven-surefire.git
git remote add apache https://git-wip-us.apache.org/repos/asf/maven-surefire.git
git remote add asfgithub https://github.com/apache/maven-surefire.git
git config --add remote.asfgithub.fetch "+refs/pull/*/head:refs/remotes/asfgithub/pr/*"
git fetch --all
(You may consider adding --global to the git config statement above to always fetch pull requests for any remote named "asfgithub")

In this setup, running "git push" will normally push to your personal github account. Furthermore, all pull requests from github are also fetched to your local clone, use

gitk --all
to try to make some sense of it all. This is an important command to understand! (gitk may need to be installed additionally)

gitk also has a quite excellent context menu that is far more context sensitive than most people realize at first impression. Right-clicking on a commit in a github pull-request will allow you to cherry-pick straight in the gui.

If you're working on the master branch, you can do stuff like this:

git push # your github account
git push apache # the authorative apache repo
Using your github account as a storage for half-finished work is excellent if you switch between multiple computers, always push to github before leaving your current computer and start by pulling at the next computer.

To merge a pull request

git merge pr/10 # merge pull request number 10 from asf@github into master
git push apache # upload to apache
Or if you're comfortable with rebasing;

git checkout pr/10
git rebase apache/master
git push apache
