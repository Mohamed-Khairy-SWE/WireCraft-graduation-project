# Module 2 — Component Library & Placement

---

## 1. Module Objective

The objective of the Component Library & Placement module is to enable users to **select, configure, and place digital circuit components onto the workspace** in a structured and consistent manner.

This module transforms the empty workspace into a **constructible design environment** by introducing standardized components with known interfaces and parameters.

It ensures that:

- Components are discoverable and categorized
- Placement is precise and visually aligned
- Each placed component has a stable identity and configuration
- Visual representation is linked to logical circuit representation

---

## 2. Module Scope Definition

### Included Capabilities

- Component library panel (sidebar)
- Component categories:
  - Logic gates (AND, OR, NOT, XOR, NAND, NOR)
  - Sequential elements (DFF, Latch — visual only at this phase)
  - I/O elements (Input pin, Output pin, Clock source)
- Drag & drop from library to workspace
- Click-to-place alternative
- Component rotation (90° increments)
- Component flipping (horizontal/vertical where applicable)
- Visual alignment to grid
- Unique component ID assignment
- Default parameter assignment

### Explicitly Out of Scope

- Electrical connectivity (wires)
- Signal propagation
- Simulation behavior
- Validation of circuit logic
- Persistence and saving

---

## 3. User Types Involved

- **Designer (Primary User)**: Places and configures components
- **Viewer (Future Phase)**: Will only observe components

At this phase, all users have full edit permissions.

---

## 4. Component Placement Lifecycle Scenarios

### 4.1 Browsing and Selecting Components

**Scenario**

1. User opens the component library
2. User browses categories or searches by name
3. User selects a component type

**Acceptance Criteria**

- Components are grouped logically by category
- Search returns partial and exact matches
- Visual preview is shown before placement

---

### 4.2 Drag-and-Drop Placement

**Scenario**

1. User drags a component from sidebar
2. Ghost preview follows cursor on workspace
3. User releases mouse to place component

**Acceptance Criteria**

- Component snaps to grid if snapping is enabled
- Placement is blocked only by workspace bounds (if any)
- Component becomes immediately selectable

---

### 4.3 Click-to-Place Placement

**Scenario**

1. User selects component from library
2. Cursor switches to placement mode
3. User clicks on workspace to place component

**Acceptance Criteria**

- Multiple placements allowed until user exits placement mode
- ESC cancels placement mode

---

### 4.4 Rotation and Orientation

**Scenario**

1. User selects a placed component
2. User rotates component using shortcut or UI control
3. Ports rotate with the component

**Acceptance Criteria**

- Rotation preserves grid alignment
- Port ordering updates logically
- Visual orientation matches logical orientation

---

### 4.5 Component Parameters (Static at This Phase)

**Scenario**

1. User selects component
2. Inspector panel shows parameters (if any)

Examples:

- Bit-width
- Label / instance name

**Acceptance Criteria**

- Default values are auto-assigned
- Changes update both visual and logical model
- Invalid values are rejected

---

## 5. Data & Identity Rules

- Every component instance must have:
  - Stable unique ID
  - Type reference
  - Position and orientation
  - Parameter map

- Visual objects must map one-to-one with logical instances
- No two components may share the same ID

This identity will be used later for wiring, simulation, and collaboration.

---

## 6. Error & Edge Case Handling

### Covered Scenarios

- Placement outside workspace limits (if bounded)
- Overlapping components (allowed but visually discouraged)
- Invalid parameter values
- Duplicate instance naming conflicts

---

## 7. Integration Points with Other Modules

### Depends On

- Module 1: Workspace & Navigation

### Enables

- Module 3: Ports & Wiring System
- Module 4: Circuit Graph & Validation

Component definitions must already include port metadata even if wires are not yet implemented.

---

## 8. Exit Criteria (Module Completion)

This module is considered complete when:

- Users can browse and search component library
- Components can be placed reliably via drag or click
- Rotation and orientation behave consistently
- Logical component model is created alongside visual objects
- Component data is stable and ready for wiring integration

At this point, the workspace transitions from empty canvas to circuit construction environment.