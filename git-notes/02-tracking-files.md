## Tracking Changes to Files

* Let's create a file called `mars.txt` that contains some notes
about the Red Planet's suitability as a base.
* (We'll use `nano` to edit the file; you can use whatever editor you like.
* In particular, this does not have to be the core.editor you set globally earlier.)

_also create a second file named venus.txt_

~~~ {.bash}
$ nano mars.txt
~~~

Type the text below into the `mars.txt` file:

~~~ {.bash}
Cold and dry, but everything is my favorite color
~~~

`mars.txt` now contains a single line:

~~~ {.bash}
$ ls
~~~

~~~ {.output}
mars.txt
~~~

~~~ {.bash}
$ cat mars.txt
~~~

~~~ {.output}
Cold and dry, but everything is my favorite color
~~~

If we check the status of our project again,
Git tells us that it's noticed the new file:

~~~ {.bash}
$ git status
~~~

~~~ {.output}
# On branch master
#
# Initial commit
#
# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#
#	mars.txt
nothing added to commit but untracked files present (use "git add" to track)
~~~

The "untracked files" message means that there's a file in the directory
that Git isn't keeping track of.

_Now, lets add files that are inside:
On the white board draw a box representing the staging area (index) and
explain that this is where we set up the next snapshot of our project.
Like a photographer in a studio, we're putting together a shot
before we actually snap the picture.
Connect the working area box and the staging box with 'git add'._

_`git add .` This adds __all__ the files in our repository.
But sometimes we only want to add a single file at a time._

We can tell Git that it should do so using `git add`:

~~~ {.bash}
$ git add mars.txt
~~~

and then check that the right thing happened:

~~~ {.bash}
$ git status
~~~

~~~ {.output}
# On branch master
#
# Initial commit
#
# Changes to be committed:
#   (use "git rm --cached <file>..." to unstage)
#
#	new file:   mars.txt
#
~~~


_-- highlight the "Untracked files" section and that git tells you how to add a file to the next commit._

* Git now knows that it's supposed to keep track of `mars.txt`,
but it hasn't yet recorded any changes for posterity as a commit.

_Tell git _"Hey, we want you to remember the way that the files look right now"_._

_On the white board draw a box representing the project history.
Once we take a snapshot of the project that snapshot becomes a permanent reference point in the project's history that we can always go back to.
The history is like a photo album of changes, and each snapshot has a time stamp, the name of the photographer, and a description.
Connect the staging area to the history with `git commit -m "message"`.
In order to save a snapshot of the current state (revision) of the repository, we use the commit command.
This command is always associated with a message describing the changes since the last commit and indicating their purpose.
Git will ask you to add a commit message.
This is just to remind you what changes you made.
Informative commit messages will serve you well someday, so make a habit of never committing changes without at least a full sentence description._

__ADVICE: Commit often__

_In the same way that it is wise to often save a document that you are working on, so too is it wise to save numerous revisions of your code.
More frequent commits increase the granularity of your undo button._

__ADVICE: Good commit messages__

