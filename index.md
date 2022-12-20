# Joomla Feature / Specification RFCs

According to the [Joomla RFC Workflow Bylaw][workflow] each Joomla RFC has a
status as it is being worked on. Once a proposal has passed the Entrance Vote it
will be listed here as "Draft". Unless a Joomla Feature / Specification RFC is marked
as "Accepted" it is subject to change. Draft can change drastically, but Review will
only have minor changes.

As also described in the [Joomla RFC Workflow Bylaw][workflow], the editor(s) of a
proposal are essentially the lead contributors and writers of the Joomla Feature /
Specification RFCs and they are supported by at least one voting member, the sponsor.
The sponsor is responsible for managing the review stage and votes.

## Index by Status

### Accepted

| Num | Title                          | Editor                  | Sponsor           |
|:---:|--------------------------------|-------------------------|-------------------|
| 0 | [RFC Procedure][rfc-procedure] | Niels Braczek <niels.braczek@community.joomla.org> | Marco Dings <marco.dings@community.joomla.org> |

### Review

| Num | Title                          | Editor                  | Sponsor           |
|:---:|--------------------------------|-------------------------|-------------------|
| N/A | N/A                            | N/A                     | N/A               |

### Draft

| Num | Title                                   | Editor                                              | Sponsor                                                                |
|:---:|-----------------------------------------|-----------------------------------------------------|------------------------------------------------------------------------|
|  1  | [Decpoupling Output][decoupling-output] | Niels Braczek <niels.braczek@community.joomla.org>  | Llewellyn van der Merwe <llewellyn.van-der-merwe@community.joomla.org> |
|  2  | [Form Admin][form-admin]                | Niels Braczek <niels.braczek@community.joomla.org>  | Llewellyn van der Merwe <llewellyn.van-der-merwe@community.joomla.org> |
|  3  | [Simple CCK][simple-cck]                | Niels Braczek <niels.braczek@community.joomla.org>  | Llewellyn van der Merwe <llewellyn.van-der-merwe@community.joomla.org> |

### Pre-Draft

| Num | Title                          | Editor                           | Sponsor           |
|:---:|--------------------------------|----------------------------------|-------------------|
| N/A | [Content Elements][contentelements]  | Niels Braczek <niels.braczek@community.joomla.org> | N/A |
| N/A | [Authorisation Service][authorisation]  | Niels Braczek <niels.braczek@community.joomla.org> | N/A |
| N/A | [Joomla Command Line][joomla-cli]  | Roland Dalmulder <roland.dalmulder@commnity.joomla.org> | N/A |
| N/A | [Mobile App][mobile-app]  | Elisa Foltyn <elisa.foltyn@community.joomla.org> | N/A |
| N/A | [Simplify Admin Views*][simplify-admin]  | Elisa Foltyn <elisa.foltyn@community.joomla.org> | N/A |
| N/A | [Simplify Admin Views*][simplify-admin2]  | Astrid Günther <astrid.guenther@community.joomla.org> | N/A |
| N/A | [Composer support][composer]  | Astrid Günther <astrid.guenther@community.joomla.org> | N/A |

*) Two different proposals on the same target, need to be merged 

### Deprecated

| Num | Title                          | Editor                  | Sponsor           |
|:---:|--------------------------------|-------------------------|-------------------|
| N/A | N/A                            | N/A                     | N/A               |

### Rejected

| Title                       | Editor                  | Sponsor           |
|-----------------------------|-------------------------|-------------------|
| [Append Form][append-form] | Niels Braczek <niels.braczek@community.joomla.org>  | Llewellyn van der Merwe <llewellyn.van-der-merwe@community.joomla.org> |

## Numerical Index

| Status | Num | Title                                   | Editor                                             | Sponsor           |
|--------|:---:|-----------------------------------------|----------------------------------------------------|-------------------|
| A      |  0  | [RFC Procedure][rfc-procedure]          | Niels Braczek <niels.braczek@community.joomla.org> | Marco Dings <marco.dings@community.joomla.org> |
| D      |  1  | [Decpoupling Output](decoupling-output) | Niels Braczek <niels.braczek@community.joomla.org> | Llewellyn van der Merwe <llewellyn.van-der-merwe@community.joomla.org> |
| D      |  2  | [Form Admin](form-admin)                | Niels Braczek <niels.braczek@community.joomla.org> | Llewellyn van der Merwe <llewellyn.van-der-merwe@community.joomla.org> |
| D      |  3  | [Simple CCK](simple-cck)                | Niels Braczek <niels.braczek@community.joomla.org> | Llewellyn van der Merwe <llewellyn.van-der-merwe@community.joomla.org> |

_**Legend:** A = Accepted | D = Draft | P = Pre-Draft | R = Review | X = Deprecated_

[workflow]: bylaws/workflow.md
[contentelements]: https://github.com/joomla/rfc/tree/master/proposed
[authorisation]: https://github.com/joomla/rfc/pull/2
[joomla-cli]: https://github.com/joomla/rfc/pull/4
[mobile-app]: https://github.com/joomla/rfc/pull/5
[simplify-admin]: https://github.com/joomla/rfc/pull/6
[simplify-admin2]: https://github.com/joomla/rfc/pull/7
[composer]: https://github.com/joomla/rfc/pull/8
[rfc-procedure]: https://github.com/joomla/rfc/blob/master/accepted/RFC-0-rfc-meta.md
[decoupling-output]: https://github.com/joomla/rfc/pull/36
[form-admin]: https://github.com/joomla/rfc/pull/31
[simple-cck]: https://github.com/joomla/rfc/pull/26
[append-form]: https://github.com/joomla/rfc/pull/18
