---
v: 3

title: >
  The "dereferenceable identifier" pattern
abbrev: dereferenceable identifiers
docname: draft-bormann-t2trg-deref-id-latest
date: 2022-11-05

keyword: Internet-Draft
cat: info
stream: IRTF
wg: Thing-to-Thing Research Group

venue:
  mail: "t2trg@irtf.org"
  github: "cabo/deref-id"

author:
  -
    name: Carsten Bormann
    org: Universität Bremen TZI
    street: Postfach 330440
    city: Bremen
    code: D-28359
    country: Germany
    phone: +49-421-218-63921
    email: cabo@tzi.org

informative:
  JSO: I-D.bhutton-json-schema-01
  PROBLEM: I-D.ietf-httpapi-rfc7807bis-04


...

--- abstract

In a protocol or an application environment, it is often important to
be able to create unambiguous identifiers for some meaning (concept or
some entity).

Due to the simplicity of create URIs, these have become popular for
this purpose.
Beyond the purpose of identifiers to be uniquely associated with a
meaning, some of these URIs are in principle *dereferenceable*, so
something can be placed that can be retrieved when encountering such a
URI.

The present -00 version is a stub to draw some attention to the
opportunity that this pattern would benefit from a common description,
documenting its benefits and pitfalls, and some mitigations for the
latter.

--- middle

Introduction        {#intro}
============

(Please see abstract.)

Examples for "dereferenceable identifiers" {#examples}
======================

Protocol and Protocol Version identifiers
-----------------------------------------

Many protocols based on XML or JSON include a protocol or protocol
version identifier in the heading to a data item.

E.g., {{JSO}} defines a language for data models that contain an
identifier to the language version in use, here
https://json-schema.org/draft/2020-12/schema.
The model that can be retrieved from this URI in turn contained
further dereferenceable identifiers that point to further details.

{{Section 8.1.1 of JSO}} has this:

{:quote}
>
   If this URI identifies a retrievable resource, that resource SHOULD
   be of media type "application/schema+json".

So it acknowledges that the dereferenceability is optional, but does
place further restrictions on what can be the result of a successful
dereference.

Concept identifiers
-------------------

{{PROBLEM}} uses a dereferenceable identifier for its "type" field.
The value is a URI that "identifies the specific "problem type" (e.g.,
"out of credit")" {{Section 1 of PROBLEM}}.

{{Section 3.1.1 of PROBLEM}} has this:

{:quote}
>
   If the type URI is a locator (e.g., those with a "http" or "https"
   scheme), dereferencing it SHOULD provide human-readable documentation
   for the problem type (e.g., using HTML [HTML5]).

but then warns:

{:quote}
>
However, consumers
   SHOULD NOT automatically dereference the type URI, unless they do so
   when providing information to developers (e.g., when a debugging tool
   is in use).

{{Section 5 of PROBLEM}} further details:

{:quote}
>
   A problem's type URI SHOULD resolve to HTML [HTML5] documentation
   that explains how to resolve the problem.

This becomes even more interesting as {{Section 5.2 of PROBLEM}} then
gives this advice:

{:quote}
>
   Registrations MAY use the prefix "https://iana.org/assignments/http-
   problem-types#" for the type URI.

A reference to the place where registrations for these items are
managed is certainly desirable, however, the implications on the
management of fragment identifiers in the HTML documents the IANA
generates are an example for the increased complexity dereferenceable
identifiers may place on the owners of the URI space used.

MORE EXAMPLES
-------------

There are a lot of examples in published RFCs; add them to this document.

Pitfalls
========

Server overload
---------------

If a data item containing a dereferenceable identifier becomes widely
distributed, naive implementations that handle such a data item might
reference it out of a routine operation.
Many definitions of dereferenceable identifiers contain admonitions
that such a behavior can cause an implosion of requests on the
server(s) for the URI.

Longevity of identifiers
------------------------

URIs contain domain names, whose ownership can change.
Parts of the name space of an origin may come under new
administration, which can change the policies

While these are problems of URIs in general (and can be mitigated by
going to a non-dereferenceable URI), the problem is exacerbated by the
use as a dereferenceable identifier.  The new owner/administrator
might more easily accept that a certain chunk of their URI space
should not be used than that certain content is to be offered their
(potentially presenting non-trivial loads plus some update traffic).

Redirect ambiguities
--------------------

Dereferencing an identifier may involve following some redirections;
whether that is actually desired (or desirable) is rarely being
discussed.

IANA Considerations
==================

This document makes no concrete requests on IANA, but does point out
that IANA might be a good target for a certain class of
dereferenceable identifiers.

Security considerations
=======================

The ability to create a denial of service attack by pointing a
dereferenceable identifier into a popular data item that is widely
distributed is discussed in {{examples}}, alongside with some
recommendations on mitigating such attacks.

--- back

Acknowledgements
================
{: numbered="no"}

{{{Christian Amsüss}}} pointed out that this document would be good to have.

<!--  LocalWords:  dereference dereferenceability dereferenceable
 -->
