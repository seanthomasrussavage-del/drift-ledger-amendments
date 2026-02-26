# Drift Ledger & Amendments

Append-only governance ledger with an explicit amendment protocol.

This repo focuses on structural credibility: it shows **how changes are governed**, not just how features are built.  
Every entry, mutation, and correction is handled through a deliberate, auditable process.

---

## 1. Purpose

The Drift Ledger exists to:

- Record governance-relevant events as **append-only** entries.
- Make every change **traceable, reviewable, and attributable**.
- Prevent **silent mutation** of rules, configs, or behaviors.
- Provide a clear pattern for **amendments instead of overwrites**.

This is the counterpart to runtime governance gates and test suites:  
it answers the question **“What changed, when, and under whose authority?”**

---

## 2. Core Guarantees

Any implementation or example in this repo should uphold:

1. **No Silent Mutation**  
   - Existing records are never edited in place.  
   - Corrections are expressed as new entries that *amend* prior ones.

2. **Explicit Amendments**  
   - Every amendment references the record it supersedes (by ID, hash, or index).  
   - Rationale, timestamp, and author are always captured.

3. **Auditability**  
   - A reader can reconstruct the full history of a rule or setting.  
   - There is a clear, human-readable trail from initial decision → current state.

4. **Separation of Concerns**  
   - The ledger itself does not “decide policy.”  
   - It only **records** and **structures** decisions made elsewhere.

---

## 3. Conceptual Model

At a high level, the ledger is a list of entries:

- **Entry ID** — unique identifier (may be numeric, UUID, hash, etc.).
- **Type** — e.g., `RULE_CREATED`, `RULE_AMENDED`, `RULE_DEPRECATED`.
- **Payload** — the actual rule, configuration, or governance note.
- **Metadata** — timestamps, author, source system, and tags.
- **Amends** *(optional)* — ID of the prior entry being amended.

A simple rule:

> If behavior or meaning changes, there must be a new entry.

---

## 4. Example Use Cases

Some scenarios this repo is meant to illustrate:

- Updating a routing rule without hiding what it used to be.  
- Correcting a governance definition while preserving the original text.  
- Marking a rule as deprecated and pointing to its replacement.  
- Maintaining a human-readable timeline of important governance changes.

These examples can be implemented as:

- Plain Python data structures,
- A simple file-backed log (JSON, YAML, or newline-delimited),
- Or a thin API that appends entries while enforcing the rules above.

---

## 5. Relationship to Other Repos

This repo pairs with:

- **Governance Gate** — protects live execution.
- **Governance Test Suite** — verifies behavior under governance.
- **Drift Ledger & Amendments (this repo)** — documents how rules *evolve* over time.

Together they show:

> *“What the system is allowed to do, how that is enforced at runtime,  
> and how any change to those rules is recorded and audited.”*

---

## 6. Next Steps (Roadmap)

Planned additions:

- Minimal Python ledger implementation (append-only file or in-memory demo).
- Amendment helpers (e.g., `amend_rule(previous_id, new_payload, reason)`).
- Simple integrity checks (e.g., ensure no entry is edited in place).
- Example integration with a test suite or governance gate.

This repo is intentionally **small but strict**:  
it’s here to demonstrate discipline around change, not to serve as a full database.
