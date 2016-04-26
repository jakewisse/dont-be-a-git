# Notes

Two big sections:

+ **Git internals**
+ **Tips and tricks, guidelines, etc.** - basically ways to get the most out of
  Git

## 1. Git Internals

Requirements for the second half to make sense:

- How infomation is stored. For this, basically slim down the chapter on git
  internals in pro git, commit something, show where it lives and then `git
  cat-file -p` it.
- Reiterate that when you write a commit, parts of the tree that can be reused,
  are.
- What remote refs are, and how they're no different than local ones.
- What HEAD is.
- Ways to describe a commit. (e.g. HEAD~1, HEAD^)
- What a tree-ish is.

## 2. Things you can do

+ `git log`: The single most useful git subcommand there is.

  - `git log --graph` (or gitk, if you really don't like CLIs)
  - Commit limiting with set-type operators (but for a tree)
    + `..`
    + `...`
    + You can use remotes as well, so that by fetching from a remote first, and
      then doing a `git log <local ref>..<remote>/<branchname>`, you can preview
      what was done upstream before you pull it in.

+ `git add/rm/checkout` all in a new light

  When you `add` or `rm` files, what you are really doing is writing to the git
  database. When you then run `git status`, you're being told how your working
  tree, i.e. the file system outside of the .git directory, differs from HEAD, in
  the context of the database. When files have been added to the
  index/db/whatever, they show up as green. (It's important to note that at this
  point, they are really in the database. [_look up the plumbing commands to prove
  this_]

  - Stop commenting code out and remove it! Even if you're just working on some
    change that's complicated, and you don't want to forget how it was before,
do:

  ``` sh
  $ git diff # See what your working tree/the filesystem as you can ls it looks
like and how it differs from the current HEAD

  # Oh crap, I want to keep that function that I deleted after all, but I like
the rest of the work:
  $ git checkout -p <file|directory|nothing> # You'll see the
interactive add series of prompts that will allow you to checkout from the
HEAD|discard parts of your working tree as you see fit.
  ```

+ `git stash`. Saves a commit that doesn't have a parent.

+ rebase

  First and foremost, do not be afraid.

  _Show an example of what's the worst that can happen._

  - Goes hand in hand with the need to `git push --force`

  - Number one use case: to keep feature branches up to date, without having a
    thousand merge commits cluttering up the history.

+ `rebase -i`

  This one deserves a section all on its own. Usually done outside of the
  context of an upstream. Go through each of the commands, use cases, etc.

  This, mixed with `git add -p` and squashing is **huge**.

+ `git commit --amend`

  How this is syntactic sugar for `git rebase -i HEAD^`

## Things you _should_ do

Yeah, yeah, everyone hates conventions that they think suck, but if you follow
some guidelines, or at least are aware of why they exist, everyone will be
happier when they have to go through your commits.

**What are you committing?**

More often than not, people write their code, get things to work the way they
should, and then just `git add -A && git commit -m "work"`. This makes me
cringe. When someone looks at that commit, how are they supposed to know what
parts of it are important and what parts aren't? Maybe most of the diff will
show whitespace changes, or line endings that differ in the entire file. Not
only is this a huge PITA for people reading the log/code reviewing, but merges?
You're basically giving the finger to the poor soul who was working off of a
version prior to your change, and who now needs to rebase on your changes after
you beat him/her to the upstream branch.

**Commit messages**

People (maybe the minority) do actually search the log for what's going on. `git
log --grep`, etc.

