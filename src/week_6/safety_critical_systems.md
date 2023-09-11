# Safety Critical Systems
A safety-critical system is a system whose failure or malfunction may result in
one (or more) of the following outcomes:
- Death or series injury
- Loss or severe damage to equipment/property
- Environmental harm

Safety-critical systems are increasingly becoming computer based. A safety-related
system comprises everything (hardware, software, and human aspects) needed to 
perform one or more safety functions.

## Safety Critical Software
Software by itself is neither safe nor unsafe; however, when it is part of a
safety-critical system, it can cause or contribute to unsafe conditions. Such
software is considered safety critical.

According to IEEE, safety-critical software is 

> Software whose use in a system can result in unacceptable risk. Safety-critical 
software includes software whose operation or failure to operate can lead to a 
hazardous state, software intended to recover from hazardous states, and software 
intended to mitigate the severity of an accident.

Software based systems are used in many applications where a failure could increase
the risk of injury or even death. The lower risk systems such as an oven temperature
controller are safety related, whereas the higher risk systems such as the interlocking
between railway points and signals are safety critical.

Although software failures can be safety-critical, the use of software control 
systems contributes to increased system safety. Software monitoring and control
allows a wider range of conditions to be monitored and controlled than is possible
using electro-mechanical safety systems. Software can also detect and correct
safety-critical operator errors.

## System Dependability
For many computer-based systems, the most important system property is the dependability
of the system. The dependability of a system reflects the users degree of trust
in that system. It reflects the extent of the users confidence that it will operate
as users expect and that it will not fail in normal use.

System failures may have widespread effects with large numbers of people affected
by the failure. The costs of a system failure may be very high if the failure
leads to economic losses or physical damage. Dependability covers the related 
systems attributes of reliablity, availability, safety, and security. These are
inter-dependent.

- **Availability**: The ability of the system to deliver services when requested.
Availability is expressed as probability: a percentage of the time that the system
is available to deliver services.
- **Reliablity**: The ability of the system to deliver services as specified.
Reliablity is also expressed as probability.
- **Safety**: The ability of the system to operate without catastrophic failure
threating people or the environment. Reliablity and availability are necessary
but not sufficient conditions for system safety.
- **Security**: The ability of the system to protect itself against accidental
or deliberate intrusion.

## How to Achieve Safety?
- **Hazard avoidance**: The system is designed so that some classes of hazard 
simply cannot arise.
- **Hazard detection and removal**: The system is designed so that hazards are
detected and removed before they result in an accident.
- **Damage limitation**: The system includes protection features that minimise
the damage that may result from an accident.

## How Safe is Safe Enough?
Accidents are inevitable, achieving complete safety is impossible in complex systems.
Accidents in complex systems rarely have a single cause as these systems are designed
to be resilient to a single point of failure. This means that almost all accidents
are a result of combinations of malfunctions rather than single failures. It is
probably the case that anticipating all problem combinations, especially, in software
controlled systems is impossible so achieving complete safety is impossible.

The answer depends greatly on the different industries:
- "How much should we spend to avoid fatal accidents on the roads or railways?"
- "What probability of failure should we permit for the protection system of this
nuclear reactor?"
- "What probability of failure should we permit for safety-critical aircraft
components?"

## Dependability Costs
Dependability costs tend to increase exponentially as increasing levels of dependability
are required. There are two main reasons behind this:
1. The use of more expensive development techniques and hardware that are required
to achieve the higher levels of dependability.
2. The increased testing and system validation that is required to convince the 
system client and regulators that the required levels of dependability have been
achieved.

Due to the very high costs of dependability achievement, it may be more cost effective
to accept untrustworthy systems and pay for failure costs.

## Causes of Failure
- **Hardware failure**: Hardware fails because of design and manufacturing errors 
or because components have reached the end of their natural life.
- **Software failure**: Software fails due to errors in its specification, design
or implementation.
- **Operational failure**: Human operators make mistakes. They are currently perhaps 
the largest single cause of system failures in socio-technical systems.

## Hazards and Risks
A hazard is anything that may cause harm. Hazard analysis attempts to identify
all the dangerous states. A risk is the combination of the probability that the
hazard will lead to an accident and the likely severity of the accident if it occurs.
For each hazard, the risk is assessed and if the risk is not acceptable but can
be made tolerable, measures must be introduces to reduce it.

## Faults and Failures
A fault is an abnormal condition/defect that may lead to failure. A failure is 
the inability of the component, subsystem, or system to perform its intended function
as designed. A failure may be the resut of one or more faults.

Fault Tree Analysis (FTA) considers how a failure may arise. Failure Modes and
Effects Analysis (FMEA) analyses the ways in which each component could fail, and
considers the effect this will have on the system.

## Safety Standards
Below are a few commonly used standards. All standards are process based. Process
alone does not guarantee quality however, they can only help reduce the risk.

| Standard       | Purpose                                          | Sector     |
| -------------- | ------------------------------------------------ | ---------- |
| ISO9001        | General quality management system.               | All        |
| ISO27001       | Information security standard.                   | All        |
| ISO13485       | Quality management system.                       | Medical    |
| IEC61508       | Functional safety.                               | All        |
| IEC62304       | Software lifecycle.                              | Medical    |
| ISO14971       | Risk management.                                 | Medical    |
| FDA GMP        | Quality system regulation.                       | Medical    |
| ISO/TR80002    | Application of 14971 to medical device software. | Medical    |
| Def-Stan 55/56 | Procurement of safety critical software.         | Defence    |
| IEC80001       | Risk management - IT networks.                   | Medical    |
| IEC60601       | Requirements for safety.                         | Medical    |
| ISO26262       | Automative software safety.                      | Automotive |

