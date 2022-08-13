# Joomla Feature / Specification RFC Workflow

## Pre-Draft

The goal of the Pre-Draft stage is to determine whether a majority of Joomla is
interested in adding a Joomla **Feature**, publishing a Joomla **Specification**
for a proposed concept or implementing a **Process**.

Interested parties may discuss a possible proposal, including possible
implementations, by whatever means they feel is appropriate. That includes informal
discussion on official Joomla discussion mediums of whether or not the idea has
merit and is within the scope of Joomla's goals.

Once those parties have determined to move forward, they must form a Working Group.
A Working Group consists of, at minimum:

* One Editor
* One member of Open Source Matters (Class 1, 2 or 3) who will act as Sponsor
* At least one other individual. This may be a member of Open Source Matters
  as well as a member of the general community.

The proposal is not required to be fully developed at this point, although that is
permitted. At minimum, it must include a statement of the problem to be solved
("what" in section *1. Summary* and "why" in section *2. Why Bother*, see
[Meta Document template](templates/spec-template-meta.md)) and
basic information on the general approach to be taken. Further revision and
expansion is expected during the Draft Phase.

Once the Working Group deems the first two sections (*1. Summary and 2. Why bother?*)
complete, the Sponsor may request an Entrance Vote among the Production Department Team
Leaders and the Production Department Coordinator to determine if there is a general
interest in publishing a Joomla Feature or Specification or implementing a Process for
the proposed topic. If the vote fails, the Sponsor may request an Entrance Vote of all
Open Source Matters Members (Class 1, 2 and 3).

For **Feature** or **Specification** proposals, the Production Department Team Leaders
and Production Department Coordinator may initiate a Rejection Vote if the proposal does
not meet the vision and mission of the Joomla project, or if its implementation would
create an unmanageable maintenance burden. A rejection must be justified in detail.

If the vote passes, the proposal officially enters Draft stage. The proposal
receives an RFC number incremented from the highest numbered RFC
which has passed the Entrance Vote, regardless of the status of that RFC.

The Working Group may continue to work on the proposal during the complete voting
period.

## Draft

The proposal (the "what") is accepted by the community and thus expresses the
community's demand. Therefor, section *1. Summary* and section *2. Why Bother* MAY NOT
be altered after a successful Entrance vote.
Joomla's Leadership MUST take all due measures to move the proposal to the Accepted state.

The goal of the Draft stage is to discuss and polish a **Feature / Specification / Process** 
proposal up to the point that it can be considered for review by the Production 
Department Team Leaders.

In Draft stage, members of the Working Group and other contributors 
MAY make any changes they see fit via
pull requests, comments on GitHub, Mailing List threads, IRC and similar tools.
Change here is not limited by any strict rules, and fundamental rewrites are
possible if supported by the Editor, except section *1. Summary* and section *2. Why Bother*. 
Alternative approaches may be proposed and
discussed at any time. If the Editor and Sponsor are convinced that an alternative
proposal is superior to the original proposal, then the alternative may replace the
original. Working Group members are expected to remain engaged throughout the Draft
Phase. Discussions are public and anyone, regardless of Joomla affiliation, is
welcome to offer constructive input. During this phase, the Editor has final
authority on changes made to the proposed specification.

The Production Department Coordinator will ensure that the Working Group is provided
with necessary resources to work on the specification, such as a dedicated GitHub
repository, mailing list, forum section, and similar such tools.

All knowledge gained during Draft stage, such as possible alternative approaches,
their implications, pros and cons etc. as well as the reasons for choosing the
proposed approach must be summarized in the meta document. The purpose of this rule
is to prevent circular discussions or alternative proposals from reappearing once
they have been decided upon.

When the Editor and Sponsor agree that the proposal is ready and that the meta
document is objective and complete, the Editor may call for a Readiness Vote of the
Working Group to determine if the specification is substantively complete and ready
for trial implementations.

If the vote passes, the proposal officially enters Review Phase. If it does not, it
remains in Draft Phase.

## Review

