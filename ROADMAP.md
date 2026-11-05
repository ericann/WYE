# Wye Product & Engineering Roadmap

> **Product direction:** Wye is a runtime analysis workspace for Salesforce Orgs. Multi-Org is its runtime foundation; Permission and Reference are its two core analysis pillars. Wye helps users understand access-control structures, resource relationships, and Org behavior so they can investigate issues and prepare operational or technical decisions.

This roadmap distinguishes current implementation, engineering remediation, and future product direction. A planned capability is not considered delivered until implemented and validated.

## Roadmap at a glance

| Phase | Focus | Outcome |
|---|---|---|
| 0 | Security & release hygiene | Resolve exposed credentials and establish a safe release baseline |
| 1 | Runtime reliability | Make Org context, Session, HTTP requests, and cache behavior consistent |
| 2 | Engineering foundation | Add repeatable tests and build quality gates |
| 3 | Permission Analysis V1 | Deliver reliable Object, Field, and scoped Record access attribution |
| 4 | Advanced Permission Analysis | Add meaningful Compare, What-if, and impact recalculation |
| 5 | Reference V1 | Establish Resource / Relationship analysis from Object and Field entry points |
| 6 | Unified Org Analysis | Combine Permission and Reference for cross-domain and cross-Org analysis |

---

## Phase 0 — Security & release hygiene

**Status:** Local P0 remediation is complete and awaiting pull request, as reported by the maintainer.

- Rotate/revoke exposed OAuth and third-party API credentials.
- Remove credentials from current tracked files and relevant Git history.
- Review documentation, configuration, and distributable artifacts for further exposure.
- Verify old credentials are no longer valid and the replacement release works.

**Exit criteria**
- P0 pull request reviewed and merged.
- Exposed credentials rotated/revoked.
- Current files and relevant Git history cleaned.
- Release artifacts checked for secrets.

Do not treat history rewriting as a substitute for credential rotation.

## Phase 1 — Runtime reliability

**Goal:** Ensure every operation remains bound to the intended Salesforce Org, including asynchronous and concurrent work.

