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
	<li class="fragment">When it doesn't need to have a working tree,<br />
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

- `git clone gittest-remote` to create another instance of the gittest repo.
- Commit to the master branch and push back to the remote.
- Move back to the first instance and run `git fetch` first, show the difference
  between the local branch and the remote-tracking one, and then use `git merge
  origin/master` to manually merge it in. 
- Talk about `git reset --hard origin/master` and how it differs from `git merge
  origin/master`.
- Now, do some work on the master branch on both consuming repos, and try to
  push from both, showing that by default, the remote only accepts new refs that
  have the current HEAD as an ancestor (a "fast-forward").

