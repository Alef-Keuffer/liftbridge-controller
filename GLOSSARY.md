# Lift bridge

A lift bridge carries a road over a canal. Its span is shared between cars, which need it down, and boats, which need it raised.

## Language

### Traffic

**Car**:
Any road vehicle that crosses the bridge.
_Avoid_: vehicle, driver

**Boat**:
Any vessel on the canal. Every boat needs the span raised to pass under the bridge.
_Avoid_: ship, vessel, skipper

### The bridge

**Span**:
The movable part of the bridge that carries the road. It is down, raised, or moving between the two.
_Avoid_: deck, leaf, "open" or "closed" for the span (ambiguous: an open bridge is closed to cars)

**Channel**:
The stretch of canal under the span.
_Avoid_: fairway, passage, waterway

**Approach**:
The stretch of canal before the bridge, where a boat waits for the boat signal. Boats come from one side only.
_Avoid_: queue, waiting area

**Clear**:
Said of the span when no car is on it, and of the channel when no boat is in it.
_Avoid_: empty, free

**Barriers**:
The road gates at both ends of the span. They move and are confirmed together, as one.
_Avoid_: gates, booms

**Road light**:
The traffic light that lets cars onto the span: green or red only.
_Avoid_: traffic light, road signal

**Road open**:
The road light is green and the barriers are up. **Road closed**: the road light is red and the barriers are down.
_Avoid_: bridge open, bridge closed

**Boat signal**:
The light that lets a boat pass under the span: green or red.
_Avoid_: river light, boat light

### Controllers

**Road controller**:
The component in charge of the road side: the road light, the barriers, and the sensor that tells whether the span is clear.
_Avoid_: car controller, traffic controller

**River controller**:
The component in charge of the river side: the approach sensor, the boat signal, and the sensor that tells whether the channel is clear.
_Avoid_: boat controller, canal controller

**Span controller**:
The component that owns the span: it alone moves it, and it decides whether the road or the river holds it.
_Avoid_: coordinator, interlocker, bridge controller

### Sharing the span

**Holder**:
The side, road or river, currently allowed to use the span. The road is the holder at rest.
_Avoid_: owner

**Revoke**:
The span controller's demand that the road give the span back so that a boat can pass.
_Avoid_: preempt, close request

**Opening**:
One full cycle for one boat: the road closes, the span rises, the boat passes, the span lowers, and the road reopens.
_Avoid_: lift, raise cycle, bridge opening

**Clearance time**:
The wait after the road light turns red before the span is trusted to be clear, so that a car that just passed the light has reached the span.
_Avoid_: amber time, grace period

### Faults

**Fault**:
The latched state of a component that commanded a movement and saw no confirmation in time. It lasts until restart.
_Avoid_: error, failure

**Alarm**:
The warning raised when a component enters a fault.
_Avoid_: siren
