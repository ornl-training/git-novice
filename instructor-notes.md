---
title: Instructor Notes
---

Using a software tool to handle the versions of your project files
lets you focus on the more interesting/innovative aspects of your project.

- Version control's advantages
  - It's easy to set up
  - Every copy of a Git repository is a full backup of a project and its history
  - A few easy-to-remember commands are all you need for most day-to-day version control tasks
  - The [GitHub][github] hosting service provides a web-based collaboration service
- Two main concepts
  - *commit*: a recorded set of changes in your project's files
  - *repository*: the history of all your project's commits
- Why use GitHub?
  - No need for a server: easy to set up
  - GitHub's strong community: your colleagues are probably already there

## Overall

Version control might be the most important topic we teach, but Git is
definitely the most complicated tool.  However, GitHub presently dominates the
open software repository landscape, so the time and effort required to teach
fundamental Git is justified and worthwhile.

Because of this complexity, we don't teach novice learners about many
interesting topics, such as branching, hashes, and commit objects.

Instead we try to convince them that version control is useful for researchers
working in teams or not, because it is

- a better way to "undo" changes,
- a better way to collaborate than mailing files back and forth, and
- a better way to share your code and other scientific work with the world.

## Teaching Notes

- You can "split" your shell so that recent commands remain in view using [this](https://github.com/rgaiacs/swc-shell-split-window) script.

- Make sure the network is working *before* starting this lesson.

- Drawings are particularly useful in this lesson: if you have a whiteboard,
  [use it][drawings]!

- Version control is usually not the first subject in a workshop,
  so get learners to create a GitHub account after the session before.
  Remind learners that the username and email they use for GitHub (and setup
  during Git configuration) will be viewable to the public by default.
  However, there are many reasons why a learner may not want their personal
  information viewable, and GitHub has [resources for keeping an email address
  private][github-privacy].

- If some learners are using Windows, there will inevitably be issues
  merging files with different line endings.  (Even if everyone's on
  some flavor of Unix, different editors may or may not add a
  newline to the last line of a file.) Take a moment to explain
  these issues, since learners will almost certainly trip over them
  again.  If learners are running into line ending problems, GitHub
  has a [page][github-line-endings] that helps with troubleshooting.
  Specifically, the [section on refreshing a repository][github-line-endings-refresh]
  may be helpful if learners need to change the `core.autocrlf` setting
  after already having made one or more commits.

- We don't use a Git GUI in these notes because we haven't found one that
  installs easily and runs reliably on the three major operating systems, and
  because we want learners to understand what commands are being run.  That
  said, instructors should demo a GUI on their desktop at some point during
  this lesson and point learners at [this page][github-gui].

- Instructors should show learners graphical diff/merge tools like
  [DiffMerge][diffmerge].

- When appropriate, explain that we teach Git rather than CVS, Subversion, or
  Mercurial primarily because of GitHub's growing popularity: CVS and
  Subversion are now seen as legacy systems, and Mercurial isn't nearly as
  widely used in the sciences right now.

- Further resources:

  - [git-it] is a self-paced command-line Git demo,
    with [git-it-electron] its GitHub Desktop successor.
  - [Code School][code-school] has a free interactive course, [Try Git][try-git].
  - for instructors, [the Git parable][git-parable] is useful background reading

## [Automated Version Control](../episodes/01-basics.md)

- Ask, "Who uses 'undo' in their editor?" All say "Me". 'Undo' is the simplest
  form of version control.

- Give learners a five-minute overview of what version control does for them
  before diving into the watch-and-do practicals.  Most of them will have
  tried to co-author papers by emailing files back and forth, or will have
  biked into the office only to realize that the USB key with last night's
  work is still on the kitchen table.  Instructors can also make jokes about
  directories with names like "final version", "final version revised",
  "final version with reviewer three's corrections", "really final version",
  and, "come on this really has to be the last version" to motivate version
  control as a better way to collaborate and as a better way to back work up.

## [Setting Up Git](../episodes/02-setup.md)

- We suggest instructors and students use `nano` as the text editor for this
  lessons because

  - it runs in all three major operating systems,
  - it runs inside the shell (switching windows can be confusing to students), and
  - it has shortcut help at the bottom of the window.

  Please point out to students during setup that they can and should use
  another text editor if they're already familiar with it.

- When setting up Git, be very clear what learners have to enter: it is
  common for them to edit the instructor's details (e.g. email).  Check at
  the end using `git config --list`.

- When setting up the default branch name, if learners have a Git version
  older than 2.28, the default branch name can be changed for the lesson
  using `git branch -M main` if there are currently commits in the repository,
  or `git checkout -b main` if there are no commits/the repository is completely empty.

## [Creating a Repository](../episodes/03-create.md)

- When you do `git status`, Mac users may see a `.DS_Store` file showing as
  untracked. This a file that Mac OS creates in each directory.

- The challenge "Places to create repositories" tries to reinforce the idea
  that the `.git` folder contains the whole Git repo and deleting this folder
  undoes a `git init`. It also gives the learner the way to fix the common
  mistake of putting unwanted folders (like `Desktop`) under version control.

  Instead of removing the `.git` folder directly, you can choose to move it
  first to a safer directory and remove it from there:

  ```bash
  $ mv .git temp_git
  $ rm -rf  temp_git
  ```

  The challenge suggests that it is a bad idea to create a Git repo inside another repo.
  For more discussion on this topic, please see [this issue][repos-in-repos].

## [Tracking Changes](../episodes/04-changes.md)

- It's important that learners do a full commit cycle by themselves (make
  changes, `git diff`, `git add`, and `git commit`). The "`bio` repository"
  challenge does that.

