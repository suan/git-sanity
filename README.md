git-sanity
===============
An extra set of git commands and hooks, particularly helpful in rigid, fork-based, corporate git workflows.

Usage
-----
Simply copy over the scripts you're interested in to somewhere on your `$PATH` (Some scripts depend on others so make sure you don't omit any needed ones). They can then be invoked without the dash, for example: `git update`.

Disclaimer
------------
These commands involve stashing and pushing and are potentially dangerous - make sure you read the instructions first; and try to grok the code a little, so you won't be completely helpless if something goes wrong. ;-)




Commands
--------
### git update [branch]
Pull the latest changes from `master` of an upstream repo into any `<branch>`, then push it to your fork, all **without leaving your curent branch**. If no `<branch>` argument is given, the current branch will be updated.

- Specify which is the upstream remote by doing `git config sanity.updatesource <upstream remote name>` from within your project, or by adding the following to the bottom of your project's .git/config:

    ```
    [sanity]
    updatesource = <upstream remote name>
    ```
  If no `updatesource` is specified, **it will default to 'upstream'**

- You can also specify the remote your fork is at. This is the remote that will be pushed to after you `git update` an untracked branch. Set this via `git config sanity.remote <your fork's remote name>`, or adding this to the `[sanity]` section in your .git/config:

    ```
    remote = <your fork's remote name>
    ```
  If this is not specified, **it defaults to 'origin'**; which should be what you want most of the time.

### git current-branch
Print the name of the current git branch. A very useful way to use this is to setup a very short bash alias like `alias t='git current branch'` in your `.bash_aliases`, so that you can save time by typing commands like ``git push origin `t` ``, instead of `git push origin 123456_some_feature_description`.

### git current-task [-l | --link]
**Depends on**: git current-branch

At work you probably use some form of bug tracking system and have to name your git feature branches with the corresponding task's number, for example, `123456_some_feature_description`, where 123456 is the task ID.

Prints out the task ID based on the current branch name, which you can in turn use to open the current task's webpage, for example. Supported branch-naming formats are as such, where the task ID is within the `<>`:

```
(t|b|bug_|task_|)<1234>(short_description|)
```
##### Options
**-l or --link**: Print out the URL to the task. Beforehand, the URL pattern needs to be configured in your git config with '<>' as a placeholder for the task ID, for example:

```
git config sanity.tasksurl https://acunote.myco.com/tasks/<>
```



Hooks
-----
### append-task-url
**Type (rename to)**: prepare-commit-msg

**Depends On**: git-current-task

Appends the current bugtracker task number, or link if `sanity.taskurl` is specified in your git config (see **git current-task**), to the end of your commit messages.

Caveat: You won't be able to just quit your editor to cancel a commit since the commit message won't be empty. Instead, you'll have to delete the appended task number/link and save the commit message file.


License
-------
git-sanity is distributed under the [BSD License](http://www.opensource.org/licenses/BSD-3-Clause)
