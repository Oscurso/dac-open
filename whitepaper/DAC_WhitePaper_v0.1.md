# Deterministic Artificial Cognition (DAC)

**A Unified White Paper**  
**Version 0.1 • October 27, 2025**  
**Authors:** Oscurso Labs  
**Reference Implementation:** Oscurso DAC Engine  
**Contact:** github.com/Oscurso • x.com/OscursoLabs  
**License:** CC BY 4.0 (white paper) • MIT (Oscurso DAC Engine)

---

## Abstract

Deterministic Artificial Cognition (DAC) is a framework for explainable, reproducible, and verifiable machine cognition. Unlike stochastic AI systems that produce non-deterministic outputs, DAC models cognition as deterministic transitions over explicit structures and rules. We formalize the DAC model, present a layered system architecture, define a deterministic lineage protocol using cryptographic hash chaining, and describe optional hybrid integrations, where probabilistic models can propose inputs or rules that DAC subsequently verifies.. We contribute: (1) a formal definition of deterministic cognition with constraints; (2) a governance and compliance model; (3) an evaluation framework and reproducibility checklist; (4) an open-source reference implementation (Oscurso). We argue DAC is essential where auditability, accountability, and repeatability are mandatory.

**Keywords:** Determinism, Explainable AI, Reproducibility, Lineage, Hash Chain, Governance, Hybrid AI, Auditability, Provenance, Oscurso.

---

## Executive Summary

**Core promise:** *Probability imagines; determinism ensures.*  
DAC does **not** replace stochastic AI—it **constrains**, **validates**, and **operationalizes** it where consistent outcomes and full audit trails are required (e.g., regulated industries, safety-critical systems). DAC provides:
- **Determinism:** Identical inputs + rules ⇒ identical states.
- **Explainability:** Every transition emits provenance and justifications.
- **Reproducibility:** Full cognitive lineage can be reconstructed and verified.

---

## Table of Contents

1. Preface — Context of Emergence  
2. Introduction — From Probability to Structure  
3. Formal Model of Deterministic Cognition  
4. Deterministic Cognition Theorem (Sketch)  
5. Reasoning Algorithms & Hash-Chain Lineage  
6. The DAC Cognitive Stack (L0–L6)  
7. System Architecture (Oscurso Reference)  
8. Rule Acquisition Pipeline  
9. Temporal Isolation & Determinism in the Wild  
10. Failure Modes & Recovery  
11. Hybrid Architecture with Probabilistic AI  
12. Evaluation Framework & Benchmarks  
13. Security, Compliance & Governance (DGM)  
14. Ethical & Philosophical Considerations  
15. Use Cases & Case Studies  
16. Roadmap & Future Work  
17. API Sketch (Oscurso DAC)  
18. Reproducibility Checklist  
19. Glossary  
20. References  
21. Appendix A — Mathematical Details  
22. Appendix B — Worked Examples  

---

## 1. Preface — Context of Emergence

The rapid adoption of large language models (LLMs) surfaced tension between capability and control. Non-determinism complicates compliance (e.g., EU AI Act), safety, and scientific reproducibility. DAC emerges as a complementary paradigm that retains creativity via probabilistic generation while **ensuring** verifiable cognition via deterministic validation and execution.

---

## 2. Introduction — From Probability to Structure

**Probabilistic AI** estimates the *next token*; **DAC** establishes the *next state*.  

### 2.1 Problems with Non-Determinism

- Inconsistent outputs → limited auditability.
- Opaque internal states → weak causal attribution.
- Correlation-based confidence → brittle long-horizon reasoning.

### 2.2 DAC — The Structural Alternative

- **Determinism:** Inputs + rules ⇒ identical states.
- **Explainability:** Emitted provenance at each step.
- **Reproducibility:** State lineage reconstructible and verifiable.

---

## 3. Formal Model of Deterministic Cognition