- This is a good moment to show a diff with a graphical diff tool. If you
  skip it because you're short on time, show it once in GitHub.

- One thing may cause confusion is recovering old versions.  If, instead of
  doing `$ git checkout f22b25e guacamole.md`, someone does `$ git checkout f22b25e`, they wind up in the "detached HEAD" state and confusion abounds.
  It's then possible to keep on committing, but things like `git push origin main` a bit later will not give easily comprehensible results.  It also
  makes it look like commits can be lost.  To "re-attach" HEAD, use
  `git checkout main`.

- This is a good moment to show a log within a Git GUI. If you skip it
  because you're short on time, show it once in GitHub.

## [Exploring History](../episodes/05-history.md)

- Git 2.23 (August 2019) added the `git restore` command as a clearer, more verbose replacement for the heavily overloaded `git checkout` when you wish to restore files into the working tree. The older style `git checkout -- file` does still work in newer versions of Git. This is an illustration of the fact that there are often multiple ways to do the same thing in Git.

## [Ignoring Things](../episodes/06-ignore.md)

Just remember that you can use wildcards and regular expressions to ignore a
particular set of files in `.gitignore`.

## [Remotes in GitLab](../episodes/07-gitlab.md)

- Make it clear that Git and GitLab are not the same thing: Git is an open
  source version control tool, GitLab is a company that hosts Git
  repositories in the web and provides a web interface to interact with repos
  they host.

- It is very useful to draw a diagram showing the different repositories
  involved.

- When pushing to a remote, the output from Git can vary slightly depending on
  what leaners execute. The lesson displays the output from git if a learner
  executes `git push origin main`. However, some learners might use syntax
  suggested by GitHub for pushing to a remote with an existing repository,
  which is `git push -u origin main`. Learners using syntax from GitLab,
  `git push -u origin main`, will have slightly different output, including
  the line `Branch main set up to track remote branch main from origin by rebasing.`

[github]: https://github.com/
[drawings]: https://marklodato.github.io/visual-git-guide/index-en.html
[github-privacy]: https://help.github.com/articles/keeping-your-email-address-private/
[github-line-endings]: https://docs.github.com/en/github/using-git/configuring-git-to-handle-line-endings
[github-line-endings-refresh]: https://docs.github.com/en/github/using-git/configuring-git-to-handle-line-endings#refreshing-a-repository-after-changing-line-endings
[github-gui]: https://git-scm.com/downloads/guis
[diffmerge]: https://sourcegear.com/diffmerge/
[git-it]: https://github.com/jlord/git-it
[git-it-electron]: https://github.com/jlord/git-it-electron
[code-school]: https://www.codeschool.com/
[try-git]: https://try.github.io
[git-parable]: https://tom.preston-werner.com/2009/05/19/the-git-parable.html
[repos-in-repos]: https://github.com/swcarpentry/git-novice/issues/272
[cc-faq-software]: https://creativecommons.org/faq/#can-i-apply-a-creative-commons-license-to-software



