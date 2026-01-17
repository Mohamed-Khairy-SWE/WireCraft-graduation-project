# Module 5 — Netlist & HDL Generation

---

## 1. Module Objective

The objective of the Netlist & HDL Generation module is to transform the validated circuit graph into a **formal, deterministic hardware description** suitable for simulation and downstream tooling.

This module bridges the gap between visual design and executable hardware models by producing:

- A normalized netlist representation
- A structured intermediate representation (IR)
- Synthesizable Verilog (or other HDL in future phases)

It ensures that:

- Signal connectivity is unambiguous
- Component behavior is mapped to HDL primitives
- Generated code is stable, readable, and reproducible

---

## 2. Module Scope Definition

### Included Capabilities

- Netlist extraction from validated circuit graph
- Net normalization and merging
- Deterministic signal naming
- Instance naming and scoping
- HDL Intermediate Representation (IR) generation
- Verilog module generation
- Parameter expansion and width propagation

### Explicitly Out of Scope

- Simulation execution
- Timing annotation
- Testbench generation (later phase)
- HDL optimization
- Synthesis constraints

---

## 3. User Types Involved

- **Designer (Primary User)**: Initiates code generation and views output
- **Viewer (Future Phase)**: Can inspect generated HDL

---

## 4. Netlist Normalization Process

### 4.1 Net Consolidation

**Objective**

Ensure that all wire segments and fan-out branches referencing the same driver are merged into a single logical net.

**Rules**

- Each net has exactly one driver
- All driven ports reference the same net ID

---

### 4.2 Signal Width Resolution

**Objective**

Resolve bus widths across connected ports.

**Rules**

- Width must match across all connected ports
- Scalar-to-bus connections are invalid unless explicitly supported

**Response**

- Width mismatch is a blocking error

---

### 4.3 Port Ordering Resolution

**Objective**

Map visual port positions to logical port order required by HDL templates.

**Rules**

- Logical port order is defined by component type
- Visual orientation must not affect HDL port mapping

---

## 5. Instance and Signal Naming Rules

### Instance Naming

- Each component instance receives a unique HDL-safe name
- Deterministic across regenerations when topology is unchanged

Example:

- AND_1, DFF_3, INPUT_0

---

### Signal Naming

- Nets are assigned auto-generated names
- Names must be stable for unchanged topology
- Avoid collisions with keywords

Example:

- n0, n1, clk, data_bus_2

---

## 6. HDL Intermediate Representation (IR)

The IR acts as a structured hardware model independent of any specific HDL syntax.

### IR Contains

- Module definition
- Port declarations
- Net declarations
- Instance list
- Parameter bindings

### Purpose

- Enable multi-language backends in future
- Simplify verification and debugging
- Decouple frontend graph from codegen backend

---

## 7. Verilog Code Generation

### Output Structure

- Top module declaration
- Port list
- Wire declarations
- Component instantiations

### Component Mapping

Each component type maps to:

- Verilog primitive
- Or predefined module template

Example mappings:

- AND gate → assign or primitive gate
- DFF → always_ff block or module

---

## 8. Consistency and Determinism Guarantees

Generated HDL must be:

- Deterministic for identical circuit graphs
- Insensitive to wire routing changes
- Independent of visual placement

Only logical topology and parameters affect output.

---

## 9. Integration Points with Other Modules

### Depends On

- Module 4: Circuit Graph & Validation

### Enables

- Module 6: Simulation Execution
- Module 7: Waveform Visualization
- External tool export

HDL generation is the sole input path for simulation engines.

---

## 10. Error & Edge Case Handling

### Covered Scenarios

- Missing drivers
- Width mismatches
- Unsupported component parameters
- Illegal HDL identifiers

Errors must be surfaced before simulation is allowed.

---

## 11. Exit Criteria (Module Completion)

This module is considered complete when:

- Valid circuits can be fully translated to HDL
- Generated code is syntactically correct and synthesizable
- IR structure supports future language backends
- Output is stable and reproducible across regenerations

At this point, designs are formally executable hardware descriptions.