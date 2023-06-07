# <a name="example_world">World example-world</a>


 - Imports:
    - interface `wasi:poll/poll`

## <a name="wasi:poll_poll">Import interface wasi:poll/poll</a>

A poll API intended to let users wait for I/O events on multiple handles
at once.

----

### Types

#### <a name="pollable">`type pollable`</a>
`u32`
<p>A "pollable" handle.

This is conceptually represents a `stream<_, _>`, or in other words,
a stream that one can wait on, repeatedly, but which does not itself
produce any data. It's temporary scaffolding until component-model's
async features are ready.

And at present, it is a `u32` instead of being an actual handle, until
the wit-bindgen implementation of handles and resources is ready.

`pollable` lifetimes are not automatically managed. Users must ensure
that they do not outlive the resource they reference.

This [represents a resource](https://github.com/WebAssembly/WASI/blob/main/docs/WitInWasi.md#Resources).

----

### Functions

#### <a name="drop_pollable">`drop-pollable: func`</a>

Dispose of the specified `pollable`, after which it may no longer
be used.

##### Params

- <a name="drop_pollable.this">`this`</a>: [`pollable`](#pollable)

#### <a name="poll_oneoff">`poll-oneoff: func`</a>

Poll for completion on a set of pollables.

The "oneoff" in the name refers to the fact that this function must do a
linear scan through the entire list of subscriptions, which may be
inefficient if the number is large and the same subscriptions are used
many times. In the future, this is expected to be obsoleted by the
component model async proposal, which will include a scalable waiting
facility.

Returns a list<bool>, which is the same length as the list<pollablke>
arguments. Each element corresponds to the readiness of the element
at the same index in the list of pollables.

##### Params

- <a name="poll_oneoff.in">`in`</a>: list<[`pollable`](#pollable)>

##### Return values

- <a name="poll_oneoff.0"></a> list<`bool`>

