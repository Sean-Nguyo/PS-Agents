# Design & Development Plan: Trailer Routing KBA

This plan outlines the essential development phases for converting a static Uniform Cost Search (UCS) pathfinder into a dynamic *Knowledge-Based Agent (KBA)* Python Notebook that guides a self-driving trailer from *Nairobi* to *Kisumu*.

## Phase 1: Task & Scope Definition

The agent operates strictly as a *High-Level Routing Brain* rather than a low-level vehicle controller. Its sole responsibility is computing the lowest-distance valid highway route between *Nairobi* and *Kisumu*, delegating physical actuation (steering, braking, and transmission) to downstream control systems.

## Phase 2: Knowledge Assembly & External Data

Static spatial topology is established using an abstracted 28-node directed graph and unfolded search tree, yielding a baseline optimal route of $357.0\text{ km}$ via *Nakuru* and *Kericho*. Live operational context is integrated via the *Google Maps Routes API* (`TRAFFIC_AWARE` distances) and web scrapers targeting *KeNHA* public notices and *Capital FM* traffic disruption reports.

## Phase 3: Vocabulary & Domain Encoding

Domain knowledge is formalized in Python using normalized town constants (`Nairobi` to `Kisumu`), status labels (`Blocked`, `Caution`, `Clear`), and distance metrics in kilometers. Declarative structures bind these entities: `highway_graph` stores base step costs, `road_conditions` tracks active edge overrides, and `trailer_rules` dictates pruning or caution policies.

## Phase 4: Dynamic Fact Ingestion

Dedicated update routines allow the Knowledge Base (KB) to adapt at runtime without modifying search logic. Automated parsers normalize town names and assert scraped disruption notices into `road_conditions` with distance penalties, while interactive notebook functions let operators manually insert, update, or clear road status facts.

## Phase 5: Inference & Query Execution

The `ucs_with_kb` inference engine executes *Uniform Cost Search* while consulting `road_conditions` at every edge expansion. Blocked segments are pruned to force automatic rerouting, whereas cautionary segments incorporate distance penalties and attach safety advisories to the final navigation output.

## Phase 6: Verification & Future Refinements

System reliability is validated through simulated road closures (such as blocking *Kericho* $\rightarrow$ *Ahero*) and unreachable reverse-route queries. Key future refinements include modeling bidirectional return edges, incorporating trailer payload and escarpment gradient weights, and adding timestamped conflict resolution for overlapping updates.

## 5. Group Work Evidence
### Meeting Minutes
- **Date**: 17/11/2026
- **Platform**: Google Meet
- **Members Present**: Albert Miricho (189990), Sean Ndung'u (191602), Sydney Aisha (190497)
- **Agenda**:
  1. Opening & Context Review (recap of the current static Uniform Cost Search implementation and the goal of transitioning to a dynamic, knowledge-based agent.)
  2. Knowledge base definition and algorithm modification.
  3. External data ingestion & integration strategy via web scraping and Google Maps API.
  4. Task assignment and timeline setting.
  5. Repository fork verification and Markdown documentation compilation.