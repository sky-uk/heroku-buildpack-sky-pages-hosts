# Contributing to the [Hosts Buildpack](https://github.com/sky-uk/heroku-buildpack-sky-pages-hosts)

We greatly appreciate and encourage people contributing back into the Hosts Buildpack.

## Creating Issues

Submit issues to the issue tracker on the [appropriate
repository](https://github.com/sky-uk/heroku-buildpack-sky-pages-hosts#structure) for suggestions,
recommendations, and bugs.

When submitting issues, please make sure you utilise the template provided by
default.

**Please note**: If it’s an issue that’s urgent / you feel you can fix yourself,
please feel free to make some changes and submit a [pull
request](#pull-requests). We’d love to see your contributions.

## Git Workflow

**N.B.** If you fail to adhere to the agreed workflow, there is a risk that your
Pull Requests may not be accepted until any issues are rectified.

### Setting Up Git

We want to set up Git to make our workflow as seamless and automated as
possible. We’re going to configure Git to utilise your preferred text editor
_and_ to use a specific commit message template. Just a couple of things to make
your life a little easier.

```bash
$ cd heroku-buildpack-sky-pages-hosts
# Tell Git to use your preferred text editor (see below):
$ git config core.editor <your editor here>
# Tell Git to prepopulate commit messages with our template
$ git config commit.template ./.github/.git-commit-template
```

**N.B.** You need to be able to open your editor from the CLI. For Atom, replace
`<your editor here>` with `atom --wait`; for VS Code, `code --wait`. For other
text editors, simply Google [_open EDITOR from command
line_](https://www.google.com/search?q=open+EDITOR+from+command+line&oq=open+EDITOR+from+command+line&aqs=chrome..69i57j0l5.6702j0j7&sourceid=chrome&ie=UTF-8).

Now, whenever you run `git commit`, you will be taken to your text editor
(instead of the default, Vim) where you can write your commit messages. Save and
close your editor, and the commit is done.

### Branching Strategy

Hosts Buildpack comprises three main branches:

1. **`master`:** Our release branch that everybody consumes. This branch is the
   one that gets tagged, versioned and deployed to npm.
2. **`develop`:** Our stable branch that we branch from and merge into. This is
   our working branch.
3. **`hbp-#####`:** Our topic branches in which we carry out work. As we will
   learn below, each of these branches is named in reference to a specific
   GitHub issue.

```
                          * hbp-#####
                          |
                          *
             * develop    |
             |\           *
             | \          |
* master     *  \         |
|\           |\  \        *
| \          | \  \       *
|  \         |  \  \      |
|   \        |   \  \     |
|    \       *    \  \    *
|     \      |\    \  \   |
|      \     | \    \  \  |
|       \    |  \    \  \ |
|        \   |   \    \   *
|         \  |    \    \  |
|          \ |     \    \ |
|            *      \     *
|            |       \    *
|            |        \   |
```

`hbp-#####` is branched off `develop` is branched off `master`.

Work in `hbp-#####` is merged into `develop` via a pull request; work in
`develop` is merged into `master` on the command line before rolling an official
release (**Core Maintainers only**).

Nine times out of ten, you will be working in a `hbp-` branch.

#### ghi

Now that branches are named after issue, it’s not as immediately clear what each
branch is responsible for. [ghi](https://github.com/stephencelis/ghi) is a great
little tool that allows you to query GitHub issues from the command line. Let’s
imagine that `git branch` leaves you looking at this:

```bash
$ git branch
  develop
  master
* hbp-00224
  hbp-00220
  hbp-00209
  hbp-00141
```

If I run `ghi 220` I soon find that branch `hbp-00220` relates to issue #220,
_Tabs navigation width issue with many tabs_.

### Committing Workflow

1. Every piece of work should have a corresponding issue on GitHub (e.g.
   `issues/224`).
2. Check out `develop` and ensure you have the latest upstream changes:

        $ cd heroku-buildpack-sky-pages-hosts
        $ git checkout develop
        $ git pull
3. Create a new branch named after your issue:

        $ git checkout -b hbp-00224

   All commits pertaining to this issue must happen within this branch.
4. All commits in this branch should begin with `[refs #00224]`: pad the issue
   number with leading zeroes until you’re at five (5) digits.
    * Instead of running `git commit -m "<message>"`, stage your files as you
      would normally, and run `git commit`. This will fire open your text
      editor with the prepopulated template ready for you to fill out.
6. Now your commits—based on the template—should resemble this:

        commit 1dcf5d4bc18d5fd3321f4c60d879cfd5d5e2dd1f
        Author: Bob Smith <bob@smith.com>
        Date:   Wed, 21 Jun 2017 10:08:36 +0100

            [refs #00224] Add Git workflow documentation

            Though relatively straightforward, our Git workflow is pretty
            involved. I’ve made my best attempt at documenting the setup and
            steps involved in writing compliant commit messages.

### Why?

A more formalised Git strategy means that

1. **We’ll have a nice, clean, respectable public history.** There’s a lot of
   great work in our open source projects; we should be equally proud of our log of it.
2. **Grepping logs for work pertaining to specific issues becomes trivial.** If
   we wanted to see all of the commits that are related to a specific body of
   work, it’s now as simple as:

        $ git log --grep='refs #00235'
3. **We can easily locate work pertaining to an issue by simply matching issue
   numbers to branch names.** Imagine a colleague was working on an issue but
   then suddenly fell ill and you needed to pick up where they left off. Now all
   you have to do is look at the issue number, and checkout its corresponding
   branch. All work becomes centralised and easy to find.

## Pull Requests

1. Create a new local branch for your work.
    * This branch should be named `hbp-<issue numner>`, e.g. `hbp-00215`,
      `hbp-00087`, `hbp-01209`.
2. As early as possible, create a pull request against `develop`. Make sure you
   give enough information in the pull request description (utilising the
   template provided by default), and add the label `in progress` with any other
   appropriate label.
3. Once any conflicts have been fixed and you’re ready for your code to be
   reviewed, remove the `in progress` label and add `reviews needed`.
4. Request a code review from two or more developers.
    * You will need an approvals on the pull request before being
      able to merge.
5. If your PR contains more than a few commits, consider rebasing them into
   something more concise.

   In most cases, another developer won't need to see the entire progress of
   your contribution. Amending your commits will help to keep things tidy and
   support our [Git workflow](#committing-workflow). Simply fixup/squash into a
   sensibly-grouped commit/s.

   For example:
      * **Before**

            13407f8 [refs #00297] Tweak sizing
            c9a0dd1 [refs #00297] Further Amends
            2ffdc23 [refs #00297] Amends
            c21d4eb [refs #00297] Slight tweak
            5471986 Publish

      * In this case, Fixup/Squash your commits via `git rebase -i 5471986`
      * **After**

            c3fee40 [refs #00297] New component
            5471986 Publish

6. One of the [core maintainers](https://github.com/sky-uk/heroku-buildpack-sky-pages-hosts#champions) will merge the changes and apply appropriate
   versioning to release (see below).

---

# [Core Maintainers](https://github.com/sky-uk/heroku-buildpack-sky-pages-hosts#champions)

## Responsibilities

### Code Reviews

* Each core maintainer should participate in 20% of PRs.
* All PRs must have at least one comment within one working day.

### Steering

* Each core maintainer should attend 50% of steering meetings.

### Contributions

* Work is done in priority order according to the
   [backlog](https://github.com/sky-uk/heroku-buildpack-sky-pages-hosts/projects/1).

## Releases

1. Ensure the fully-approved PR is up to date with `develop`.
    * If necessary, run `git rebase develop` within the branch. **Avoid** using 
      GitHub's "update branch" button as it leaves us with unhelpful merge 
      commit messages.
2. Merge fully-approved PR into `develop`.
3. Run `git checkout develop && git pull`.
4. Run `git checkout master && git pull && lerna bootstrap`.
5. Run `git merge develop`.
6. Include all new functional changes in the appropriate `CHANGELOG.md`(s).
7. Commit and push the `CHANGELOG.md` changes to `master`.
8. Go to [Hosts Buildpack/Releases](https://github.com/sky-uk/heroku-buildpack-sky-pages-hosts/releases), and
    check the tag exists.
    * If the tag exists, congrats! Now create a [**new**
      release](https://github.com/sky-uk/heroku-buildpack-sky-pages-hosts/releases/new) that utilises that
      tag.
    * If the tag doesn't exist, something went wrong.
9. Communicate changes out on Slack.
10. Update our `develop` branch with `master`.
    * Run `git checkout develop && git merge master && git push`