[because it's important!](http://www.commitlogsfromlastnight.com/)
_There are no hard and fast rules, but good commits are atomic: they are the smallest change that remain meaningful.
A good commit message usually contains a one-line description followed by a longer explanation if necessary.
For code, it's useful to commit changes that can be reviewed by someone in under an hour.
Or it can be useful to commit changes that "go together" - for example, one paragraph of a manuscript, or each new function added to your script.

For example, if you work on your code all day long (add 200 lines of code, including 5 new functions and write 7 pages of your new manuscript including deleting an old paragraph), and at 3:00 you make a fatal error or deletion, but you didn't commit once, then you will have a hard time recreating the version you are looking for - because it doesn't exist!_


To get it to do that,
we need to run one more command:

~~~ {.bash}
$ git commit -m "Starting to think about Mars"
~~~

~~~ {.output}
[master (root-commit) f22b25e] Starting to think about Mars
 1 file changed, 1 insertion(+)
 create mode 100644 mars.txt
~~~

When we run `git commit`,
Git takes everything we have told it to save by using `git add`
and stores a copy permanently inside the special `.git` directory.
This permanent copy is called a [revision](../../gloss.html#revision)
and its short identifier is `f22b25e`.
(Your revision may have another identifier.)

We use the `-m` flag (for "message")
to record a comment that will help us remember later on what we did and why.
If we just run `git commit` without the `-m` option,
Git will launch `nano` (or whatever other editor we configured at the start)
so that we can write a longer message.

__ADVICE:__ _You must have a commit message. It's good practice and git won't let you commit without one._

_If you only want to add one file, use `git commit filename.txt -m "message"
`git commit -am "message` will add ALL tracked files._

If we run `git status` now:

~~~ {.bash}
$ git status
~~~

~~~ {.output}
# On branch master
nothing to commit, working directory clean
~~~

it tells us everything is up to date.
If we want to know what we've done recently,
we can ask Git to show us the project's history using `git log`.
You can see all the changes you have ever made using this command:

~~~ {.bash}
$ git log
~~~

~~~ {.output}
commit f22b25e3233b4645dabd0d81e651fe074bd8e73b
Author: Vlad Dracula <vlad@tran.sylvan.ia>
Date:   Thu Aug 22 09:51:46 2013 -0400

    Starting to think about Mars
~~~

`git log` lists all revisions  made to a repository in reverse chronological order.
The listing for each revision includes
the revision's full identifier
(which starts with the same characters as
the short identifier printed by the `git commit` command earlier),
the revision's author,
when it was created,
and the log message Git was given when the revision was created.

> #### Where Are My Changes?
>
> If we run `ls` at this point, we will still see just one file called `mars.txt`.
> That's because Git saves information about files' history
> in the special `.git` directory mentioned earlier
> so that our filesystem doesn't become cluttered
> (and so that we can't accidentally edit or delete an old version).

### Changing a File

Now suppose Dracula adds more information to the file.
(Again, we'll edit with `nano` and then `cat` the file to show its contents;
you may use a different editor, and don't need to `cat`.)

~~~ {.bash}
$ nano mars.txt
$ cat mars.txt
~~~

~~~ {.output}
Cold and dry, but everything is my favorite color
The two moons may be a problem for Wolfman
~~~

When we run `git status` now,
it tells us that a file it already knows about has been modified:

~~~ {.bash}
$ git status
~~~

~~~ {.output}
# On branch master
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#
#	modified:   mars.txt
#
no changes added to commit (use "git add" and/or "git commit -a")
~~~

The last line is the key phrase:
"no changes added to commit".
We have changed this file,
but we haven't told Git we will want to save those changes
(which we do with `git add`)
much less actually saved them.
Let's double-check our work using `git diff`,
which shows us the differences between
the current state of the file
and the most recently saved version:

~~~ {.bash}
$ git diff
~~~

~~~ {.output}
diff --git a/mars.txt b/mars.txt
index df0654a..315bf3a 100644
--- a/mars.txt
+++ b/mars.txt
@@ -1 +1,2 @@
 Cold and dry, but everything is my favorite color
+The two moons may be a problem for Wolfman
~~~

The output is cryptic because
it is actually a series of commands for tools like editors and `patch`
telling them how to reconstruct one file given the other.
If we can break it down into pieces:

1.  The first line tells us that Git is producing output similar to the Unix `diff` command
    comparing the old and new versions of the file.
2.  The second line tells exactly which [revisions](../../gloss.html#revision) of the file
    Git is comparing;
    `df0654a` and `315bf3a` are unique computer-generated labels for those revisions.
3.  The remaining lines show us the actual differences
    and the lines on which they occur.
    In particular,
    the `+` markers in the first column show where we are adding lines.

Let's commit our change:

~~~ {.bash}
$ git commit -m "Concerns about Mars's moons on my furry friend"
~~~

~~~ {.output}
# On branch master
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#
#	modified:   mars.txt
#
no changes added to commit (use "git add" and/or "git commit -a")
~~~

Whoops:
Git won't commit because we didn't use `git add` first.
Let's fix that:

~~~ {.bash}
$ git add mars.txt
$ git commit -m "Concerns about Mars's moons on my furry friend"
~~~

~~~ {.output}
[master 34961b1] Concerns about Mars's moons on my furry friend
 1 file changed, 1 insertion(+)
~~~

Git insists that we add files to the set we want to commit
before actually committing anything
because we may not want to commit everything at once.
For example,
suppose we're adding a few citations to our supervisor's work
to our thesis.
We might want to commit those additions,
and the corresponding addition to the bibliography,
but *not* commit the work we're doing on the conclusion
(which we haven't finished yet).

To allow for this,
Git has a special staging area
where it keeps track of things that have been added to
the current [change set](../../gloss.html#change-set)
but not yet committed.
`git add` puts things in this area,
and `git commit` then copies them to long-term storage (as a commit):

<img src="img/git-staging-area.svg" alt="The Git Staging Area" />

Let's watch as our changes to a file move from our editor
to the staging area
and into long-term storage.
First,
we'll add another line to the file:

~~~ {.bash}
$ nano mars.txt
$ cat mars.txt
~~~

~~~ {.output}
Cold and dry, but everything is my favorite color
The two moons may be a problem for Wolfman
But the Mummy will appreciate the lack of humidity
~~~

~~~ {.bash}
$ git diff
~~~

~~~ {.output}
diff --git a/mars.txt b/mars.txt
index 315bf3a..b36abfd 100644
--- a/mars.txt
+++ b/mars.txt
@@ -1,2 +1,3 @@
 Cold and dry, but everything is my favorite color
 The two moons may be a problem for Wolfman
+But the Mummy will appreciate the lack of humidity
~~~

So far, so good:
we've added one line to the end of the file
(shown with a `+` in the first column).
Now let's put that change in the staging area
and see what `git diff` reports:

~~~ {.bash}
$ git add mars.txt
$ git diff
~~~

There is no output:
as far as Git can tell,
there's no difference between what it's been asked to save permanently
and what's currently in the directory.
However,
if we do this:

~~~ {.bash}
$ git diff --staged
~~~

~~~ {.output}
diff --git a/mars.txt b/mars.txt
index 315bf3a..b36abfd 100644
--- a/mars.txt
+++ b/mars.txt
@@ -1,2 +1,3 @@
 Cold and dry, but everything is my favorite color
 The two moons may be a problem for Wolfman
+But the Mummy will appreciate the lack of humidity
~~~

it shows us the difference between
the last committed change
and what's in the staging area.
Let's save our changes:

~~~ {.bash}
$ git commit -m "Thoughts about the climate"
~~~

~~~ {.output}
[master 005937f] Thoughts about the climate
 1 file changed, 1 insertion(+)
~~~

check our status:

~~~ {.bash}
$ git status
~~~

~~~ {.output}
# On branch master
nothing to commit, working directory clean
~~~

and look at the history of what we've done so far:

~~~ {.bash}
$ git log
~~~

~~~ {.output}
commit 005937fbe2a98fb83f0ade869025dc2636b4dad5
Author: Vlad Dracula <vlad@tran.sylvan.ia>
Date:   Thu Aug 22 10:14:07 2013 -0400

    Thoughts about the climate

commit 34961b159c27df3b475cfe4415d94a6d1fcd064d
Author: Vlad Dracula <vlad@tran.sylvan.ia>
Date:   Thu Aug 22 10:07:21 2013 -0400

    Concerns about Mars's moons on my furry friend

commit f22b25e3233b4645dabd0d81e651fe074bd8e73b
Author: Vlad Dracula <vlad@tran.sylvan.ia>
Date:   Thu Aug 22 09:51:46 2013 -0400

    Starting to think about Mars
~~~

_Useful `git log` flags:_

* -3 (shows only the 3 most recent commits)
* --oneline (condenses each log into a single line, for quicker scanning)
* --stat (gives more details for each commit, ++--)
* --since=X.minutes/hours/days/weeks/months/years or YY-MM-DD-HH:MM (for specific time frames)
* --author=<pattern> (look for specific people)

To recap, when we want to add changes to our repository,
we first need to add the changed files to the staging area
(`git add`) and then commit the staged changes to the
repository (`git commit`):

<img src="img/git-committing.svg" alt="The Git Commit Workflow" />

### Exploring History

If we want to see what we changed when,
we use `git diff` again,
but refer to old versions
using the notation `HEAD~1`, `HEAD~2`, and so on:

~~~ {.bash}
$ git diff HEAD~1 mars.txt
~~~

~~~ {.output}
diff --git a/mars.txt b/mars.txt
index 315bf3a..b36abfd 100644
--- a/mars.txt
+++ b/mars.txt
@@ -1,2 +1,3 @@
 Cold and dry, but everything is my favorite color
 The two moons may be a problem for Wolfman
+But the Mummy will appreciate the lack of humidity
~~~

~~~ {.bash}
$ git diff HEAD~2 mars.txt
~~~

~~~ {.output}
diff --git a/mars.txt b/mars.txt
index df0654a..b36abfd 100644
--- a/mars.txt
+++ b/mars.txt
@@ -1 +1,3 @@
 Cold and dry, but everything is my favorite color
+The two moons may be a problem for Wolfman
+But the Mummy will appreciate the lack of humidity
~~~

_Useful git diff flags_

* `git diff --stat` gives us a summary of the filename and number of insertions/deletions
* `git diff -- filename` looks at the differences for a specific file

In this way,
we build up a chain of revisions.
The most recent end of the chain is referred to as `HEAD`;
we can refer to previous revisions using the `~` notation,
so `HEAD~1` (pronounced "head minus one")
means "the previous revision",
while `HEAD~123` goes back 123 revisions from where we are now.

We can also refer to revisions using
those long strings of digits and letters
that `git log` displays.
These are unique IDs for the changes,
and "unique" really does mean unique:
every change to any set of files on any machine
has a unique 40-character identifier.
Our first commit was given the ID
f22b25e3233b4645dabd0d81e651fe074bd8e73b,
so let's try this:

~~~ {.bash}
$ git diff f22b25e3233b4645dabd0d81e651fe074bd8e73b mars.txt
~~~

~~~ {.output}
diff --git a/mars.txt b/mars.txt
index df0654a..b36abfd 100644
--- a/mars.txt
+++ b/mars.txt
@@ -1 +1,3 @@
 Cold and dry, but everything is my favorite color
+The two moons may be a problem for Wolfman
+But the Mummy will appreciate the lack of humidity
~~~

That's the right answer,
but typing random 40-character strings is annoying,
so Git lets us use just the first few:

~~~ {.bash}
$ git diff f22b25e mars.txt
~~~

~~~ {.output}
diff --git a/mars.txt b/mars.txt
index df0654a..b36abfd 100644
--- a/mars.txt
+++ b/mars.txt
@@ -1 +1,3 @@
 Cold and dry, but everything is my favorite color
+The two moons may be a problem for Wolfman
+But the Mummy will appreciate the lack of humidity
~~~

### Recovering Old Versions

_So far, this seems like a lot of work. Why are we keeping track of all these little things??
Let's say you fatally ruin a file during an editing mistake
(like when I deleted an awesome paragraph from my dissertation instead of cutting and pasting it like I meant to.)
Maybe you even accidentally delete an important file (This code is old, why should I keep it?).
If you have version control, you don't need to track down your System Administrator. You can fix your problem easily!_

All right:
we can save changes to files and see what we've changed---how
can we restore older versions of things?
Let's suppose we accidentally overwrite our file:

~~~ {.bash}
$ nano mars.txt
$ cat mars.txt
~~~

~~~ {.output}
We will need to manufacture our own oxygen
~~~

`git status` now tells us that the file has been changed,
but those changes haven't been staged:

~~~ {.bash}
$ git status
~~~

~~~ {.output}
# On branch master
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#
#	modified:   mars.txt
#
no changes added to commit (use "git add" and/or "git commit -a")
~~~

We can put things back the way they were
by using `git checkout`:

~~~ {.bash}
$ git checkout HEAD mars.txt
$ cat mars.txt
~~~

~~~ {.output}
Cold and dry, but everything is my favorite color
The two moons may be a problem for Wolfman
But the Mummy will appreciate the lack of humidity
~~~

As you might guess from its name,
`git checkout` checks out (i.e., restores) an old version of a file.
In this case,
we're telling Git that we want to recover the version of the file recorded in `HEAD`,
which is the last saved revision.

_This would work even if we deleted our file, and wanted to get it back!_
_delete mars.txt, and then show that it can be checked back out_

If we want to go back even further,
we can use a revision identifier instead:

~~~ {.bash}
$ git checkout f22b25e mars.txt
~~~

It's important to remember that
we must use the revision number that identifies the state of the repository
*before* the change we're trying to undo.
A common mistake is to use the revision number of
the commit in which we made the change we're trying to get rid of.
In the example below, we want retrieve the state from before the most
recent commit (`HEAD~1`), which is revision `f22b25e`:

<img src="img/git-checkout.svg" alt="Git Checkout" />

The following diagram illustrates what the history of a file might look
like (moving back from `HEAD`, the most recently committed version):

<img src="img/git-when-revisions-updated.svg" alt="When Git Updates Revision Numbers" />

> #### Simplifying the Common Case
>
> If you read the output of `git status` carefully,
> you'll see that it includes this hint:
>
> ~~~ {.bash}
> (use "git checkout -- <file>..." to discard changes in working directory)
> ~~~
>
> As it says,
> `git checkout` without a version identifier restores files to the state saved in `HEAD`.
> The double dash `--` is needed to separate the names of the files being recovered
> from the command itself:
> without it,
> Git would try to use the name of the file as the revision identifier.

The fact that files can be reverted one by one
tends to change the way people organize their work.
If everything is in one large document,
it's hard (but not impossible) to undo changes to the introduction
without also undoing changes made later to the conclusion.
If the introduction and conclusion are stored in separate files,
on the other hand,
moving backward and forward in time becomes much easier.
Or for your code, if you store functions in files separate from code that executes them, or makes figures,
you can go back in time to find or retrieve specific chunks.

### Ignoring Things

What if we have files that we do not want Git to track for us,
like backup files created by our editor
or intermediate files created during data analysis.

_while git can keep track of data files, this is often not a great idea.
Share story of .rdata files in collaborative project. Why they needed to be in the .git ignore file_

Let's create a few dummy files:

~~~ {.bash}
$ mkdir results
$ touch a.dat b.dat c.dat results/a.out results/b.out
~~~

and see what Git says:

~~~ {.bash}
$ git status
~~~

~~~ {.output}
# On branch master
# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#
#	a.dat
#	b.dat
#	c.dat
#	results/
nothing added to commit but untracked files present (use "git add" to track)
~~~

_Note: if you already added these files (git add .) you can unstage them by typing git reset HEAD_

Putting these files under version control would be a waste of disk space.
What's worse,
having them all listed could distract us from changes that actually matter,
so let's tell Git to ignore them.

We do this by creating a file in the root directory of our project called `.gitignore`.

~~~ {.bash}
$ nano .gitignore
$ cat .gitignore
~~~

~~~ {.output}
*.dat
results/
~~~

These patterns tell Git to ignore any file whose name ends in `.dat`
and everything in the `results` directory.
(If any of these files were already being tracked,
Git would continue to track them.)

Once we have created this file,
the output of `git status` is much cleaner:

~~~ {.bash}
$ git status
~~~

~~~ {.output}
# On branch master
# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#
#	.gitignore
nothing added to commit but untracked files present (use "git add" to track)
~~~

The only thing Git notices now is the newly-created `.gitignore` file.
You might think we wouldn't want to track it,
but everyone we're sharing our repository with will probably want to ignore
the same things that we're ignoring.
Let's add and commit `.gitignore`:

~~~ {.bash}
$ git add .gitignore
$ git commit -m "Add the ignore file"
$ git status
~~~

~~~ {.output}
# On branch master
nothing to commit, working directory clean
~~~

As a bonus,
using `.gitignore` helps us avoid accidentally adding files to the repository that we don't want.

~~~ {.bash}
$ git add a.dat
~~~

~~~ {.output}
The following paths are ignored by one of your .gitignore files:
a.dat
Use -f if you really want to add them.
fatal: no files added
~~~

If we really want to override our ignore settings,
we can use `git add -f` to force Git to add something.
We can also always see the status of ignored files if we want:

~~~ {.bash}
$ git status --ignored
~~~

~~~ {.output}
# On branch master
# Ignored files:
#  (use "git add -f <file>..." to include in what will be committed)
#
#        a.dat
#        b.dat
#        c.dat
#        results/

nothing to commit, working directory clean
~~~

_To discard all your most recent changes and GO BACK IN TIME,
first look at your `git log` to decide what version you want to go back to.
Remember the first 5-7 digits in the commit code of the version that wasn't screwed up._

_use `git reset --hard versioncode`_

_To roll back to a specific file, use
`git checkout version name --filename`_

_To roll back one version (usually I know that I messed up pretty quickly)
`git checkout master~1 PathToFile`_


_A short exercise to show moving back and forth. If I mess up and I notice right away,
 might want to go back in time quickly. Commit some changes to `mars.txt`.
 I can return to the previous version by typing `git checkout master~1 mars.txt`, and then
 committing those changes with a message like "I deleted the thing I just added".
 This will preserve your entire history, including the short-lived mistake, which will allow
 you to return to it if you should decide it wasn't a mistake at all.
 If you check out the entire repository using `git checkout master~1` you will be in
 "detached head state". This can be quickly remedied by typing `git checkout master`, to return
 you to the correct place. Detached head is when the head is not the same version as the master._


> ### Key Points {.objectives}
>
> *   Use `git config` to configure a user name, email address, editor, and other preferences once per machine.
> *   `git init` initializes a repository.
> *   `git status` shows the status of a repository.
> *   Files can be stored in a project's working directory (which users see),
>     the staging area (where the next commit is being built up)
>     and the local repository (where snapshots are permanently recorded).
> *   `git add` puts files in the staging area.
> *   `git commit` creates a snapshot of the staging area in the local repository.
> *   Always write a log message when committing changes.
> *   `git diff` displays differences between revisions.
> *   `git checkout` recovers old versions of files.
> *   The `.gitignore` file tells Git what files to ignore.

> ### Challenge {.challange}
>
> Create a new Git repository on your computer called `bio`.
> Write a three-line biography for yourself in a file called `me.txt`,
> commit your changes,
> then modify one line and add a fourth and display the differences
> between its updated state and its original state.

> ### Challenge {.challenge}
>
> The following sequence of commands creates one Git repository inside another:
>
> ~~~ {.bash}
> cd           # return to home directory
> mkdir alpha  # make a new directory alpha
> cd alpha     # go into alpha
> git init     # make the alpha directory a Git repository
> mkdir beta   # make a sub-directory alpha/beta
> cd beta      # go into alpha/beta
> git init     # make the beta sub-directory a Git repository
> ~~~
>
>
> Why is it a bad idea to do this?