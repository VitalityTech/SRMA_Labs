# Entities and Attributes

- **Manager**:
    - `manager_id`: UUIDv7 (PK)
    - `email`: string (UK)
    - `full_name`: string
    - `created_at`: timestamp

- **Client**:
    - `client_id`: UUIDv7 (PK)
    - `company_name`: string
    - `contact_email`: string (UK)
    - `created_at`: timestamp

- **Deal**:
    - `deal_id`: UUIDv7 (PK)
    - `client_id`: UUIDv7 (FK)
    - `manager_id`: UUIDv7 (FK)
    - `title`: string
    - `amount`: float
    - `status`: string
    - `created_at`: timestamp

- **Product**:
    - `product_id`: UUIDv7 (PK)
    - `name`: string (UK)
    - `price`: float
    - `description`: string (optional)

# Relations
1. **`Manager` -manages- `Deal` ( 1 : 0..N ):**
    * One manager can manage zero-to-many deals ( 1 : 0..M )
    * One deal must have one and only manager ( 1 : 1 )
2. **`Client` -has- `Deal` ( 1 : 0..N ):**
    * One client can have zero-to-many deals ( 1 : 0..M )
    * One deal must have one and only client ( 1 : 1 )
3. **`Deal` -includes- `Product` ( 0..M : 1..N ):**
    * One deal must include at least one product ( 1 : 1..M )
    * One product can be included in zero-to-many deals ( 1 : 0..M )

# Acceptance criteria
1. **Artifacts (CRITICAL):**
   - Mermaid model entity relationships diagram, saved in file `model/er-diagram.mmd`.
   - Rendered visual diagram file saved in `model/er-diagram.png`.
2. **Conceptual Model Constraints**:
   - Model business entities and domain relationships only, not physical database tables.
   - STRICTLY no associative entities for many-to-many relationships without own attributes. Many-to-many must be modeled as a direct relation between entities.
   - Associative entities are permitted only if the relationship itself carries domain-specific attributes.
   - Associative entities are permitted only if the relationship itself carries domain-specific attributes.
3. **Normalization (3NF):**
   - No non-key attribute depends on another non-key attribute.
   - All non-key attributes must depend directly on the primary key.
4. **Unification of identifiers:**
   - All PK and FK is `UUIDv7`.
   - Entity and attributes names should be exactly the same to the `Entities and Attributes` paragraph (snake_case for attributes, PascalCase for entities).