Let **Structure** \(S=(E,R,C)\) with entities \(E\), relations \(R\), constraints \(C\).  
Let **Ruleset** \(\mathcal{R}=\{r_1,\dots,r_n\}\) where each rule \(r_i: \sigma \mapsto \sigma'\) iff \(C(\sigma')=\text{true}\).  
Let **State** \(\sigma\in\Sigma\) be a configuration satisfying \(C\).  
Define the **Transition Function** \(T: \Sigma\times\mathcal{R}\to\Sigma\) and **Cognition** as the sequence \(\mathcal{C} = (\sigma_0,\dots,\sigma_n)\) with \(\sigma_{i+1}=T(\sigma_i,r_i)\).  
Let **Provenance** \(P\) capture metadata over \(\sigma_0\dots\sigma_n,\mathcal{R}\).  
Objective: produce observable \(O=f(\sigma_n)\) with reproducibility guarantee \(H(\sigma_n)=H'(\sigma_n)\).

---

## 4. Deterministic Cognition Theorem (Sketch)

**Theorem.** Given fixed \(S\), fixed \(\mathcal{R}\), and a frozen input snapshot, all DAC trajectories are unique and identical for identical inputs: for any runs A and B, \(\sigma^{A}_{n}=\sigma^{B}_{n}\).

**Sketch.** By construction, \(T\) is a function; thus for a given \((\sigma_i,r_i)\) there exists a unique \(\sigma_{i+1}\). Compositionality of \(T\) implies the trajectory is unique. Hash-chain lineage \(h_i = \operatorname{SHA256}(\sigma_i\Vert r_i\Vert \sigma_{i+1}\Vert h_{i-1})\) ensures tamper-evident verification.

---

## 5. Reasoning Algorithms & Hash-Chain Lineage

**Algorithm DAC-Reason(\(\sigma_0,\mathcal{R}\))**

1. \(L\leftarrow[~]\), \(\sigma\leftarrow\sigma_0\), \(h_{\text{prev}}\leftarrow \text{GENESIS\_HASH}\)
2. For each \(r\in\mathcal{R}\):
   - a. \(\sigma'\leftarrow r(\sigma)\)
   - b. assert \(C(\sigma')\)
   - c. \(h\leftarrow\operatorname{SHA256}(\sigma,r,\sigma', h_{\text{prev}})\)
   - d. append \((h, \sigma, r, \sigma')\) to \(L\)
   - e. \(\sigma\leftarrow\sigma'\), \(h_{\text{prev}}\leftarrow h\)
3. return \((\sigma, L)\)

**Lineage:** \(L=\{(h_1, \sigma_0, r_1, \sigma_1), (h_2, \sigma_1, r_2, \sigma_2), \dots, (h_n, \sigma_{n-1}, r_n, \sigma_n)\}\) forms the deterministic cognitive fingerprint, where each \(h_i\) cryptographically commits to the reasoning step and chains to \(h_{i-1}\).

**Hash extraction:** The hash chain \(\{h_0, h_1, \dots, h_n\}\) can be extracted from \(L\) for compact verification.

**Figure (concept):**
```
σ₀ --r₁--> σ₁ --r₂--> σ₂ -- … --rₙ--> σₙ
|          |          |              |
h₀         h₁         h₂            hₙ
└──────────┴──────────┴──────────────┘
   (each hᵢ = SHA256(σᵢ, rᵢ, σᵢ₊₁, hᵢ₋₁))
```

---

## 6. The DAC Cognitive Stack (L0–L6)

| Layer | Purpose | Key Artifacts |
|---|---|---|
| **L0 — Schema** | Entity graphs, invariants, constraints | Ontology, schemas, constraint specs |
| **L1 — Deterministic Engine** | Rule application and state evolution | Transition executor, validator |
| **L2 — Temporal Isolation** | Frozen external context | Input snapshots, cached APIs |
| **L3 — Lineage Store** | Tamper-evident audit trail | Hash-chain, state deltas, proofs |
| **L4 — Cognitive Interface** | Introspection & visualization | APIs, dashboards, explanations |
| **L5 — Human-in-the-Loop** | Policy override & adjudication | Review queues, approvals |
| **L6 — Distributed Nodes** | Federation & consensus | Deterministic quorum, signed releases |

---

## 7. System Architecture (Oscurso Reference)

**Textual Diagram:**
```
Client ──► [L4: Cognitive Interface]
          │         ▲
          │         │ explanations, proofs
          ▼         │
       [L3: Lineage Store] ──► Hash Chain / Proofs
          ▲
          │ deltas
       [L2: Temporal Isolation]
          ▲
          │ frozen inputs
       [L1: Deterministic Engine]
          ▲
          │ model
       [L0: Schema]
```
**Features:** REST APIs, visual lineage explorer, plugin system for rule sources, deterministic replay.

---

## 8. Rule Acquisition Pipeline

- **Expert Definition:** Highest precision for critical paths.  
- **Probabilistic Extraction:** LLMs propose candidate rules → DAC normalizes & verifies.  
- **Graph Inference:** Mine structural patterns and constraints from KGs.  
**Lifecycle:** draft → normalize → validate → sign → release (versioned).

---

## 9. Temporal Isolation & Determinism in the Wild

Freeze external inputs to maintain determinism:
```json
{
  "sensor_data": "fixed_timestamp",
  "api_responses": "cached_version",
  "environment_state": "hash(frozen)"
}
```

**This 'frozen snapshot' is the artifact created by L2 (Temporal Isolation). It serves as the definitive `context_snapshot` for the L1 Deterministic Engine, ensuring that all non-deterministic inputs are converted into fixed facts *before* cognition begins.**

Replays on identical snapshots produce identical terminal states \(\sigma_n\).

---

## 10. Failure Modes & Recovery

- **Contradictory Rules:** Constraint violation → isolate offending ruleset, quarantine, request adjudication.  
- **Incomplete Rules:** Fall back to probabilistic proposal mode; proposed rules must pass deterministic validation.  
- **Lineage Corruption:** Hash mismatch → rollback to last verified checkpoint; raise integrity event.

---

## 11. Hybrid Architecture with Probabilistic AI

**Flow:** Probabilistic generation → DAC verification → Deterministic execution → Transparent output.  
Benefits: flexibility + reliability, rapid prototyping, graceful degradation when deterministic paths are missing.

---

## 12. Evaluation Framework & Benchmarks

**Core Metrics**
- **Reproducibility %:** share of runs where \(H(\sigma_n)\) matches across independent environments.  
- **Verification Latency (ms):** rule validation + hash-chain overhead.  
- **Cognitive Depth (steps):** average transitions per decision.  
- **Rule Coverage (%):** rules exercised over a corpus of scenarios.  
- **Constraint Violation Rate:** per 1,000 transitions.  

**Benchmark Protocol**
1. Publish \(S\), \(\mathcal{R}\), input snapshots.  
2. Execute N independent runs on M environments.  
3. Compare terminal states and lineage hashes.  
4. Report metrics with confidence intervals.

**Example Table (illustrative)**
| Metric | Value |
|---|---|
| Reproducibility | 100.0% (500/500 runs) |
| Verification Latency | 3.2 ms p50 / 7.9 ms p95 |
| Cognitive Depth | 42 steps avg |
| Rule Coverage | 87% |
| Constraint Violations | 0.6/1k transitions |

---

## 13. Security, Compliance & Governance (DGM)

### 13.1 Cryptographic Verification

Every transition emits a SHA-256 hash; the lineage forms an immutable audit trail.

### 13.2 Regulatory Alignment

- **Explainability:** full trace (e.g., EU AI Act Article 13/52).  
- **Auditability:** signed, versioned releases (SOX §404).  
- **Electronic Records:** tamper-evidence (FDA 21 CFR Part 11).

### 13.3 Deterministic Governance Model (DGM)

- **Versioning:** semantic versions for \(S\) and \(\mathcal{R}\).  
- **Change Control:** proposals → review → deterministic tests → signed release.  
- **Access Control:** role-based, least privilege.  
- **Consensus (L6):** optional deterministic quorum for multi-party rule updates.  
- **Attestations:** cryptographic signatures attached to lineage and releases.

---

## 14. Ethical & Philosophical Considerations

Determinism in cognition maintains human agency and accountability. DAC increases transparency without eliminating creativity: probabilistic components still explore; DAC ensures that deployed outcomes are verifiable and reproducible.

---

## 15. Use Cases & Case Studies

- **Financial Compliance:** Transaction analysis via LLM; DAC verifies against regulatory constraints; produces regulator-ready audit trails.  
- **Medical Diagnostics:** Symptom interpretation via LLM; DAC validates against knowledge graphs and constraints; traceable diagnoses.  
- **Smart Contracts:** Candidate code or states proposed; DAC verifies deterministic state transitions; security via structural guarantees.  
- **Scientific Reproducibility:** Experiment workflows recorded; DAC stores lineage; publications include hash-chains.

---

## 16. Roadmap & Future Work

- **Phase I — Foundation (Q1 2026):** Formal spec; Oscurso v1.0 release.
- **Phase II — Integration (Q2–Q3 2026):** SDKs for LLM integration; benchmark suite.
- **Phase III — Propagation (Q4 2026 – Q1 2027):** Distributed DAC nodes; cross-domain transfer.
- **Phase IV — Continuum (2027+):** Self-organizing DAC networks; end-to-end formal verification.

---

## 17. API Sketch (Oscurso DAC)

**POST /api/v1/cognition/execute**
```json
{
  "initial_state": { /* ... */ },
  "ruleset_id": "uuid",
  "context_snapshot": { /* frozen inputs */ }
}
```
**GET /api/v1/lineage/{execution_id}** → returns full hash-chain and state deltas.  
**POST /api/v1/verify**
```json
{
  "lineage": [ /* ... */ ],
  "claimed_hash": "..."
}
```

**Example curl**
```bash
curl -X POST https://api.oscurso.dev/api/v1/cognition/execute \
  -H "Content-Type: application/json" \
  -d '{"initial_state":{},"ruleset_id":"b3f...","context_snapshot":{}}'
```

---

## 18. Reproducibility Checklist

- [ ] Define complete Structure \(S=(E,R,C)\)
- [ ] Specify deterministic Ruleset \(\mathcal{R}\)
- [ ] Implement constraint validation (assert \(C(\sigma')=\text{true}\))
- [ ] Generate **cryptographic** hash-chain (ensure \(h_i\) chains \(h_{i-1}\))
- [ ] Freeze external inputs (L2 Temporal Isolation)
- [ ] Store full lineage **tuples** \((h, \sigma, r, \sigma')\)
- [ ] Provide verification API (for lineage replay)
- [ ] Document failure modes & recovery
- [ ] Test cross-environment reproduction
- [ ] **Implement governance lifecycle (validate → sign → release)**
- [ ] Publish **signed** ruleset versions and checksums

---

## 19. Glossary

- **Cognition State (\(\sigma\))**: a complete configuration of the structural model at a given point.  
- **Constraint (C):** invariants that must hold for valid states.  
- **Lineage (L):** hash-chained sequence of transitions.  
- **Provenance (P):** origin, transformations, and justifications metadata.  
- **Ruleset (\(\mathcal{R}\))**: deterministic transformation functions.  
- **Structure (S):** entities, relations, and constraints.  
- **Temporal Isolation:** freezing external state for reproducibility.

---

## 20. References

- Oscurso DAC Engine (2025).  
- Russell & Norvig, *Artificial Intelligence: A Modern Approach*, 4e (2020).  
- Lamport (1998), *The Part-Time Parliament*.  
- Goodfellow, Bengio, Courville, *Deep Learning* (2016).  
- EU AI Act (2024): Regulation (EU) 2024/1689 on Artificial Intelligence.

---

## 21. Appendix A — Mathematical Details

**A.1 State Space**  
\(\Sigma=\{\sigma\mid \forall C\in\mathcal{C},~C(\sigma)=\text{true}\}\).  

**A.2 Transition Properties**  
Determinism: \(\forall\sigma\in\Sigma,\forall r\in\mathcal{R}: T(\sigma,r)=\sigma'\) unique.  
Constraint-preserving: \(\sigma'\in\Sigma\).  
Compositional: \(T(T(\sigma,r_1),r_2)=T(\sigma,[r_1,r_2])\).

**A.3 Hash-Chain Verification**  
\(h_i=\operatorname{SHA256}(\sigma_i\Vert r_i\Vert \sigma_{i+1}\Vert h_{i-1})\).  
Verification: recompute \(h_i\) and compare to stored lineage.

---

## 22. Appendix B — Worked Examples

### B.1 Banking Transfer (Toy)
Initial: `balance=100`, constraints: `balance>=0`.  
Rule `transfer(25)` with `KYC=true`.  
Result: `balance=75`.  
Lineage: `h0 = SHA256(100, transfer25, 75)`.

### B.2 Medical Triage (Sketch)
LLM proposes diagnosis candidates; DAC validates against constraints (drug interactions, dosage limits, contraindications). Output includes justification chain with deterministic acceptance logic.

---

**End of White Paper v0.1**

