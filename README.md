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
