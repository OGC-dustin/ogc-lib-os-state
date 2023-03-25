# OGC.Engineering
## ogc-lib-os-state - State Machine
Developer contact - dustin < at > ogc.engineering

---
https://en.wikipedia.org/wiki/Finite-state_machine

A finite-state machine (FSM) or finite-state automaton (FSA, plural: automata), finite automaton, or simply a state
machine, is a mathematical model of computation. It is an abstract machine that can be in exactly one of a finite
number of states at any given time. The FSM can change from one state to another in response to some inputs; the change
from one state to another is called a transition. An FSM is defined by a list of its states, its initial state, and the
inputs that trigger each transition.

---

Library provides functions to transition between states, each state needs to can have an on_entry() and on_exit()
function to construct and tear down needed resources.  If the state exits without initiating a transition its state
function will be recalled.  A transition request will immediately trigger the current states on_exit() function,
library tracking logic will transition to the new state and the on_entry() function will be called before calling the
new state function.

---
Requirements:

---

- the DEPLOYMENT/PROJECT layer(folder) must contain:
    - app.h header that redirects to the primary application ( because multiple applications are possible )

- the APP layer(folder) must define:
    - void app_init( void );
        - The function app_init() must initialize the state tracking structure and define the initial state

- the HAL layer(folder) must define:
    - void hal_config ( void );
        - configuration of the watchdog, clocks, pins, and other things that do not require the state machine
    - void hal_init( void );
        - initialization of hal level interrupt events that run in interrupt context