The Review Phase is an opportunity for the community to experiment with a reasonably
fixed target to evaluate a proposal's practicality. At this stage, the Sponsor is
the final authority on changes to the specification as well as any decisions to move
the proposal forward or backward, however, the Editor may veto proposed changes they
believe are harmful to the design of the specification.

During this phase, trial implementations of the specification are expected and
encouraged. Changes to the specification are limited to those directly informed by
trial implementations, wording, typos, clarification, etc. Major changes are not
permitted in this phase. If the development of trial implementations demonstrates
the need for major changes then the specification must be pushed back to Draft
Phase. Any incompatible change that would require significant effort for trial
implementations to adjust for qualifies as a major change. Small to moderate
incompatible changes do not necessarily mandate a return to Draft Phase.

Unless a proposal is moved to Draft stage again, it must remain in Review stage for
a minimum of four weeks and until

- the User Interface is defined and the manual (help) page is written for the
  functionality proposed in **Feature RFCs**.
- two independent viable trial implementations can be demonstrated for
  **Specification RFCs**, ideally as examples in the proposal repository. The 
  responsibility for finding such trial implementations and presenting them to the 
  Production Department Team Leaders lies with the Working Group, and especially 
  the Editor and Sponsor. As not all specifications are PHP interfaces where the 
  definition of "implementation" is self-evident, the Sponsor should use good 
  faith judgement to  determine when that is the case. Any member of the Production 
  Department Team Leaders may object to a given trial implementation as irrelevant 
  or insufficient with due cause.

Once four weeks have passed and UI and help page or two viable trial implementations
can be demonstrated, the Sponsor may call an Acceptance Vote. If the Acceptance
Vote fails, the specification may remain in Review.

## Accepted

If the Acceptance Vote passes, then the proposal officially becomes an **Accepted
Feature / Specification / Process**. At this time, the Working Group is automatically 
dissolved,  however the Editor's input (or a nominated individual communicated to 
the Production Department Coordinator) may be called upon in the future should 
typos, changes or Errata on the specification be raised.

In case of Feature RFCs, a Development Team is created within the Production
Department. 

## Deprecated

A **Deprecated Specification / Feature / Process** is one that has been approved,
but is no longer 
considered relevant or recommended. Typically this is due to the Specification / Feature / Process 
being superseded by a new version, but that is not required.

A Specification / Feature / Process may be Deprecated explicitly as part of the Acceptance Vote for 
another Specification / Feature / Process. Alternatively, it may be marked Deprecated by a Deprecation 
Vote.

## Implemented

An **Implemented Feature** is one that has been developed, tested and merged for 
the next available major or minor release. 

## Abandoned

An **Abandoned Feature / Specification / Process** is one that is not actively being worked 
upon. A Feature / Specification / Process can be forwarded to an Abandonment vote by the Production 
Department Coordinator when it is without an Editor for 60 days or a Sponsor for
60 days, or after a period of 6 months without significant activity in a Working 
Group. An Abandonment vote is up to the members of Open Source Matters (Class 1, 2 or 3).

At this time the Working Group is automatically dissolved.

Once a Feature / Specification / Process is in "Abandoned" stage it may only once again be 
moved to Draft after a fresh Entrance vote by the members of Open Source Matters (Class 1, 2 or 3) 
following the same procedure as if it was a pre-draft, except it may retain its 
previously assigned number. If the aims of the Feature / Specification / Process differ from 
the original entrance vote, it is up to the discretion of the Production Department 
Team Leaders whether or not it should be considered a fresh Feature / Specification / Process 
or a restart of activity on the Abandoned Feature / Specification / Process.

## Project Referendum

At any time the Editor of a Feature / Specification / Process in Draft or Review Phase may 
call for a non-binding Referendum of Production Department Team Leaders on the 
current state of a Feature / Specification / Process.  Such a Referendum may be called 
multiple times if appropriate as the Feature / Specification / Process evolves, or never, at 
the Editor's discretion. The Production Department Team Leaders may also require 
such a Referendum as a condition of an Acceptance Vote if appropriate.  Referendum 
results are non-binding but the Working Group and Production Department Team 
Leaders are expected to give the results due consideration.
