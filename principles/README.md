# Principles

## Preamble

Included below are a list of principles. No, not 'universal principles' that apply in all cases, situations, and scenarios. These are 'personal principles', things that guide my approach to thinking, planning, execution, collaboration, and pretty much everything else that relates to work in general and my work in particular.

A few notes:

- These principles are fluid, meaning that they will change over time. New principles will emerge, and existing principles will be modified or discarded. This is natural, expected, and good.
- These principles are based on my personal and professional experiences. I don't expect them to work for everyone (they won't), but they've helped me and they _may_ help you too.
- These principles are comprehensive, but they are not exhaustive. I've made an effort to capture the things that I believe most deeply, and which I think are worth sharing with others.

## The List

### Intention cannot be derived from implementation

To put it another way: a given engineer, looking at a given 'unit' of code (a procedure, a function, a class, an API, etc.), may understand the _what_, but they cannot understand the _why_.

I'm making a few assumptions here, which I'll call out. First, that 'the engineer' was not involved in the original implementation of the code _and_ that they were not present for the planning and conversations that shaped it. Second, that 'the unit' is either non-trivial or that it encapsulates some business logic (eg. it is not something to the effect of `const square = (n: number) => n * n;`). Third, that 'implementation' refers to _code and only code_ (ie. it excludes any supporting comments or documentation that may contain this missing context).

Ok, so what does this mean _in general_ and _in practice_?

In general, it means that we cannot (and should not) expect engineers and technologist to understand every single thing about the code that they work on, own, or maintain.

In practice, it means a few things:
- That continuity of ownership is extremely valuable (especially when the owners are also the original implementers).
 - That we must be extra (extra, extra, extra) diligent in accurately capturing important decisions, requirements, and other relevant context surrounding the code. This includes product and technical requirements documents, but also 'ad hoc' decisions, definitions of the key concepts, and the 'philosophy' that shaped the implementation in the first place.
- That defects are much more likely to occur when the thread of ownership is severed _and_ this supporting context is missing.

### The code is incidental

This is something that I trot out quite a bit, but I've never bothered to write down. Until now.

To put it simply, we don't write code _just_ for the sake of writing code\*. We write code to _solve problems_, and by extension to _provide value_. On the one hand this probably seems obvious. On the other hand it seems to get forgotten quite often.

This has a few important implications:
- First, that we should look for — and apply — 'no code' solutions when and where we can.
- Second, that we must accept that our code will evolve and change over time (ie. to accommodate new requirements and deliver new value). To this end we need to remain egoless about the code that we write.
- Third, that there may come a time when 'writing code' (or perhaps 'writing code by hand') is no longer a practical or efficient way to solve problems. The emergence of 'assistive' technologies like Github's Copilot and AI-enabled editors like Cursor are strong signals to this effect.

To be clear: this is not an excuse to write _bad_ code or to let code 'rot' and fall into disrepair. The code that we write must still be fit to purpose, correct, well tested, easy to reason about, easy to maintain, and so on. The point is that centre the idea that the code solves a problem, and that it provides value. And if it doesn't, well then _that's_ a problem.

\* Ok, we may do this periodically, but generally not in an 'I write code for a living'-type scenario.
