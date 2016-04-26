# (Git Pun Here)
_All about the amazing content tracker._

@@@

## Why a talk about Git?

Notes:

_Before starting_:

I know that there's probably a wide range of Git aptitudes here, but I thought
it would be useful to get some core Git knowledge out in the open.

@@@

We all use it **every** single day,
<p class="fragment"><i>And I feel like it could be leveraged much more than it is.</i></p>

Notes:

- Mentality that the VC software you use is secondary to the code you track with
  it. (This is, of course, true)
- Doesn't mean that we can't all up our Git game, and reap some pretty awesome
  benefits.
- Towards the end of this talk I'll get into some specifics of exactly what
  this means, specifically.

@@@

## An analogy

<img alt="Vim" src="img/vim.png" class="fragment img-simple" />

Notes:

- When first starting in Vim, it's paralyzing. "I just wanna use the arrow
  keys and stay in insert mode!"
- The more you learn, the more things you can do with it (and hopefully be more
  productive as a result).
- So too with Git. When you're stuck using basic commands and not peeking behind
  the curtains, it's like staying in Insert mode and using the arrow keys.
- Like with source control, at first you have this idea that the tool is
  secondary to what you're making with it. **But**, if you invest in gaining
  deep knowledge of the tool, there are many benefits to be had.

@@@

> You can totally "stay in insert mode" all day long and get by, but you'd be
> completely ignoring everything that makes the tool powerful.

Notes:

Bottom line: **if you're extremely comfortable using Git to its full potential,
we can be more flexible and resilient programmers in the face of change (e.g.
changes in release schedules, etc.).**

@@@

### Another reason for this talk: <i>Git's CLI</i> ###

<p class="fragment">Given the wrong mental model of what's going on, it can be misleading, and
therefore pretty frustrating.</p>

Notes:

- `git checkout` doesn't have a ton in common with `svn checkout`
- If we look at Git's internals a little bit, we can all be sure that no one is
  making any incorrect assumptions about what Git is doing when we use it. (As I
  did)

@@@

## Goals ##

- Peek behind the curtains, and take a look at how Git persists information.
- Armed with a correct model of Git, demo a couple of great things that Git does (via its CLI).

