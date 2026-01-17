# Module 4 — Circuit Graph & Validation

---

## 1. Module Objective

The objective of the Circuit Graph & Validation module is to convert the visual wiring model into a **formal logical graph representation** and continuously verify that the circuit satisfies **structural and logical correctness rules** required for simulation and HDL generation.

This module acts as the **semantic gatekeeper** of the system, ensuring that only valid circuits can proceed to simulation and code generation stages.

It ensures that:

- The circuit is representable as a valid directed signal graph
- Signal driving rules are enforced
- Structural errors are detected early
- Errors are mapped back to visual elements

---

## 2. Module Scope Definition

### Included Capabilities

- Construction of circuit graph from nets and components
- Node and edge classification
- Signal direction consistency checks
- Detection of structural design errors
- Incremental validation on every edit
- Error reporting and visual annotation

### Explicitly Out of Scope

- Signal simulation
- Timing analysis
- Performance estimation
- HDL generation

---

## 3. User Types Involved

- **Designer (Primary User)**: Receives validation feedback and corrects errors
- **Viewer (Future Phase)**: Observes error states but cannot modify

---

## 4. Circuit Graph Model

### Graph Construction Rules

- Each component instance is a node
- Each net is a directed edge group
- Ports define edge direction
- Fan-out produces multiple outgoing edges from same source

### Graph Layers

1. **Physical Graph** — components and nets
2. **Logical Graph** — signal dependencies between components

Validation operates primarily on the logical graph.

---

## 5. Validation Categories

### 5.1 Port Direction Errors

**Detected Cases**

- Input driving input
- Output driven by output
- Multiple drivers on same net

**Response**

- Block simulation and HDL export
- Highlight conflicting ports and wires

---

### 5.2 Floating and Undriven Signals

**Detected Cases**

- Input ports with no driver
- Sequential elements without clock

**Response**

- Warning or error depending on component type
- Visual warning indicator

---

### 5.3 Combinational Loop Detection

**Detected Cases**

- Cycles in purely combinational subgraph

**Rules**

- Sequential elements break cycles

**Response**

- Block simulation
- Highlight loop path

---

### 5.4 Incomplete Interface Connections

**Detected Cases**

- Partially connected multi-bit interfaces
- Missing required control signals

**Response**

- Error classification by severity

---

## 6. Incremental Validation Strategy

Validation must be:

- Triggered on every structural edit
- Limited to affected subgraph
- Fast enough for real-time feedback

Full graph validation is allowed only on demand or before simulation.

---

## 7. Error Visualization Rules

Errors must be:

- Associated with concrete visual elements
- Shown directly on canvas
- Listed in error panel with descriptions

Visual cues:

- Port-level highlight
- Wire coloring
- Component-level error badge

---

## 8. Integration Points with Other Modules

### Depends On

- Module 2: Component Library & Placement
- Module 3: Ports & Wiring System

### Enables

- Module 5: Netlist & HDL Generation
- Module 6: Simulation Execution

No circuit may proceed to simulation without passing validation.

---

## 9. Error Severity Levels

- **Blocking Errors**: prevent simulation and export
- **Warnings**: allowed but risky
- **Informational**: design quality suggestions

Severity classification must be consistent and extensible.

---

## 10. Exit Criteria (Module Completion)

This module is considered complete when:

- Logical graph is correctly constructed from visual nets
- All major structural errors are detected
- Errors are mapped to visible circuit elements
- Validation runs incrementally without noticeable lag

At this point, the system can guarantee that designs are structurally executable.

