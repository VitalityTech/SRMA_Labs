# CRM Architecture & Requirements Modeling

Welcome to the documentation and modeling repository for a custom B2B CRM system. This project demonstrates the complete software modeling lifecycle—from initial entity-relationship diagrams (ERD) to advanced component architecture.

## Project Context
This repository is developed and maintained as part of the "Software Requirements Modeling and Analysis" course at Igor Sikorsky Kyiv Polytechnic Institute (KPI). The objective is to design a scalable architecture for a CRM platform managing clients, deals, and managers, ensuring consistency across all UML/Mermaid models.

## Developer
- **Vitaliy Hladchenko**
- **Faculty:** FIOT (Faculty of Informatics and Computer Engineering)
- **Group:** IM-54
- **GitHub Profile:** @VitalityTech / https://github.com/VitalityTech

## Laboratory Works

### Lab 1: Domain & Data Model (ER)
- Specification: [lab1/spec.md](lab1/spec.md)
- ER Model: [lab1/model/er-diagram.mmd](lab1/model/er-diagram.mmd) / [Render (PNG)](lab1/model/er-diagram.png)
- Defense & Audit: [lab1/DEFENSE.md](lab1/DEFENSE.md)
- ADRs:
  - [ADR-0001: Direct Many-to-Many Relationships](lab1/adr/0001-direct-many-to-many-relationships.md)
  - [ADR-0002: Unified UUIDv7 Identifiers](lab1/adr/0002-unified-uuidv7-identifiers.md)
- AI Prompts & Trace:
  - [Prompt 1 (Spec Review)](lab1/ai/prompt-1.md)
  - [Prompt 2 (Initial Generation)](lab1/ai/prompt-2.md)
  - [Prompt 3 (Model Audit)](lab1/ai/prompt-3.md)

### Lab 2: Requirements and Use Cases (UC + Gherkin + EARS + NFR)
- Specification: [lab2/spec.md](lab2/spec.md)
- Use Case Model: [lab2/model/use-case-diagram.mmd](lab2/model/use-case-diagram.mmd) / [Render (PNG)](lab2/model/use-case-diagram.png)
- Defense & Audit: [lab2/DEFENSE.md](lab2/DEFENSE.md)
- ADRs:
  - [ADR-0001: Single Complex Use Case Selection](lab2/adr/0001-selected-use-case.md)
  - [ADR-0002: Measurable NFR Thresholds](lab2/adr/0002-nfr-measurable.md)
- AI Prompts & Trace:
  - [Prompt 1 (Actor & UC Review)](lab2/ai/prompt-1.md)
  - [Prompt 2 (Diagram Generation)](lab2/ai/prompt-2.md)
  - [Prompt 3 (Requirements Audit)](lab2/ai/prompt-3.md)

### Lab 3: Interaction (Sequence Diagrams)
- Specification: [lab3/spec.md](lab3/spec.md)
- Sequence Models:
  - S1 (Happy path): [lab3/model/sequence-1-happy.mmd](lab3/model/sequence-1-happy.mmd) / [Render (PNG)](lab3/model/sequence-1-happy.png)
  - S2 (Client not found): [lab3/model/sequence-2-client-not-found.mmd](lab3/model/sequence-2-client-not-found.mmd) / [Render (PNG)](lab3/model/sequence-2-client-not-found.png)
  - S3 (No products): [lab3/model/sequence-3-no-products.mmd](lab3/model/sequence-3-no-products.mmd) / [Render (PNG)](lab3/model/sequence-3-no-products.png)
  - S4 (Invalid amount): [lab3/model/sequence-4-invalid-amount.mmd](lab3/model/sequence-4-invalid-amount.mmd) / [Render (PNG)](lab3/model/sequence-4-invalid-amount.png)
  - S5 (Unauthenticated): [lab3/model/sequence-5-unauthenticated.mmd](lab3/model/sequence-5-unauthenticated.mmd) / [Render (PNG)](lab3/model/sequence-5-unauthenticated.png)
- Defense & Audit: [lab3/DEFENSE.md](lab3/DEFENSE.md)
- ADRs:
  - [ADR-0001: One Diagram Per Scenario](lab3/adr/0001-one-diagram-per-scenario.md)
  - [ADR-0002: Participants Aligned with ER Model](lab3/adr/0002-participants-aligned.md)
- AI Prompts & Trace:
  - [Prompt 1 (Scenario S1)](lab3/ai/prompt-1.md)
  - [Prompt 2 (Scenarios S2–S5)](lab3/ai/prompt-2.md)
  - [Prompt 3 (Interaction Audit)](lab3/ai/prompt-3.md)

### Lab 4: Process and Behavior (Activity Model)
- Specification: [lab4/spec.md](lab4/spec.md)
- Activity Model: [lab4/model/activity-diagram.mmd](lab4/model/activity-diagram.mmd) / [Render (PNG)](lab4/model/activity-diagram.png) / [Render (SVG)](lab4/model/activity-diagram.svg)
- Defense & Audit: [lab4/DEFENSE.md](lab4/DEFENSE.md)
- ADRs:
  - [ADR-0001: Activity Diagram Notation Choice](lab4/adr/0001-activity-diagram-notation.md)
  - [ADR-0002: Async Message and Timeout Handling](lab4/adr/0002-async-message-handling.md)
- AI Prompts & Trace:
  - [Prompt 1 (Process Steps Review)](lab4/ai/prompt-1.md)
  - [Prompt 2 (Diagram Generation)](lab4/ai/prompt-2.md)
  - [Prompt 3 (Behavior Audit)](lab4/ai/prompt-3.md)
