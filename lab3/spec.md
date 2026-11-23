# Lab 3 — Interaction (Sequence Diagrams)

## 1. UC and scenarios (from Lab 2)

Selected UC: **UC-3 "Create Deal"** with 5 scenarios (S1–S5). Participants correspond to entities/services of the ER model (Lab 1): `Manager`, `Client`, `Deal`, `Product`, plus `DealController`, `DealService`, `ClientRepository`, `ProductRepository`, `Database`, `AuthService`.

## 2. Sequence diagrams

One diagram per scenario. Each diagram includes at least one combined fragment (alt/opt/loop) and realistic call names. Activation bars are kept continuous across branches where a participant works outside or in multiple branches.

- S1 (happy path): `model/sequence-1-happy.mmd` → `sequence-1-happy.png` — loop (validate products) + opt (discount).
- S2 (client not found): `model/sequence-2-client-not-found.mmd` → `sequence-2-client-not-found.png` — alt (client exists vs not).
- S3 (no products): `model/sequence-3-no-products.mmd` → `sequence-3-no-products.png` — alt (products provided vs not).
- S4 (invalid amount): `model/sequence-4-invalid-amount.mmd` → `sequence-4-invalid-amount.png` — alt (amount > 0 vs <= 0).
- S5 (unauthenticated): `model/sequence-5-unauthenticated.mmd` → `sequence-5-unauthenticated.png` — alt (authenticated vs not).

## 3. Notes on activation bars

For participants active across a conditional fragment (e.g., `DealService` in S2–S4), activation starts before the `alt` and ends after it, not inside a single branch. Participants active only in one branch (e.g., `DealService` in S5 is never reached) are activated within that branch.

## 4. Audit (top-3 discrepancies)

1. **Activation bar broken inside branch**: initial AI draft deactivated `DealService` inside the `else` branch → corrected to deactivate after the fragment.
2. **Participants not matching ER model**: AI used generic "System"/"Server" → replaced with `DealService`, `ClientRepository`, `ProductRepository`, `Database` aligned with Lab 1 entities.
3. **Missing return messages**: AI omitted `-->>` returns → added explicit return messages for each call.

## 5. Consistency

- Participants map to Lab 1 entities: Manager, Client, Deal, Product.
- Steps match Gherkin scenarios of Lab 2 (S1–S5).
- No changes to data model.
