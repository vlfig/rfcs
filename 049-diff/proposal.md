# Summary

This proposal outlines a new message for resource types requesting a description of the differences
 between two valid revisions: `diff`.

# Motivation

The traceability and visibility guarantees that Concourse offers are invaluable.
We can know with relative ease the exact revisions of resources that were used or produced in any given build.
With _causality_ we will be able to also have a _transitive_ view of those same relations.

More often than not — especially when pondering whether to deploy to production — what the user really wants to know is what changed. The difference.
Important though it may be, the difference is often hard to tell.

To the left (upstream) where ingredients are rawer, structures are simpler but revisions abound. Many are faulty, some are partial, others are reversions, only a few make it downstream.
The ability to quickly understand the difference between any two helps us understand which are which, understand why something failed, when something's complete, incomplete, or the same.

Further to the right (downstream) waters are calmer but murkier.
All but the simplest of delivery DAGs result in end products so processed that a naive `diff` on them would only return unintelligible gibberish.
Conversely, a more meaningful `diff` requires more knowledge of the particular structures and formats of that end product. 
While we cannot magically reverse the jobs that created an artifact, we do know the transitive closure of the upstream resource revisions used in making it.
So, if instead of trying to compare instances of the end product we were to compare their ingredients, transitively, we'd get a much more meaningful view of their differences.

Causality therefore allows us to compose the knowledge of the particular structures of our end products.
That knowledge lives in resources.
A `git` resource knows how to interpret and display the differences between two revisions of a git repository.
A `registry-image` resource would know how to diff docker images.
A resource that operates with json files would know that the order of map entries is irrelevant.
Different resources would have a particular interpretation of what it means to be different, because they have the knowledge to normalize before diffing, to hide irrelevant changes or to capture relevant ones from elsewhere if need be.
Together, diff-capable resources and causality, make it easy to tell what is different at the end of our pipelines.

# Proposal

> Describe your proposal.
>
> Things that can help: clearly defining terms, providing example content,
> pseudocode, etc.
>
> Feel free to mention key implementation concerns.

An extension to the `resource` interface, adding the `diff` message.
Prototypes are free to not implement it. If they implement it they have to provide conformant responses.
Always a function of two revisions.

diff(one: Revision, another: Revision): Either[Error, DiffMessage]

DiffMessage {


Concourse 
Implement 


# Open Questions

> Raise any concerns here for things you aren't sure about yet.

Resource containers are kept around and allowed to cache stuff.
Can we say that a resource will never be asked for diffs of revisions that it hasn't yet given?
Is it even relevant?

{::nomarkdown}
<svg width="400" height=300>
    <circle cx="150" cy="100" r="10" fill="blue"/>
</svg>
{:/}

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
