# Things I can actually use

Notes:

- This part of the talk is like Git tips, but instead of being magic incantations, these should make sense in light of what we now know about how Git stores data.

@@@

## Visualizing histories

_Many times in Git, it's important to be able to visualize a history, and to be able to ask questions about how histories/branches relate to each other._

@@@

## `git log`

Prints a list of commits that are reachable from the specified branch.

<ul>
	<li class="fragment">More options than you can shake a stick at, so aliases are your friend</li>
	<li class="fragment">Real power comes from all the ways that you can filter its output.</li>
</ul>

@@@

### Revision ranges

You can use `git log` to compare the revision trees of two different branches using set-like operators.

@@@

<code>$ git log &lt;commit-a&gt;<span style="color: #E810DA;">..</span>&lt;commit-b&gt;</code>

<i style="color: darkgray;">Show me all the commits that are reachable from &lt;commit-b&gt; but not reachable
from &lt;commit-a&gt;</i>

@@@

`$ git log develop..feature`

@@@

<p style="text-align: left;">
`$ git fetch origin develop`<br />
`$ git log develop..origin/develop`
</p>

Notes:

- Useful for checking to see what commits were introduced to the remote before you merge them in to your local branch.

@@@

<code>$ git log &lt;commit-a&gt;<span style="color: #E810DA;">...</span>&lt;commit-b&gt;</code>

<i style="color: darkgray;">Show me all the commits that are only reachable from &lt;commit-a&gt; or &lt;commit-b&gt;, but not both.</i>

@@@

`$ git log --left-right develop...feature`

Notes:

I use this form _much_ less than the double-dot operator, but still, here it is.

@@@

### Useful options for `git log`

- `-p`
  + Show a diff between each commit and its parent
- `-w`
  + Ignore whitespace changes when showing the diff
- `--name-only`
  + Show a list of files that were modified by the commit
- `-G<regex>`
  + Show only commits whose diff contains a match to the given regex

Notes:

**I know this is a lot**. But we use this thing every single, freaking day, so if you practice in your daily workflow, next thing you know this stuff is a second language to you.

@@@

### What am I committing?

<p>Many times people will not pay attention to what they are committing, or what commits their branches contain.</p>

<p class="fragment">I propose that we should all be <b style="color: lightgreen;">proud of our histories!</b></p>

@@@

### What am I committing?

Rather than show you guys a ton of slides with sequences of commands on them, I figure this is best explained with another <b style="color: pink;">DEMO</b>.

Notes:

Using the gittest repo:

_All of these changes are going to be rebased into a single commit_

- Make a bunch of modifications to a file.
- Use `git checkout -p` to recover some changes that you didn't mean to discard
- Commit something
- Make some more modification to a couple of files, and then use

@@@

### What am I committing?

- `-p` flag with `git add` and `git checkout`
- Check what you're about to commit with `git diff --cached`
- Check what you're about to throw away with `git diff`
- Squash commits together with `git rebase -i <commit>`

@@@

### Rebasing

Time permitting... yet another <i style="color: lightgreen;">DEMO.</i>

@@@

**The end**