### Org context integrity
- [ ] [#1 — Preserve target Org Host during RestService forced refresh](https://github.com/ericann/WYE/issues/1)
- [ ] [#2 — Pin Org context for the full analysis task](https://github.com/ericann/WYE/issues/2)

### Session and cache integrity
- [ ] [#3 — Correct ChromeStorageAPI remove / clear cache invalidation](https://github.com/ericann/WYE/issues/3)
- [ ] [#4 — Await Session registration during Org switching](https://github.com/ericann/WYE/issues/4)

### Browser runtime boundaries
- [ ] [#5 — Prevent duplicate DOMInspector message listeners](https://github.com/ericann/WYE/issues/5)
- [ ] [#6 — Validate Background message sender and Salesforce Cookie scope](https://github.com/ericann/WYE/issues/6)

**Exit criteria**
- A task started in Org A continues to issue requests only to Org A, even if the selected Org changes.
- Responses are stored under the same Org from which they were fetched.
- Session state and Token state remain consistent during rapid switching.
- Cache deletion cannot return stale in-memory values.
- Runtime listeners do not accumulate during DOM changes/navigation.
- Message sources and Cookie lookup scope are explicitly validated.

## Phase 2 — Engineering foundation

**Goal:** Make critical behavior reproducibly testable before expanding analysis complexity.

- [ ] [#9 — Add core automated tests and build quality gates](https://github.com/ericann/WYE/issues/9)

Initial test priorities:
1. Multi-Org Session registration, switching, and Token refresh.
2. HTTP Host isolation and concurrent refresh behavior.
3. Storage key generation, remove, clear, and cache invalidation.
4. Permission Set / Permission Set Group Grant and Muting aggregation.
5. Explicit Host propagation through RestService and analysis call chains.

Build pipeline target:

`install → typecheck → tests → build`

Start with the high-risk paths; avoid building a large test framework before it is needed.

**Exit criteria**
- Test dependencies and commands work from a clean install.
- Critical service paths have automated regression coverage.
- TypeScript type checking runs as a build gate.
- CI runs install, typecheck, tests, and build.

## Phase 3 — Permission Analysis V1

**Goal:** Move from permission data collection and presentation toward trustworthy access attribution.

### Object and Field permissions
- Validate combined Permission Set / Permission Set Group Grant and Muting behavior.
- Integrate Graph analysis into the actual Permission analysis path, or remove unused graph construction.
- Ensure Muting semantics are reflected in effective-path analysis.
- Keep the Tree as the readable structure and attribution view; use Graph for compound, cross-branch relationship analysis.
- Add real-Org validation cases and automated regression tests.

Related: [#7 — Integrate Permission Graph and handle Muting paths](https://github.com/ericann/WYE/issues/7)

### Record access
- [ ] Distinguish actual access results (for example, UserRecordAccess) from identified grant sources.
- [ ] Improve direct User Share attribution.
- [ ] Evaluate GroupMember and nested Group expansion.
- [ ] Define support boundaries for Role Hierarchy and Sharing Rules.
- [ ] Expose partial, unknown, or failed source resolution instead of silently implying complete attribution.

Related: [#8 — Complete Record Access sharing-source attribution boundaries](https://github.com/ericann/WYE/issues/8)

**Exit criteria**
- Supported Object / Field results are validated against real Org behavior.
- Muting paths are not presented as effective grants.
- Record access output clearly separates observed access from known attribution.
- Unsupported or unresolved sources are explicitly marked.
- Tree and Graph contribute distinct, connected analysis value.

## Phase 4 — Advanced Permission Analysis

**Goal:** Extend Permission from explanation of current state to comparison and controlled simulation.

### Compare
Compare users, permission assignments, Permission Set Groups, Org configurations, or captured states. Explain changes in effective permissions and access paths, not only raw metadata differences.

### What-if
A What-if operation must modify an analysis model and recalculate its consequences. Hiding a node or comparing paths alone is not a complete simulation.

Suggested progression:
1. Permission-source changes.
2. Recalculation of effective grant paths, including Muting.
3. Re-evaluation of Object, Field, and supported Record access.
4. Clear separation between simulated results and the actual Org state.

### Impact analysis
Identify which permissions or access outcomes change when a provider or relationship changes. Distinguish graph reachability from loss of all valid authorization paths after recalculation.

**Exit criteria**
- Compare has explicit baseline and comparison models.
- What-if performs recalculation rather than presentation-only changes.
- Impact results identify affected outcomes and explain their evidence.
- Simulations never imply that the live Org has been changed.

## Phase 5 — Reference V1

**Goal:** Establish a minimal, evidence-backed Resource and Relationship model.

- [ ] [#10 — Define and implement Reference V1](https://github.com/ericann/WYE/issues/10)

### Initial scope
- Use Object and Field as the primary analysis entry points.
- Discover related Buttons, Flows, Apex Classes, Triggers, and other selected metadata resources.
- Define relationship semantics rather than representing every association as an undifferentiated edge.
- Preserve evidence and distinguish confirmed, inferred, and possible relationships.
- Start with reliably discoverable static/configuration relationships; do not claim complete runtime tracing.

### Suggested model concepts
- **Resource:** identity, type, API name, Org context, and relevant metadata.
- **Relationship:** source, target, semantic type, evidence, and confidence/provenance.

### Explicit non-goals for V1
- Full-Org dependency graph completeness.
- Complete runtime execution tracing.
- Automatic inference of every business execution chain.
- Automated execution or modification of business processes.

**Exit criteria**
- Supported resource and relationship types are documented.
- Object / Field entry points return related resources with traceable evidence.
- Confirmed, inferred, and possible relationships are distinguishable.
- At least one real-Org scenario validates the model and its limitations.

## Phase 6 — Unified Org Analysis

**Goal:** Create compound analysis value by combining the two core pillars.

### Permission × Reference
For a user-facing operation, connect the resource path involved in the operation with the user's effective Object, Field, and Record access. Help explain not only that access is missing, but where the relevant resource participates and which permission constraints may matter.

### Cross-Org analysis
Build on the Multi-Org foundation to compare:
- Permission differences for equivalent users or roles.
- Metadata/resource relationship differences.
- Environment drift between Sandbox and Production.
- Combined permission and resource changes across Orgs.

### Analysis to decision
Organize results around the user's question, evidence, impact, and possible next investigation or operation. Wye should prepare users to make decisions, not silently make business decisions on their behalf.

This phase is a longer-term direction, not a prerequisite for the earlier milestones.

---

## Recommended execution order

1. Merge and verify the P0 security remediation.
2. Complete Phase 1 runtime reliability, prioritizing #1, #2, and #3.
3. Establish Phase 2 test and build gates early enough to protect subsequent fixes.
4. Complete Permission V1 attribution and validation.
5. Design Reference V1 against concrete metadata examples, then implement its minimal model.
6. Pursue advanced What-if and unified analysis after the underlying models are trustworthy.

## Milestones

| Milestone | Included phases | Release meaning |
|---|---|---|
| M1 — Reliable Runtime | Phases 0–2 | Secure, Org-consistent, testable foundation |
| M2 — Permission Analysis | Phase 3, with selected Phase 4 groundwork | Trustworthy first analysis pillar |
| M3 — Resource Analysis | Phase 5 | Second analysis pillar established |
| M4 — Unified Analysis | Phases 4 and 6 | Compound analysis, simulation, and cross-Org insight |

## Scope and status discipline

- Multi-Org is the foundation, not the highest-level product definition.
- Permission and Reference are the two core analysis pillars.
- Tree remains the readable structured attribution view; Graph provides compound relationship analysis and should surface through meaningful interactions rather than requiring a permanent full-graph UI.
- The current Reference implementation is a reserved UI/manager entry point, not a delivered relationship-analysis engine.
- Graph algorithms present in source code are not automatically equivalent to integrated, validated What-if or impact-analysis product capabilities.
- Do not claim a capability is complete based solely on the presence of a class, method, UI entry, or algorithm. Completion requires integration, validation, and clear output boundaries.
