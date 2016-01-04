### What is Git anyway?

@@@

> Git is a <span style="color: lightgreen;">content-addressable</span> file system, with a VCS built on top.

<p style="text-align: center;">
	<ul>
		<li class="fragment">Porcelain vs. Plumbing</li>
		<li class="fragment">Immutable data structure. Easy to compare files for equality</li>
	</ul>
</p>

Notes:

What does this mean?

- Git isn't just a VCS. It's a content tracker.
- While most of the commands we use are very VC-oriented, they are simply
  porcelain commands that are implemented by plumbing ones that interact with
  the Git file system, or database.
- Contrast to location-addressable file system, which has a path/location as an
  address.
- What happens when you change the data? No longer the same address. **Immutability**.
- (Git's db is an immutable data structure)

@@@

### Question:

How many of you think (or thought at one point) that Git stores a series of
deltas?

<div class="fragment wrong-answer">NOPE</div>

@@@

### How Git stores data

- Instead of a series of deltas, Git's db consists of <i style="color: lightgreen;" >compressed snapshots of files</i>.

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
	<li class="fragment">But not only files...</li>
</ul>

@@@

### How Git stores data

<p style="font-size: .8em;">In Git's database, there are a couple of different kinds of objects that are stored:</p>

<ul>
	<li><b style="color: lightgreen;">Blobs</b>  _(versions of files)_</i></li>
	<li><b style="color: lightblue;">Trees</b>  _(versions of directories)_</li>
	<li><b style="color: pink;">Commits</b>  _(pointers to root trees)_</li>
</ul>

@@@

## The outside world ##

<p class="fragment">
	You often hear that Git is a <i style="color: lightgreen">distributed</i> version control system.
</p>

@@@

<div class="git-logo">
	<img src="img/git-logo-edit.png" alt="Git logo" class="img-simple">
	<span>--distributed-is-the-new-centralized</span>
</div>

Notes:

Now that we have a little insight into how git stores a repo's history, how
are we supposed to connect our separate Git databases/histories so that we can
collaborate?

@@@

<code>$ git push <b style="color: darkturquoise;">origin</b> feature</code>

<ul style="margin-top: 16px;">
	<li class="fragment">`origin` is what's called a <b style="color: lightgreen;">remote</b></li>
	<li class="fragment">It's just another Git repository</li>
	<li class="fragment">But it doesn't need to have a working tree, so<br />
	it's called a <i>bare</i> repository</li>
</ul>

Notes:

- First think about pushing a branch that doesn't yet exist on the remote
- The only reason that in users' repo's there is a `.git` directory, is that
  you need to have some space to actually **use** the files that the git
  database represents.
- Now think about conflict resolution. What if I try to push to a remote's
  branch that is already there?
- When you push branches that already exist, the remote by default only
  accepts fast-forwards.

- The remote's object database contains the result of merging all reachable
  objects from everyone branches that have been pushed, or copied there.

@@@

## _DEMO_

Notes:

- Create a new remote directory, and `git init --bare`.
- Poke around, and show that some of the commands that you would usually use
  don't work.
- Go back to the original repo, and `git remote add path/to/remotedir origin`.
- Push to the remote with `git push origin master`.
- `cd` over to the remote, and `tree refs/` and take a look at the contents of
  `refs/heads/origin`
- Time permitting, `git cat-file` down into the database and show that the
  same files are persisted, the exact same way.

@@@

### Remote-tracking branches ###

<code style="color: lightskyblue;">$ git pull origin master</code>

<ul style="margin-top: 16px;">
	<li class="fragment">Actually a pretty loaded command</li>
	<li class="fragment">What does it do?</li>
	<ul>
		<li class="fragment">Updates <code>/refs/remotes/origin/master</code></li>
		<li class="fragment">Attempts to reconcile your local branch with what changed on the remote</li>
	</ul>
</ul>


Notes:

- Yet another term you've probably all heard somewhere.
- `git pull` is sort of a loaded command, but oddly enough it's one of the
  first ones that people tell you to use. (Maybe because it does something
  similar to other centralized VCS's)
- No concept of merging/reconciling differences between remote and remote
  tracking branches; remote is always copied.
- `fetch` combined with a `merge`. (If you're OCD about knowing what happened,
  you can do them separately and see what changed before merging)

@@@

## _MORE DEMO_

Notes:






















