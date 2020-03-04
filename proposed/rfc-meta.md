# Proposal Process Meta Document
*Pre-Draft*

## 1. Summary

For a sustainable success of the Joomla project, Features and Specifications need to be well-thought and generally accepted.
At the time of this writing (Jan 2020), the organisation does not have a defined process to ensure this.

This proposal aims to define a way to enable everybody in the community to suggest features or specifications, and to define, how the community / project decides on the proposal.

## 2. Why Bother?

During the *Forum for the Future* event in January 2020, there was an overwhelming consensus about the need to act more professional.

The project is encountering long-standing showstoppers for the release of Joomla 4.0, which could have been avoided by a *think-first-then-implement* approach. An RfC (*Request for Comments*) process is an appropriate tool to address this kind of problems, and will additionally increase the (not only the perceived) professionalism of the project. 

## 3. Scope

### 3.1 Goals

The goals for this proposal are to

* define how to propose specifications, features or procedures
* define the possible states of a proposal
* define the workflow through those states
* define the decision process

### 3.2 Non-Goals

It is not the goal of this proposal to limit the ability of anybody to propose 
specifications, features or processes.

## 4. Approaches

The wording and structure for this proposal are heavily inspired
by the [PHP FIG][]. In fact, the README, workflow bylaw, voting protocol, and the 
RfC document structure were created from copies of the FIG original.

### 4.1 How to Propose Specifications, Features or Procedures

As a single point of truth, all proposals are managed in this repository 
(currently *joomla-x/joomla-standards*, which should be moved to a pinned repository 
*joomla/joomla-standards* or *joomla/rfc*).

In the `template/` directory of the repository, templates for the proposals are 
provided, so they will follow a certain structure. Having this structure allows 
to build user interfaces for users who are not familiar with GitHub, f.x. on the 
[Ideas portal][ideas].

To get started, the two first paragraphs are most important:
* **1. Summary** to describe what the proposal is about, and
* **2. Why Bother** to describe why anybody should spend time on it.

The second paragraph is the point where also Marketing gets involved into the proposal, 
so they can tell, whether or not that proposal makes sense to our audience, and what is 
important from a non-technical point of view. In most cases, Marketing will rephrase 
that paragraph. 

### 4.2 Possible States of a Proposal

* #### Pre-Draft

    The goal of the Pre-Draft stage is to determine whether a majority of Joomla is
    interested in adding a Joomla **Feature** or publishing a Joomla **Specification**
    for a proposed concept.

* #### Draft

    The goal of the Draft stage is to discuss and polish a **Feature / Specification** 
    proposal up to the point that it can be considered for review.
    
* #### Review
  
    The Review Phase is an opportunity for the community to experiment with a reasonably
    fixed target to evaluate a proposal's practicality.
    
* #### Accepted
      
    If the Acceptance Vote passes, then the proposal officially becomes an **Accepted
    Feature / Specification**.

* #### Deprecated

    A **Deprecated Specification** is one that has been approved, but is no longer 
    considered relevant or recommended. Typically this is due to the Specification 
    being superseded by a new version, but that is not required.

* #### Implemented

    An **Implemented Feature** is one that has been developed, tested and merged for 
    the next available major or minor release. 

* #### Abandoned

    An **Abandoned Feature / Specification** is one that is not actively being worked 
    upon. 

### 4.3 Workflow through the States

The workflow is described in detail in a separate [Workflow Document][rfc-workflow].

### 4.4 Decision Process

The voting process is described in detail in a separate [Voting Document][rfc-voting].

## 5. Design Decisions

## 6. People

### 6.1 Editor(s)

* Niels Braczek, <niels.braczek@community.joomla.org>

### 6.2 Sponsors

* N/A

### 6.3 Contributors

* N/A

## 7. Votes

* **Entrance Vote:** _(not yet taken)_
* **Acceptance Vote:** _(not yet taken)_

## 8. Relevant Links

_**Note:** Order descending chronologically._

* [PHP FIG][]
* [Workflow Document][rfc-workflow]
* [Voting Document][rfc-voting]


[PHP FIG]: http://www.php-fig.org/
[ideas]: https://ideas.joomla.org
[rfc-workflow]: rfc-workflow.md
[rfc-voting]: rfc-voting.md

## 9. Errata

...
