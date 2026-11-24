## A. System and ECU requirements

| ID | Requirement | Priority | Acceptance criterion |
|---|---|---|---|
| SYS-001 | The system shall implement three independent logical ECUs. | P0 | All three execute their own state and message-processing logic. |
| SYS-002 | Each ECU shall have a defined responsibility and interface. | P0 | Interface documentation exists for every ECU. |
| SYS-003 | ECU application logic shall be independent of the physical CAN driver. | P0 | The same core logic runs against a virtual and hardware transport adapter. |
| SYS-004 | Each ECU shall initialize into a defined safe state. | P0 | Startup tests verify outputs and communication state before normal operation. |
| SYS-005 | Each ECU shall support reset and reinitialization. | P1 | After reset, the ECU returns to a defined state and resumes permitted communication. |
| SYS-006 | Runtime behavior shall be observable through logs and diagnostics. | P0 | Every injected fault produces a traceable event or documented reason for no event. |

## B. CAN communication requirements

| ID | Requirement | Priority | Acceptance criterion |
|---|---|---|---|
| CAN-001 | Every application message shall have a defined CAN identifier and payload layout. | P0 | No duplicate IDs among messages that coexist in the same network configuration. |
| CAN-002 | Every signal shall define its bit position, width, byte order, scaling, offset and valid range where applicable. | P0 | Encoding and decoding tests match published test vectors. |
| CAN-003 | Periodic messages shall use configured transmission intervals. | P0 | Measured intervals remain within defined tolerances under the specified test load. |
| CAN-004 | Receivers shall validate message identifiers, payload lengths and signal ranges. | P0 | Malformed or invalid inputs are rejected or handled according to documented rules. |
| CAN-005 | Receivers shall detect stale data and missing periodic messages. | P0 | Timeout tests detect missing messages within the configured deadline. |
| CAN-006 | The implementation shall handle transmit queue saturation and receive buffer exhaustion. | P1 | Overflow is detected, counted and handled without memory corruption. |
| CAN-007 | The network shall define message priorities and an arbitration-aware ID allocation scheme. | P1 | Design documentation explains priority choices and worst-case considerations. |
| CAN-008 | The application shall expose counters for transmission errors, receive errors, timeouts and dropped frames where measurable. | P1 | Counters are observable and tested. |
| CAN-009 | The hardware implementation shall handle controller error states and bus-off recovery. | P1 | Hardware tests demonstrate fault detection and documented recovery behavior. |
| CAN-010 | The protocol shall support versioned message definitions or an explicit compatibility policy. | P2 | Incompatible message versions are detected or rejected according to the policy. |

## C. ECU behavior requirements

| ID | Requirement | Priority | Acceptance criterion |
|---|---|---|---|
| ECU-001 | The Powertrain ECU shall publish simulated engine RPM and vehicle speed. | P0 | Values update at configured rates and remain within documented limits. |
| ECU-002 | The Body ECU shall manage door and lighting states. | P0 | Input events produce the expected state changes and CAN messages. |
| ECU-003 | The Dashboard ECU shall consume vehicle signals and generate display and warning states. | P0 | Displayed values agree with valid source signals; stale data produces a defined warning. |
| ECU-004 | Each ECU shall implement an explicit state machine. | P0 | Valid and invalid state transitions are covered by tests. |
| ECU-005 | The Dashboard ECU shall distinguish normal, stale and invalid signals. | P0 | Each condition maps to a documented behavior. |
| ECU-006 | ECUs shall start and stop independently without crashing other logical ECUs. | P1 | Resetting or stopping one ECU does not corrupt other ECU state. |
| ECU-007 | Signals shall have defined startup values and invalid/unavailable representations where needed. | P1 | Startup and invalid-value test cases produce predictable results. |
| ECU-008 | The system shall support configurable simulation scenarios. | P1 | A scenario file can control inputs and timing without changing application source code. |

## D. Diagnostics and fault management

| ID | Requirement | Priority | Acceptance criterion |
|---|---|---|---|
| DIA-001 | Each ECU shall maintain a diagnostic trouble code (DTC) store. | P0 | Defined faults create the expected diagnostic records. |
| DIA-002 | Faults shall have defined detection, confirmation and clearing rules. | P0 | Tests verify transitions from normal to faulted and back. |
| DIA-003 | A diagnostic client shall be able to request supported diagnostic information. | P0 | Valid requests return correct data; invalid requests return defined errors. |
| DIA-004 | The system shall record relevant fault occurrence and recovery events. | P0 | Logs identify the ECU, fault type and event sequence. |
| DIA-005 | Diagnostic requests shall have timeouts and malformed-request handling. | P0 | Invalid or incomplete requests do not crash an ECU. |
| DIA-006 | The diagnostic system shall expose supported services and data identifiers. | P1 | A protocol document lists services, request formats and responses. |
| DIA-007 | The project shall implement a subset of UDS-inspired diagnostic services. | P1 | At minimum, read supported data and read or clear DTCs through a documented interface. |
| DIA-008 | Diagnostic access control shall be documented if protected services are implemented. | P2 | Protected operations reject unauthorized requests in the selected threat model. |

## E. Fault injection and resilience requirements

| ID | Requirement | Priority | Acceptance criterion |
|---|---|---|---|
| FLT-001 | The test environment shall be able to stop or suppress selected periodic messages. | P0 | The receiving ECU detects the resulting timeout. |
| FLT-002 | The system shall support out-of-range and stale signal injection. | P0 | The receiving application follows its documented rejection or fallback rules. |
| FLT-003 | The system shall support independent ECU restart simulation. | P0 | Restart behavior and message recovery are observable. |
| FLT-004 | The system shall support invalid diagnostic requests. | P0 | Invalid requests receive a defined response or controlled rejection. |
| FLT-005 | The system shall simulate a CAN bus outage. | P1 | Communication loss is detected, and recovery behavior is tested. |
| FLT-006 | The system shall detect queue overflows and resource exhaustion. | P1 | Failures are counted and handled without undefined behavior. |
| FLT-007 | The system shall generate repeatable fault scenarios. | P1 | The same scenario produces comparable event sequences across repeated runs. |
| FLT-008 | The physical implementation shall test controller error states and bus-off recovery. | P1 | A documented hardware test validates the actual controller behavior. |

## Non-functional requirements (timing and performance)

| ID | Requirement | Initial target |
|---|---|---|
| NFR-001 | Periodic message scheduling | Support configurable 10 ms, 20 ms, 100 ms and 1 s message periods. |
| NFR-002 | Receive processing latency | Measure latency from frame reception to application handling; establish and document a target per deployment. |
| NFR-003 | Timeout detection | Detect a missing message within its configured timeout plus a documented scheduling tolerance. |
| NFR-004 | CPU utilization | Measure worst observed load under nominal and fault-injection scenarios. |
| NFR-005 | Buffer management | Demonstrate bounded memory usage during sustained operation. |
| NFR-006 | Long-duration stability | Run a continuous simulation for at least 2 hours without crashes, deadlocks or unexplained resource growth. |
