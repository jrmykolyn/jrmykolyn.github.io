# Intention and Expectation in Code Review

## Pre-amble

This is an updated — well, rewritten — version of a presentation that I delivered sometime between 2020 and 2021. I delivered it as part of a 'technical show and tell'-type event, which was held by the Feel In Control journey  at RBC.

Sadly, I lost access to my presentation, technical notes, and other programming-related articles when I left RBC in 2021.

## Introduction

Any organization whose output involves writing code, and which has more than one person who writes code, has _some_ form of code review process. This article explores a specific _aspect_ of code review: expressing intention and expectation.

It focuses exclusively on _human_-supplied code review, rather than programmatic code review (eg. static analysis) or the results of CI/CD integrations (eg. linting, type checking, formatting, etc.).

## The _Purpose_ of Code Review

Small organizations tend to have informal code review processes, or processes based on the personal preferences and experiences of the employees. Enterprise-scale organizations, as well as organizations whose code powers critical systems (eg. healthy and safety, manufacturing, energy, transportation, etc.) tend to have highly formalized code review processes.

That said, the _purpose_ of code review in both small and large organizations is roughly the same: to ensure that the code under review is correct, comprehensible, maintainable, and defect free. Organizations — and the individuals within them — have different opinions about how to achieve this, and even whether all of these things are actually possible.

Much has been written about the role of code review in ensuring the correctness and defect-free-ness. There are studies and white papers on the relationship between the number of lines in a pull request and  the likelihood that an escaped defect will follow. These are good and valuable studies, but they're not relevant for this article. If your organization practices code review, and if you yourself review code, then you believe that human-supplied code review provides _some_ value.

This brings us to the focus — and central question — of the article: when reviewing code, how can I unambiguously express my intentions and my expectations?

## Intention and Expectation

First, let's break down our terms.

In this case 'intention' refers to what we're trying to get across. Sometimes our intention is to understand what the code under review is actually trying to do (and why). Sometimes our intention is to suggestion an alternative approach or implementation. Sometimes our intention is to acknowledge and celebrate a particularly clever solution. These examples differ significantly in terms of their intention.

'Expectation' refers to what we want the author to _do_ with our review. Sometimes our expectation is for the author to clarify part of the solution, or the requirement that it satisfies. Sometimes our expectation is for the author to review our suggestion, and to make a decision about whether or not to implement it. Sometimes our expectation is for the author to change a portion of the solution (or the approach as a whole). _These_ examples differ significantly in terms of their expectations.

## The Problem (That We're Focusing On)

So what happens when there's misalignment between the intention and expectations of a review and how the review is received by the author?

Misunderstanding _intention_ results in confusion and wasted time. The author can't effectively prioritize the feedback that they've received, which _may_ lead them to focus on the wrong things. This leads to another round of feedback, which leads to more confusion, which leads to more feedback, and so on.

Misunderstanding _expectation_ leads to frustration for both author and reviewer. The reviewer _expects_ an answer, but they don't receive it. Frustrating. The author mistakes _optional_ suggestions for blocking changes. Frustrating. The author mistakes _blocking_ changes for optional suggestions. Frustrating.

## The Solution (Part Of It At Least)
It's good to understand why misalignment around intention and expectation are _bad_, but what can we do to prevent these misunderstandings in the first place? Well, we can use a small set of keywords with agreed-upon meaning and calls-to-action.

### Keywords

#### NOTE:
- Intention: reviewer has additional context or information to share.
- Expectation: author absorbs additional information, decides whether action is required.
- Example:

```
[NOTE]:
It looks like this is building on some of the code that I wrote for the previous project.
We had to accommodate quite a few edge cases, so be careful not to remove that functionality in this update.
```

#### QUESTION:
- Intention: reviewer is communicating certainty/confusion/missing context.
- Expectation: author provides clarification; code change not necessarily required.
- Example:

```
[QUESTION]:
I see that you're checking for `null` here, but not for other falsy values. Is that intentional?
```

#### SUGGESTION:
- Intention: reviewer shares alternative approach, improvement, or other optional change.
- Expectation: author considers the suggestion, decides whether not to implement it. Non-blocking.
- Example:

```
[SUGGESTION]:
This snippet looks like it would be useful elsewhere. How about extracting it out into a generic utility?
```

#### REQUIRED:
- Intention: reviewer shares a change that must be made prior to approval. Blocking.
- Expectation: author makes the required change, then re-request review.
- Example:

```
[REQUIRED]:
This code produces a race condition. Update it to _ensure_ that the request has resolved before attempting to display the UI.
```

#### KUDOS:
- Intention: reviewer draws attention to part of the solution that is clever, helpful, or otherwise deserving of praise.
- Expectation: author feels nice.
- Example:

```
[KUDOS]:
I see that you removed a ton of duplicate test code by making the mocks configurable. Excellent job!
```

#### PICKY:
- Intention: reviewer is expressing a personal preference or proposing a trivial/non-critical change.
- Expectation: author decides whether any action is necessary/appropriate; may deprioritize picky comments.
- Example:

```
[PICKY]:
This method name is inconsistent with the rest of the class. I know we don't enforce this convention, but I'd like us to be consistent with what's already in place.
```

The keywords above — NOTE, QUESTION, SUGGESTION, REQUIRED, KUDOS, and PICKY — _should_ cover any type of feedback that a reviewer may provide as part of a pull request. Using them gives the author additional information about the review's intention (eg. what they're trying to get across) and their expectations (eg. what they want the author to _do_ with the feedback).

Also note that only one keyword signals _blocking_ feedback: REQUIRED. All of the other keywords are non-blocking, no matter how many times they appear in a review.

## Conclusion

And now for the ask: share this with your team _and_ try it out.

Yes, there's a bit of upfront work to make sure that everyone is familiar with the keywords and what they signal, but that's a minor cost (and it only needs to be paid once per team member).

As a reviewer, these keywords are powerful tools for signalling your intention and expectation. They give pull request authors direct insight into your perspective, and they allow both sides to spend less time working through review-time misalignment and misunderstandings.

The result: code review that is more efficient, more clear, and less frustrating.

Give it a shot.

## Reference

| Keyword | Intention | Expectation | Blocking? |
| - | - | - | - |
| NOTE | Reviewer has additional context or information to share. | Author absorbs additional information, decides whether action is required. | No |
| QUESTION | Reviewer is communicating certainty/confusion/missing context. | Author provides clarification; code change not necessarily required. | No |
| SUGGESTION | Reviewer shares alternative approach, improvement, or other optional change. | Author considers the suggestion, decides whether not to implement it. | No |
| REQUIRED | Reviewer shares a change that must be made prior to approval. | Author makes the required change, then re-request review. | Yes |
| KUDOS | Reviewer draws attention to part of the solution that is clever, helpful, or otherwise deserving of praise. | Author feels nice. | No |
| PICKY | Reviewer is expressing a personal preference or proposing a trivial/non-critical change. | Author decides whether any action is necessary/appropriate; may deprioritize picky comments. | No |

## CHANGELOG

### 2024/10/31 (👻)

- Changed 'TODO' (the original _blocking_ keyword)  to 'REQUIRED'.
- This change sidesteps any confusion that might arise from the fact that 'TODO' is widely used _in-code_ as a way to defer work (ie. kick it down the road).
- Thanks to [Kevin Lin](https://github.com/kevinlinpt) for feedback.
