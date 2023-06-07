<h1><a name="example_world">World example-world</a></h1>
<ul>
<li>Imports:
<ul>
<li>interface <a href="#poll"><code>poll</code></a></li>
</ul>
</li>
</ul>
<h2><a name="poll">Import interface poll</a></h2>
<p>A poll API intended to let users wait for I/O events on multiple handles
at once.</p>
<hr />
<h3>Types</h3>
<h4><a name="pollable"><code>type pollable</code></a></h4>
<p><code>u32</code></p>
<p>A "pollable" handle.
<p>This is conceptually represents a <code>stream&lt;_, _&gt;</code>, or in other words,
a stream that one can wait on, repeatedly, but which does not itself
produce any data. It's temporary scaffolding until component-model's
async features are ready.</p>
<p>And at present, it is a <code>u32</code> instead of being an actual handle, until
the wit-bindgen implementation of handles and resources is ready.</p>
<p><a href="#pollable"><code>pollable</code></a> lifetimes are not automatically managed. Users must ensure
that they do not outlive the resource they reference.</p>
<p>This <a href="https://github.com/WebAssembly/WASI/blob/main/docs/WitInWasi.md#Resources">represents a resource</a>.</p>
<hr />
<h3>Functions</h3>
<h4><a name="drop_pollable"><code>drop-pollable: func</code></a></h4>
<p>Dispose of the specified <a href="#pollable"><code>pollable</code></a>, after which it may no longer
be used.</p>
<h5>Params</h5>
<ul>
<li><a name="drop_pollable.this"><code>this</code></a>: <a href="#pollable"><a href="#pollable"><code>pollable</code></a></a></li>
</ul>
<h4><a name="poll_oneoff"><code>poll-oneoff: func</code></a></h4>
<p>Poll for completion on a set of pollables.</p>
<p>The &quot;oneoff&quot; in the name refers to the fact that this function must do a
linear scan through the entire list of subscriptions, which may be
inefficient if the number is large and the same subscriptions are used
many times. In the future, this is expected to be obsoleted by the
component model async proposal, which will include a scalable waiting
facility.</p>
<p>Note that the return type would ideally be <code>list&lt;bool&gt;</code>, but that would
be more difficult to polyfill given the current state of <code>wit-bindgen</code>.
See <a href="https://github.com/bytecodealliance/preview2-prototyping/pull/11#issuecomment-1329873061">https://github.com/bytecodealliance/preview2-prototyping/pull/11#issuecomment-1329873061</a>
for details.  For now, we use zero to mean &quot;not ready&quot; and non-zero to
mean &quot;ready&quot;.</p>
<h5>Params</h5>
<ul>
<li><a name="poll_oneoff.in"><code>in</code></a>: list&lt;<a href="#pollable"><a href="#pollable"><code>pollable</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="poll_oneoff.0"></a> list&lt;<code>u8</code>&gt;</li>
</ul>