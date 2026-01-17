# Module 6 — Simulation Execution

---

## 1. Module Objective

The objective of the Simulation Execution module is to execute the generated HDL model in a controlled environment and produce **time-based signal behavior results** that reflect the functional operation of the designed circuit.

This module converts static hardware descriptions into **dynamic behavioral data** usable for debugging, verification, and learning.

It ensures that:

- Simulations are reproducible and isolated
- Input stimuli and clocks are applied deterministically
- Execution errors are captured and reported clearly
- Results are available for visualization and analysis

---

## 2. Module Scope Definition

### Included Capabilities

- Simulation job creation
- HDL compilation and elaboration
- Controlled execution (run / step / stop)
- Clock source management
- Manual and scripted input stimulus
- Simulation time management
- Error capture and reporting
- Result data generation (signal traces)

### Explicitly Out of Scope

- Waveform visualization (handled by Module 7)
- Formal verification
- Performance analysis
- Hardware synthesis
- Long-running stress simulations

---

## 3. User Types Involved

- **Designer (Primary User)**: Runs and controls simulations
- **Viewer (Future Phase)**: Observes simulation output only

---

## 4. Simulation Lifecycle

### 4.1 Simulation Setup

**Scenario**

1. User clicks "Run Simulation"
2. System verifies no blocking validation errors
3. HDL is compiled by simulator backend
4. Simulation environment is initialized

**Acceptance Criteria**

- Compilation errors are reported before execution
- No simulation starts with invalid HDL

---

### 4.2 Clock and Input Stimulus Configuration

**Scenario**

1. User defines clock frequency or period
2. User toggles input pins manually or via script

**Rules**

- Multiple clock sources may exist
- Inputs may change only at discrete simulation times

---

### 4.3 Execution Control

**Scenario**

- User runs continuous simulation
- User pauses execution
- User steps forward by fixed time quantum

**Acceptance Criteria**

- Simulation state is preserved between steps
- Inputs may be modified only while paused

---

### 4.4 Simulation Termination

**Scenario**

1. User stops simulation
2. Resources are released

**Acceptance Criteria**

- No residual processes remain
- New simulation can be started cleanly

---

## 5. Execution Environment Requirements

### Isolation

Each simulation must run in:

- Separate process or sandbox
- With strict resource limits

### Determinism

- Same design + same inputs → same outputs
- No dependency on execution timing or load

---

## 6. Error Handling and Reporting

### Error Types

- HDL syntax errors
- Elaboration errors
- Runtime simulation faults
- Timeout or resource exhaustion

### Error Reporting Rules

- Errors must reference HDL line numbers
- Errors must map back to visual components when possible
- Execution must halt on fatal errors

---

## 7. Result Data Generation

### Output Artifacts

- Time-ordered signal values
- Event timestamps
- Optional VCD or equivalent trace format

### Requirements

- All user-visible signals must be recorded
- Internal signals may be optionally recorded

Result data is passed directly to Module 7 for visualization.

---

## 8. Integration Points with Other Modules

### Depends On

- Module 5: Netlist & HDL Generation

### Enables

- Module 7: Waveform Visualization
- Module 10+: AI Debugging and Analysis

Simulation is the sole source of behavioral truth for the system.

---

## 9. Security and Resource Control

Because user designs generate executable code:

- Execution must be sandboxed
- CPU and memory limits must be enforced
- File system access must be restricted

This is mandatory for cloud deployment.

---

## 10. Exit Criteria (Module Completion)

This module is considered complete when:

- Valid designs can be simulated reliably
- Users can control execution time and inputs
- Errors are captured and displayed clearly
- Signal trace data is produced consistently

At this point, the platform supports full functional verification of circuits.