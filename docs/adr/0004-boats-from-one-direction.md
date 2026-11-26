# Boats come from one direction only

The river side has one approach, one boat signal and one channel sensor, and one boat passes per opening. Boats from both sides would need a second approach and signal, an ordering between sides, and a boat-vs-boat race. We chose the brief's "small, explicitly simplified model with thorough tests" instead. The required race scenario therefore comes from elsewhere: a boat entering the channel just as its give-up time ends. Adding the second direction later means changing the river controller's sensors and state machine.
