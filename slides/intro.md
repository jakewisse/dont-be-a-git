# Don't be a git.
_A talk about Git and why it's awesome_

@@@

# Why a talk about Git?

Notes:

### Preface

- Feel free to ignore [or better yet, correct] me if you already know what I'm
  talking about
- We all use Git every single day, it's a huge part of how we get things done,
  and some people still just use three/four commands that they assume work a
  certain way based on their behavior.

@@@

We all use it **every** single day,
<p class="fragment">And I feel like it's _hugely_ underutilized.</p>

@@@

## An analogy

<img alt="Vim" src="img/vim.png" class="fragment img-simple" />

Notes:

- When first starting in Vim, it's paralyzing. "I just wanna use the arrow
  keys and stay in insert mode!"
- The more you learn about the API and vimscript, the more things you can do
  with it (and hopefully be more productive as a result).
- So too with Git. When you're stuck using basic commands and not peeking behind
  the curtains, it's like staying in Insert mode and using the arrow keys.

@@@

> You can totally "stay in insert mode" all day long and get by, but you'd be
> completely ignoring everything that makes the tool powerful.

Notes:

Bottom line: if you're extremely comfortable using Git to its full potential,
we can be more flexible and resilient programmers in the face of change and
complicated workflows/release cycles, etc.

@@@

### Another reason for this talk: <i>Git's CLI</i> ###

<p class="fragment">Given the wrong mental model of what's going on, it can be misleading, and
therefore pretty frustrating.</p>

Notes:

- `git checkout` doesn't have a ton in common with `svn checkout`
- "I think if we look at Git's internals a little bit, we can all be sure that
  no one is making any incorrect assumptions about what Git is doing when we
  use it. (As I did)"


@@@

## Goals ##

- Peek behind the curtains, and take a look at how Git persists information.
- Armed with a correct model of Git, demo a couple of great things that Git does (from the CLI).
