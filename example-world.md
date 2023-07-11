<h1><a name="example_world">World example-world</a></h1>
<ul>
<li>Imports:
<ul>
<li>interface <a href="#wasi:poll_poll"><code>wasi:poll/poll</code></a></li>
</ul>
</li>
</ul>
<h2><a name="wasi:poll_poll">Import interface wasi:poll/poll</a></h2>
<p>A poll API intended to let users wait for I/O events on multiple handles
at once.</p>
<hr />
<h3>Types</h3>
<h4><a name="pollable"><code>resource pollable</code></a></h4>
<h5>Resource Members</h5>
<p>TODO</p>
<hr />
<h3>Functions</h3>
<h4><a name="poll_oneoff"><code>poll-oneoff: func</code></a></h4>
<p>Poll for completion on a set of pollables.</p>
<p>This function takes a list of pollables, which identify I/O sources of
interest, and waits until one or more of the events is ready for I/O.</p>
<p>The result <code>list&lt;bool&gt;</code> is the same length as the argument
<code>list&lt;pollable&gt;</code>, and indicates the readiness of each corresponding
element in that list, with true indicating ready. A single call can
return multiple true elements.</p>
<p>A timeout can be implemented by adding a pollable from the
wasi-clocks API to the list.</p>
<p>This function does not return a <code>result</code>; polling in itself does not
do any I/O so it doesn't fail. If any of the I/O sources identified by
the pollables has an error, it is indicated by marking the source as
ready in the <code>list&lt;bool&gt;</code>.</p>
<p>The &quot;oneoff&quot; in the name refers to the fact that this function must do a
linear scan through the entire list of subscriptions, which may be
inefficient if the number is large and the same subscriptions are used
many times. In the future, this is expected to be obsoleted by the
component model async proposal, which will include a scalable waiting
facility.</p>
<h5>Params</h5>
<ul>
<li><a name="poll_oneoff.in"><code>in</code></a>: list&lt;own&lt;<a href="#pollable"><a href="#pollable"><code>pollable</code></a></a>&gt;&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="poll_oneoff.0"></a> list&lt;<code>bool</code>&gt;</li>
</ul>
