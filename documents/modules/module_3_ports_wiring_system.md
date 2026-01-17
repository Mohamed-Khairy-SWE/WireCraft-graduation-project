# Module 3 — Ports & Wiring System

---

## 1. Module Objective

The objective of the Ports & Wiring System module is to enable users to **create valid signal connections between components** by linking output ports to compatible input ports, forming the physical topology of the digital circuit.

This module transforms isolated components into an interconnected **signal network (netlist graph)** that represents real logical relationships required for simulation and code generation.

It ensures that:

- Connections are created only between compatible ports
- Wires visually and logically represent signal flow
- Connection integrity is maintained during editing
- Each wire corresponds to a unique logical net or net segment

---

## 2. Module Scope Definition

### Included Capabilities

- Port rendering on components
- Port types and directions:
  - Input
  - Output
  - Bidirectional (future extension)
- Interactive wire drawing
- Port snapping and highlight feedback
- Auto-routing (orthogonal or straight)
- Wire segments and junction handling
- Reconnecting existing wires
- Wire deletion
- Visual indication of signal direction

### Explicitly Out of Scope

- Signal values or propagation
- Timing behavior
- Electrical constraints
- Logic validation beyond direction compatibility
- Simulation

---

## 3. User Types Involved

- **Designer (Primary User)**: Creates and edits connections
- **Viewer (Future Phase)**: Observes wiring layout

All users have full edit permissions at this phase.

---

## 4. Wiring Lifecycle Scenarios

### 4.1 Creating a New Connection

**Scenario**

1. User clicks on an output port
2. Wire preview follows cursor
3. Compatible input ports are highlighted
4. User releases on valid target port
5. Wire is committed to the circuit

**Acceptance Criteria**

- Connection only allowed from output → input
- Invalid targets are visually rejected
- Wire snaps exactly to port center

---

### 4.2 Multi-Drop Connections (Fan-out)

**Scenario**

1. User connects one output to multiple inputs

**Rules**

- One output may drive multiple inputs
- Multiple outputs may NOT drive same input

**Acceptance Criteria**

- Shared net is created internally
- All wire segments reference same logical net

---

### 4.3 Wire Routing and Adjustment

**Scenario**

1. System auto-routes wire using default style
2. User drags wire segment to adjust path

**Acceptance Criteria**

- Wire remains connected to original ports
- Junction points remain visually consistent

---

### 4.4 Reconnecting Wires

**Scenario**

1. User drags wire endpoint away from port
2. Wire enters reconnect mode
3. User attaches to different compatible port

**Acceptance Criteria**

- Old connection is removed
- New connection is validated
- Logical net is updated accordingly

---

### 4.5 Wire Deletion

**Scenario**

1. User selects wire
2. User deletes wire

**Acceptance Criteria**

- Net is removed or split if required
- No dangling references remain

---

## 5. Logical Net Model

Each wire belongs to a **Net** structure:

- Net ID
- Driving port (single)
- Driven ports (multiple)
- Wire segments (visual)

Rules:

- Each net must have exactly one driver
- Nets may exist temporarily without driver during editing

This net model is required for later HDL generation.

---

## 6. Visual vs Logical Consistency Rules

- Visual wire paths are independent of logical connectivity
- Editing visual routes must not affect net membership
- Logical changes must propagate to all visual segments

The system must strictly separate rendering concerns from netlist logic.

---

## 7. Error & Edge Case Handling

### Covered Scenarios

- Connecting input to input
- Connecting output to output
- Attempting to connect to occupied input
- Deleting component with attached wires
- Moving components with connected wires

**Rules**

- All connected wires must follow component movement
- Deleting a component deletes all attached nets

---

## 8. Integration Points with Other Modules

### Depends On

- Module 1: Workspace & Navigation
- Module 2: Component Library & Placement

### Enables

- Module 4: Circuit Graph & Validation
- Module 5: Netlist & HDL Generation

Ports and nets form the structural backbone for all later logic processing.

---

## 9. Exit Criteria (Module Completion)

This module is considered complete when:

- Users can reliably connect compatible ports
- Fan-out connections are supported
- Wires visually track component movement
- Logical net model remains consistent under all edits
- Invalid connections are blocked and clearly communicated

At this point, the design is structurally a real circuit, not just a diagram.