IEC61508 is an umbrella standard for functional safety across all industries.
Compliance to IEC61508 ensures compliance with industry specific safety standards.
IEC61508 has the following views on risks:
- Zero risk can never be reached, only probabilities can be reduced.
- Non-tolerable risks must be reduced (ALARP - as low as reasonably possible).
- Optimal, cost effective safety is achieved when addressed in the entire safety
lifecycle.

The IEC61508 standard defines three successive tiers of safety assessment:
- Safety Instrumented System (SIS): The entire system.
- Safety Instrumented Functions (SIF): A singular component.
- Safety Integrity Level (SIL): The safety integrity level of a specific SIF which
is being implemented by an SIS.

## Functional Safety
The functional safety goal is the goal that an automatic safety function will perform
the intended function correctly or the system will fail in a predictable (safe)
manner. 

It will either:
- perform the intended function correctly (reliable)
- or, fail in a predictable manner (safe)

## Real-time Operating System (RTOS) Areas of Concern
- Tasking:
    - Task terminates or is deleted.
    - Overflow of Kernel's storage area for task control blocks.
    - Task stack size is exceeded.
- Scheduling:
    - Deadlocks.
    - Tasks spawn additional tasks that starve CPU resources.
    - Service calls with unbounded execution times.
- Memory and I/O device access:
    - An incorrect pointer referencing/dereferncing.
    - Data overwrite.
    - Unauthorised access to critical system devices.
- Queueing:
    - Overflow of Kernel work queue.
    - Task queue.
    - Message queue.
- Interrupts and exceptions:
    - No interrupt handler.
    - No exception handler.
    - Improper protection of supervisor task.

## Software Planning Process
The purpose of software planning is to determine what will be done to produce
safe, requirements-based software.

The expected outputs are:
- A plan for Software Aspects of Certification (PSAC).
- Software development plan.
- Software verification plan.
- Software configuration management plan.
- Software quality assurance plan.

The software development process is broken down into four sub-processes:
- **Software requirement process**: High-level requirements in relation to function,
performance, interface, and safety.
- **Software design process**: Low-level requirements used to implement the source
code.
- **Software coding process**: Production of source-code from the design process.
- **Integration process**: Integration of code into a real-time environment.

The following tangible outputs are the result of the combined four sub-processes:
- Software requirements data.
- Software design description.
- Source code.
- Executable object code.

## C Coding Standards
| Coding Standard        | C Standard  | Security Standard | Safety Standard | International Standard | Whole Language |
| ---------------------- | ----------- | ----------------- | --------------- | ---------------------- | -------------- |
| CWE                    | None/All    | Yes               | No              | No                     | N/A            |
| MISRA 2012 Amendment 2 | C99/C11/C18 | No                | Yes             | No                     | No             |
| CERT C                 | C99/C11     | Yes               | No              | No                     | Yes            |
| ISO/IEC TS 17961       | C11         | Yes               | No              | Yes                    | Yes            |

## MISRA C
MISRA - The Motor Industry Software Reliability Association - provides coding
standards for developing safety-critical systems. MISRA C is a set of software
development guidelines for the C programming language developed by The MISRA Consortium.
It is not for finding bugs, rather for preventing unsafe coding habits.

Although originating from the automotive industry, it has evolved as a widely 
accepted model for best practices by leading developers in sectors including
automotive, aerospace, telecom, medical devices, defense, railway, and more.

MISRA C has trhee categories of guidelines:
1. **Mandatory**: You must follow these, no exceptions permitted.
2. **Required**: You must follow these but there can be execptions in certain cases.
3. **Advisory**: You must try to follow these but they are not mandatory.

The guidelines provided by MISRA C are not "you should not do that" but "this is
dangerous, you may only do that if it is needed and is safe to do so". Therefore,
the deviation process is an essential part of MISRA C. Violation of a guideline
does not necessarily mean a software error. For example, there is nothing wrong
about converting an integer constant to a pointer when it is necessary to address 
memory mapped registers or other hardware features. However, such conversions
are implementation-defined and have undefined behaviours, so Rule 11.4 suggests
avoiding them everywhere apart from the very specific instances where they are
both required and safe.

For example, here are some safe coding practices in ISO 26262-6:2018
- One entry and one exit point in sub-programs and functions.
- No dynamic objects or variables, or else online test during their creation.
- Initialisation of variables.
- No multiple use of variable names.
- Avoid global variables or else justify their usage.
- Restricted use of pointers.
- No implicit type conversions.
- No hidden data flow or control flow.
- No unconditional jumps.
- No recursions.

## NASA - The power of 10: Rules for developing safety-critical code
1. Avoid complex flow constructs such as `goto` and recursion.
2. All loops must have fixed bounds. This prevents runaway code.
3. Avoid heap memory allocation, e.g. do not use `malloc`.
4. Restrict functions to a single printed page.
5. Use a minimum of two runtime assertions per function.
6. Restrict the scope of data to the smallest possible.
7. Check the return value of all non-void functions, or cast to void to indicate
the return value is useless.
8. Use the pre-processor sparingly, e.g. do not use `stdio.h`, `local.h`, 
`abort()`/`exit()`/`system()` from `stdlib.h`, time handling from `time.h`, etc.
9. Limit pointer use to single dereference, and do not use function pointers.
10. Compile with all possible warnings active; all warnings should then be addressed
before release of the software.
