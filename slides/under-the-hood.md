### What is Git anyway?

@@@

> Git is a <span style="color: lightgreen;">content-addressable</span> file system, with a VCS built on top.

<p style="text-align: center;">
	<ul>
    <li class="fragment">Immutable data structure <small>(More on this later)</small></li>
    <li class="fragment">Porcelain vs. Plumbing</li>
	</ul>
</p>

Notes:

What does this mean?

- Git isn't just a VCS. It's a content tracker.
- What is a "content-addressable file system?"
- Contrast to location-addressable file system, which has a path/location as an
  address.
- What happens when you change the data? No longer the same address. **Immutability**.
- (Git's db is an immutable data structure)

Most of the VC-oriented commands we use are known as **porcelain commands**.
These are implemented by **plumbing commands** interact with the Git file
system, or database.

@@@

### Question:

How many of you think (or thought at one point) that Git stores a series of
deltas?

<div class="fragment wrong-answer">NOPE</div>

@@@

### How Git stores data

- Instead of a series of deltas, Git's db consists of <i style="color: lightgreen;" >compressed snapshots of files</i>.

Notes:

- If you were to add a new file to a repository and commit it, then modify the
  file and commit it again, inside Git's database there would be two distinct,
  compressed files stored.

@@@

### But isn't that wasteful?

<p class="fragment"><i>Not necessarily</i></p>

Notes:

- Usually you aren't modifying every single file in a repo in every commit, and
  git reuses any file-states that aren't modified.
- Using a system of what's called packfiles, Git bundles up objects in its db
  into a delta-compressed "packfile". (So I sort of lied about the deltas
  thing :P)

@@@

## _DEMO_

Notes:

### Demo

_Encourage everyone to go read the Pro Git book by Scott Chacon, specifically
the chapter on Git Internals._

- Init. a brand new git repo
- Create a file
- `tree .git/objects`, and show that there's nothing in there except the
  `info/` and `pack/` directories.
- `git add file1`
- `tree .git/objects/` again, and show that there's now a new directory, with
  a new file in it.
- Look at the `.git/index` file
- Commit, and then use `git log` to look at the commit.
- use `git cat-file -p <SHA>` to look at the commit object as persisted in the
  database, and then trace it down to the saved blob.
- Do the same thing again, but with a new directory and a couple more files.

@@@

### How Git stores data

<ul>
	<li>Instead of a series of deltas, Git's db consists of <i style="color: lightgreen;" >compressed snapshots of files</i>.</li>
	<li class="fragment">But, as you've seen, not only files</li>
</ul>


@@@

### How Git stores data

<p style="font-size: .8em;">In Git's database, there are a couple of different kinds of objects that are stored:</p>

<ul>
	<li><b style="color: lightblue;">Blobs</b>  _(versions of files)_</i></li>
	<li><b style="color: lightgreen;">Trees</b>  _(versions of directories)_</li>
	<li><b style="color: pink;">Commits</b>  _(pointers to root trees)_</li>
</ul>

Notes:

### Blobs

- Whenever a new file/modification to a file is `git add`ed, a new blob object
  is created, at a new address.

### Trees

- Whenever a new file/modification to a file is `git add`ed, All of the tree
  objects above it are invalidated, and new ones must be created.
- This means that no matter what change occurs in Git, a new root tree will
  always be created. **(Root tree objects as snapshots of the state of the
  repo)**

### Commits

- They not only represent the state of the repository at a place in time (by
  pointing at a root tree object) but because they contain a list of parent
  commits, they form a directed, acyclic graph that represents a history.

@@@

> Commit objects are what make Git a VCS.

@@@

<img src="img/git-tree-1.png" class="img-simple" />

@@@

<img src="img/git-tree-2.png" class="img-simple" />

@@@

<img src="img/git-tree-3.png" class="img-simple" />

<p style="color: red;">These objects are all invalidated, and new ones must be
created.</p>

@@@

## Branches

- Pointer to a commit, and therefore like naming a history
- Implemented as a file, containing only the address of a commit object
- `refs/heads/<branch-name>`
- `HEAD`: a pointer to the "current" branch

Notes:

- Branches are ephemeral in Git. They're cheap, easy to create and delete.
  Once you merge a branch into another branch, you can safely delete the
  first. If for some reason you want to go back and continue work, you can
  always create a new branch that points to just prior to the merge.















