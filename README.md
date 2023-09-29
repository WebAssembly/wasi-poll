# WASI Poll

This wasi-poll repository has been subsumed by [wasi-io](https://github.com/WebAssembly/wasi-io).
Its contents, including the specification of the `poll-oneff` function, which has been renamed
to `poll-list`, has moved there.

---

A proposed [WebAssembly System Interface](https://github.com/WebAssembly/WASI) API.

### Current Phase

WASI-poll is currently in [Phase 2].

[Phase 2]: https://github.com/WebAssembly/WASI/blob/42fe2a3ca159011b23099c3d10b5b1d9aff2140e/docs/Proposals.md#phase-2---proposed-spec-text-available-cg--wg

### Champions

- Dan Gohman

### Phase 4 Advancement Criteria

WASI poll must have host implementations which can pass the testsuite
on at least Windows, macOS, and Linux.

WASI poll must have at least two complete independent implementations.

## Table of Contents [if the explainer is longer than one printed page]

- [Introduction](#introduction)
- [Goals](#goals)
- [Non-goals](#non-goals)
- [API walk-through](#api-walk-through)
  - [Use case 1](#use-case-1)
  - [Use case 2](#use-case-2)
- [Detailed design discussion](#detailed-design-discussion)
  - [[Tricky design choice 1]](#tricky-design-choice-1)
  - [[Tricky design choice 2]](#tricky-design-choice-2)
- [Considered alternatives](#considered-alternatives)
  - [[Alternative 1]](#alternative-1)
  - [[Alternative 2]](#alternative-2)
- [Stakeholder Interest & Feedback](#stakeholder-interest--feedback)
- [References & acknowledgements](#references--acknowledgements)

### Introduction

WASI Poll is a WASI API for waiting for I/O events on multiple handles.

It is similar in spirit to the POSIX `poll` function.

### Goals

The primary goal of WASI Poll is to allow users to use WASI programs to
be able to wait for stream read, stream write, stream error, and clock timeout
events, on multiple handles.

### Non-goals

WASI Poll is not yet aiming to support large numbers of handles efficiently.
Future proposals will ideally add something similar to Linux's `epoll`, but
that is not yet addressed.

### API walk-through

[Walk through of how someone would use this API.]

#### [Use case 1]

[Provide example code snippets and diagrams explaining how the API would be used to solve the given problem]

#### [Use case 2]

[etc.]

### Detailed design discussion

[This section should mostly refer to the .wit.md file that specifies the API. This section is for any discussion of the choices made in the API which don't make sense to document in the spec file itself.]

### Why is the function called `poll_oneoff`?

This is referencing the fact that this function is not efficient when used
repeatedly with the same large set of handles. In the future, it is expected
that follow-up proposals will add a poll function which can create sets of
handles that can be polled together efficiently.

### Why doesn't the return type have a way to indicate failure?

`poll_oneoff` itself never fails. It may be interrupted, and there may be
errors on the I/O resources referred to by the handles passed to it, but
the poll isn't doing any I/O of its own, so it has no need to fail.

### Considered alternatives

[This section is not required if you already covered considered alternatives in the design discussion above.]

#### [Alternative 1]

[Describe an alternative which was considered, and why you decided against it.]

#### [Alternative 2]

[etc.]

### Stakeholder Interest & Feedback

TODO before entering Phase 3.

[This should include a list of implementers who have expressed interest in implementing the proposal]

### References & acknowledgements

Many thanks for valuable feedback and advice from:

- [Person 1]
- [Person 2]
- [etc.]
