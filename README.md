git-sanity
===============
An extra set of git commands, particularly helpful in dealing with github-fork workflows.

Usage
-----
Simply copy over the scripts you're interested in to somewhere on your `$PATH`. They can then be invoked without the dash, for example: `git update`.

Disclaimer (Don't sue me)!!
------------
These commands involve stashing and pushing and are potentially dangerous - make sure you read the instructions first; and try to grok the code a little, so you won't be completely helpless if something goes wrong. ;-)




Commands
========

git update \<branch\>
---------------------
Pull the latest changes from `master` of an upstream repo into any `<branch>`, then push it to your fork, all **without leaving your curent branch**.

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
