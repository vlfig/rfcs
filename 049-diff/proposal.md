# Summary

This proposal outlines a new message for resource types requesting a description of the differences
 between two valid revisions: `diff`.

# Motivation

The traceability and visibility guarantees that Concourse offers are invaluable.
We can know with relative ease the exact revisions of which resources were used in, or output from, which builds.
With _causality_ we will be able to also have a transitive view of those same relations.

More often than not, what the user really wants when looking at such information is to know what changed. The difference.
It's not for nothing that the more traditional would call the field in which Concourse operates "change management".
Many concerns, from the technical to the legal, revolve around the difference that's being shipped rather than the contents of the end product.
In computation, the importance and the size of a change correlate very little. It is crucial to spot small and large changes equally well and to understand which are relevant and which are not.
Differences are by nature associative, they coalesce.

Important though it may be, the difference is often hard to tell.

To the left (upstream) where ingredients are rawer, structures are simpler but revisions abound. Many are faulty, some are partial, others are reversions, few make it downstream. The ability to quickly understand the difference between any two helps us understand which are which, understand why something failed, when something's complete, or the same.

Further to the right (downstream) waters are calmer but murkier. All but the simplest of delivery DAGs result in end products so processed that a naive `diff` on them would only return unintelligible gibberish. Conversely, a more meaningful `diff` requires more knowledge of the particular structures and formats of that end product. While we cannot magically reverse the jobs that created an artifact, we do know the transitive closure of the upstream resource revisions used in making it.

So, if comparing two end products is futile, comparing their ingredients is promising
 
That knowledge lives in resources.

A `git` resource knows how to interpret and display the differences between two revisions of a git repository. A `registry-image` resource would know how to diff docker images. A resource that operates with json files would know that changes in the order of map entries are irrelevant. Different resources would have a particular interpretation of what it means to be different, because they have the knowledge to normalize before diffing, to hide irrelevant changes or to capture relevant ones from elsewhere if need be.
 

> Describe the problem that this change intends to solve. Don't get into how it
> solves it yet.
>
> This can be brief, but if there is any additional context or any
> empathy-building that you'd like to communicate, it can't hurt to include it
> with plenty of detail and hypothetical examples.


# Proposal

> Describe your proposal.
>
> Things that can help: clearly defining terms, providing example content,
> pseudocode, etc.
>
> Feel free to mention key implementation concerns.


# Open Questions

> Raise any concerns here for things you aren't sure about yet.


# Answered Questions

> If there were any major concerns that have already (or eventually, through
> the RFC process) reached consensus, it can still help to include them along
> with their resolution, if it's otherwise unclear.
>
> This can be especially useful for RFCs that have taken a long time and there
> were some subtle yet important details to get right.
>
> This may very well be empty if the proposal is simple enough.


# New Implications

> What is the impact of this change, outside of the change itself? How might it
> change peoples' workflows today, good or bad?
