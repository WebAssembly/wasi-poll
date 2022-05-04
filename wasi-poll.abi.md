# Types

## <a href="#subscription" name="subscription"></a> `subscription`: record

The type of event to subscribe to.

Size: 40, Alignment: 8

### Record Fields

- <a href="subscription.info" name="subscription.info"></a> [`info`](#subscription.info): [`subscription-info`](#subscription_info)
  
  Information about the subscription.
  
- <a href="subscription.userdata" name="subscription.userdata"></a> [`userdata`](#subscription.userdata): [`userdata`](#userdata)
  
  The value of the `userdata` to include in associated events.
  
## <a href="#subscription_info" name="subscription_info"></a> `subscription-info`: variant

Information about events to subscribe to.

Size: 32, Alignment: 8

### Variant Cases

- <a href="subscription_info.monotonic_clock_timeout" name="subscription_info.monotonic_clock_timeout"></a> [`monotonic-clock-timeout`](#subscription_info.monotonic_clock_timeout): [`monotonic-clock-timeout`](#monotonic_clock_timeout)
  
  Set a monotonic clock timer.
  
- <a href="subscription_info.wall_clock_timeout" name="subscription_info.wall_clock_timeout"></a> [`wall-clock-timeout`](#subscription_info.wall_clock_timeout): [`wall-clock-timeout`](#wall_clock_timeout)
  
  Set a wall clock timer.
  
- <a href="subscription_info.read" name="subscription_info.read"></a> [`read`](#subscription_info.read): handle<descriptor>
  
  Wait for a readable stream to have data ready.
  
- <a href="subscription_info.write" name="subscription_info.write"></a> [`write`](#subscription_info.write): handle<descriptor>
  
  Wait for a writeable stream to be ready to accept data.
  
## <a href="#monotonic_clock_timeout" name="monotonic_clock_timeout"></a> `monotonic-clock-timeout`: record

Information about a monotonic clock timeout.

Size: 16, Alignment: 8

### Record Fields

- <a href="monotonic_clock_timeout.timeout" name="monotonic_clock_timeout.timeout"></a> [`timeout`](#monotonic_clock_timeout.timeout): [`instant`](#instant)
  
  An absolute or relative timestamp.
  
- <a href="monotonic_clock_timeout.is_absolute" name="monotonic_clock_timeout.is_absolute"></a> [`is-absolute`](#monotonic_clock_timeout.is_absolute): `bool`
  
  Specifies an absolute, rather than relative, timeout.
  
## <a href="#wall_clock_timeout" name="wall_clock_timeout"></a> `wall-clock-timeout`: record

Information about a wall clock timeout.

Size: 24, Alignment: 8

### Record Fields

- <a href="wall_clock_timeout.timeout" name="wall_clock_timeout.timeout"></a> [`timeout`](#wall_clock_timeout.timeout): [`datetime`](#datetime)
  
  An absolute or relative timestamp.
  
- <a href="wall_clock_timeout.is_absolute" name="wall_clock_timeout.is_absolute"></a> [`is-absolute`](#wall_clock_timeout.is_absolute): `bool`
  
  Specifies an absolute, rather than relative, timeout.
  
## <a href="#event" name="event"></a> `event`: record

An event which has occurred.

Size: 32, Alignment: 8

### Record Fields

- <a href="event.userdata" name="event.userdata"></a> [`userdata`](#event.userdata): [`userdata`](#userdata)
  
  The value of the `userdata` from the associated subscription.
  
- <a href="event.info" name="event.info"></a> [`info`](#event.info): [`event-info`](#event_info)
  
  Information about the event.
  
## <a href="#event_info" name="event_info"></a> `event-info`: variant

Information about an event which has occurred.

Size: 24, Alignment: 8

### Variant Cases

- <a href="event_info.monotonic_clock_timeout" name="event_info.monotonic_clock_timeout"></a> [`monotonic-clock-timeout`](#event_info.monotonic_clock_timeout)
  
  A monotonic clock timer expired.
  
- <a href="event_info.wall_clock_timeout" name="event_info.wall_clock_timeout"></a> [`wall-clock-timeout`](#event_info.wall_clock_timeout)
  
  A wall clock timer expired.
  
- <a href="event_info.read" name="event_info.read"></a> [`read`](#event_info.read): [`read-event`](#read_event)
  
  A readable stream has data ready.
  
- <a href="event_info.write" name="event_info.write"></a> [`write`](#event_info.write): [`write-event`](#write_event)
  
  A writable stream is ready to accept data.
  
## <a href="#read_event" name="read_event"></a> `read-event`: record

An event indicating that a readable stream has data ready.

Size: 16, Alignment: 8

### Record Fields

- <a href="read_event.nbytes" name="read_event.nbytes"></a> [`nbytes`](#read_event.nbytes): `u64`
  
  The number of bytes ready to be read.
  
- <a href="read_event.is_closed" name="read_event.is_closed"></a> [`is-closed`](#read_event.is_closed): `bool`
  
  Indicates the other end of the stream has disconnected and no further
  data will be available on this stream.
  
## <a href="#write_event" name="write_event"></a> `write-event`: record

An event indicating that a writeable stream is ready to accept data.

Size: 16, Alignment: 8

### Record Fields

- <a href="write_event.nbytes" name="write_event.nbytes"></a> [`nbytes`](#write_event.nbytes): `u64`
  
  The number of bytes ready to be accepted
  
- <a href="write_event.is_closed" name="write_event.is_closed"></a> [`is-closed`](#write_event.is_closed): `bool`
  
  Indicates the other end of the stream has disconnected and no further
  data will be accepted on this stream.
  
## <a href="#userdata" name="userdata"></a> `userdata`: `u64`

User-provided data provided with subscriptions that is copied back
into emitted events.

Size: 8, Alignment: 8

## <a href="#instant" name="instant"></a> `instant`: `u64`

A timestamp in nanoseconds.

TODO: When wit-bindgen supports importing types from other wit files, use
the type from wasi-clocks.

Size: 8, Alignment: 8

## <a href="#datetime" name="datetime"></a> `datetime`: record

A time and date in seconds plus nanoseconds.

TODO: When wit-bindgen supports importing types from other wit files, use
the type from wasi-clocks.

Size: 16, Alignment: 8

### Record Fields

- <a href="datetime.seconds" name="datetime.seconds"></a> [`seconds`](#datetime.seconds): `u64`
  
  
- <a href="datetime.nanoseconds" name="datetime.nanoseconds"></a> [`nanoseconds`](#datetime.nanoseconds): `u32`
  
  
# Functions

----

#### <a href="#poll_oneoff" name="poll_oneoff"></a> `poll-oneoff` 

##### Params

- <a href="#poll_oneoff.in" name="poll_oneoff.in"></a> `in`: list<[`subscription`](#subscription)>
##### Results

- <a href="#poll_oneoff.result" name="poll_oneoff.result"></a> `result`: list<[`event`](#event)>

