# Liftbridge controller: specification

# Context
what the controller does; its sensors, actuators and users.

# Functional requirements
the users' journeys (J1, J2, …, a sentence each), and the alternative and exception flows that can happen in them (A1, E1, …), each with what the controller does.

# Non-functional requirements
temporal properties (P1, P2, …), each one sentence that can be checked on a log, with the hazard it guards against, and its times as named values ("within RESPONSE_LIMIT = 11 s"). Ask of every journey what must never happen (safety) and what must happen within a time limit (bounded response), and cover faults and the shared resource too.

# Constraints, assumptions and exclusions
on the solution, on the environment, and what you leave out.

# Design
a structural diagram (communication, component or class diagram), a state machine for each concurrent component with its transitions numbered, and a sequence diagram of the main scenario, all as text (Mermaid or PlantUML); a table of the messages; how the shared resource is requested, granted and released; and the main design decisions (D1, D2, …), each with its rationale.
