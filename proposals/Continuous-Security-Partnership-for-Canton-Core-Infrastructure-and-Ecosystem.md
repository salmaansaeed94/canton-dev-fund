# Development Fund Proposal: Continuous Security Partnership for Canton Core Infrastructure and Ecosystem

**Author:** VulSight (vulsight.com) — Salman [@ItsShad0wWalker](https://twitter.com/ItsShad0wWalker) & Waleed (Technical Lead)  
**Status:** Draft  
**Created:** 2026-03-04

---

## Abstract

VulSight proposes a continuous security partnership for the Canton Network structured in two stages: a **zero-upfront-cost, pay-per-vulnerability core protocol audit** followed by a milestone-funded ecosystem security buildout.

**Stage 1 — Core Protocol Audit (Pay-Per-Vulnerability):** VulSight performs a deep, manual security audit of Canton's Scala infrastructure — sequencer, mediator, participant nodes, cross-domain protocols, Daml runtime, Splice components, and API surfaces — at zero cost to the Canton Foundation unless exploitable vulnerabilities are confirmed. Payment is made only for validated findings:

- **$20,000 per Critical vulnerability**
- **$10,000 per High vulnerability**
- **$5,000 per Medium vulnerability**

If VulSight finds nothing, Canton pays nothing. The Foundation's downside is zero.

**Stage 2 — Ecosystem Security Buildout (Milestone-Funded):** Contingent on Stage 1 demonstrating value, VulSight delivers permanent ecosystem security capabilities: Daml-specific security research, a public vulnerability knowledge base, quarterly protocol re-audits, ecosystem application audit capacity, security office hours, and incident response retainer.

Canton is now critical infrastructure for institutional finance. DTCC is tokenizing U.S. Treasury securities on the network. Goldman Sachs, BNP Paribas, Tradeweb, Citadel Securities, and nearly 400 ecosystem participants depend on the correctness of Canton's protocol layer. This proposal puts VulSight's reputation and resources on the line before asking the Foundation to commit a single Canton Coin — because we are confident enough in our ability to find real vulnerabilities in Canton's Scala codebase that we are willing to work for free if we can't.

---

## Specification

### 1. Objective

Canton's security guarantees — sub-transaction privacy, BFT consensus integrity, cross-domain atomic transactions, Daml authorization enforcement — are ultimately delivered by Scala code running on sequencers, mediators, and participant nodes operated by independent organizations. Bugs at this layer do not cause individual application failures; they break the trust model for the entire network.

**The problem:** Canton's codebase is large, complex, and evolving rapidly. Point-in-time audits — whether traditional or contest-based — produce findings for the version reviewed but provide no defense against regressions in subsequent releases. Meanwhile, the ecosystem of applications building on Canton lacks access to security expertise that understands Daml's unique authorization model and Canton's privacy-preserving architecture.

**The intended outcome:** A continuously hardened Canton protocol stack with retained audit context across releases; a public Daml security knowledge base that raises the security floor for all builders; and a clear, funded pathway for any Canton ecosystem application to access security auditing from a team with deep Canton-specific expertise — initiated through a zero-risk engagement model that ensures the Foundation pays only for verified security value.

### 2. Implementation Mechanics

#### Stage 1 — Core Protocol Security Audit (Pay-Per-Vulnerability)

Deep, manual adversarial review of Canton's Scala implementation. VulSight bears all cost and resource risk. The Foundation pays only for confirmed, validated vulnerabilities and gets an Audit report.

**Methodology:**

- **Key threat derivation and ranking:** Identify the 15–25 highest-impact threats against Canton's protocol guarantees (transaction forgery, privacy boundary violation, consensus manipulation, unauthorized state changes, liveness denial, cross-domain atomicity failure). Rank by damage potential and feasibility based on Canton's actual deployment topology.
- **Attack surface mapping:** For each ranked threat, trace code paths from entry points (Ledger API, gRPC interfaces, network protocol messages, operator commands) through internal logic (sequencer message ordering, mediator confirmation flows, topology manager decisions, Daml interpreter execution) to state changes.
- **Deep manual code review:** Focused review of mapped paths targeting logic errors, concurrency bugs, serialization mishandling, cryptographic misuse, cross-domain edge cases, and authorization bypass vectors.
- **Exploitation validation:** Every suspected vulnerability is validated with a proof-of-concept exploit or detailed exploitation scenario. Findings without a credible attack path are downgraded to Informational (unpaid). No padding the report with theoretical concerns — we only get paid for real bugs.
- **Remediation support:** Code-level fix recommendations and suggested regression tests for every paid finding, plus one round of remediation verification for all Critical and High findings at no additional cost.

**Target components:**

- **Sequencer and Mediator:** Message ordering integrity, confirmation request/response validation, encrypted sub-transaction routing, conflict resolution logic. Includes new processing paths introduced in the Canton 3.3/3.4 migration (CIP-0089) that have not been independently reviewed.
- **Participant Nodes:** Daml interpreter execution, authorization model enforcement, contract visibility boundary integrity, private contract store isolation, DAR package deployment validation.
- **Cross-Domain Protocols:** Atomicity and coordination guarantees across independently operated sync domains — Canton's most architecturally unique and complex attack surface.
- **Topology Manager:** Topology state transitions, identity management, key rotation, certificate chain validation.
- **Ledger API and gRPC Surfaces:** External input validation, party authentication, event stream integrity. The Canton Network Token Standard (CIP-0056) and dApp Standard (CIP-0103) have introduced new API surfaces expanding the attack surface.
- **Splice Open-Source Components:** Token standard implementations, validator node deployment logic, governance application attack surface.

**Severity classification:** Severity ratings follow industry-standard definitions aligned with Canton's architecture:

- **Critical:** Exploitable vulnerability enabling theft or permanent loss of assets, consensus bypass, or complete privacy model breakdown. Exploitable by external attacker or single malicious operator without requiring collusion.
- **High:** Exploitable vulnerability enabling significant unauthorized state changes, partial privacy breach, liveness denial affecting multiple participants, or privilege escalation across trust boundaries. May require specific preconditions.
- **Medium:** Vulnerability enabling limited unauthorized behavior, information leakage below the level of full privacy breach, denial-of-service against individual components, or authorization weaknesses requiring unlikely but possible preconditions.
- **Informational / Low:** Code quality issues, deviations from best practices, theoretical concerns without demonstrated exploit paths. Reported in the final audit report but not subject to payment.

**Why this model works for both parties:**

- **For Canton Foundation:** Zero financial risk. The Foundation commits no budget unless VulSight delivers confirmed, exploitable vulnerabilities with proof-of-concept demonstrations. If the codebase is clean, the Foundation pays nothing and receives a comprehensive audit report confirming the protocol's security posture — itself a valuable deliverable for institutional participants evaluating Canton.
- **For VulSight:** We are confident enough in our methodology and track record to absorb the cost of a multi-month audit engagement. The pay-per-vulnerability model is our commitment to results over billing. We discovered CVE-2026-26314 in Ethereum's Geth client — a high-severity vulnerability in the most widely deployed L1 execution client in production. We do not propose engagements where we expect to find nothing.

#### Stage 2 — Ecosystem Security Buildout (Milestone-Funded, Contingent on Stage 1)

Activated after Stage 1 demonstrates value. Milestone-funded to build permanent security capabilities for the Canton ecosystem.

**Phase 2A — Daml Security Tooling and Public Knowledge Base (Months 1–2 of Stage 2)**

- **Daml Security Audit Framework:** Open-source, Canton-specific vulnerability pattern guide covering authorization logic flaws, signatory/observer privilege escalation, contract archival race conditions, cross-domain atomicity violations, time-handling edge cases, visibility boundary leakage, and DAR package dependency attacks.
- **Canton Vulnerability Pattern Database:** Structured repository of 20+ attack patterns with severity ratings, affected components, detection methods, and remediation strategies.
- **Automated Daml Security Linting Rules:** Static analysis rules for common Daml misconfigurations, packaged for CI/CD integration.

**Phase 2B — Continuous Security Partnership (Months 3–9 of Stage 2)**

- **Quarterly Protocol Re-Audit:** Review of protocol changes, CIP implementations, and version upgrades with full retained context from Stage 1.
- **Ecosystem Application Audit Pipeline:** Dedicated audit capacity for Canton ecosystem projects.
- **Security Office Hours:** Monthly open sessions for Canton developers.
- **Incident Response Retainer:** Emergency security response and coordinated disclosure support.
- **CIP Security Review:** Proactive security review of Canton Improvement Proposals before implementation.

### 3. Architectural Alignment

This work directly serves the Canton Foundation's mandate under CIP-0082 (Development Fund for security as a core public good) and CIP-0100 (ecosystem fund governance).

**Privacy model validation:** Audit will validate sub-transaction privacy guarantees under adversarial conditions — including malicious participant nodes attempting to extract information beyond authorized visibility scope, and colluding parties attempting to reconstruct private transaction data from individual views.

**Consensus integrity testing:** The Global Synchronizer's 2/3 BFT consensus will be stress-tested against Byzantine fault scenarios including colluding Super Validators, message reordering, and governance vote manipulation.

**Cross-domain atomicity assurance:** Specific focus on atomic cross-domain composition security — ensuring atomicity holds across independently operated sync domains even when one or more domains behave adversarially.

### 4. Backward Compatibility

*No backward compatibility impact.* All findings responsibly disclosed to the Tech & Ops Committee before any public communication. Remediation recommendations designed to be implementable without breaking changes to existing integrations.

---

## Milestones and Deliverables

### Stage 1: Core Protocol Audit (Pay-Per-Vulnerability)

#### Milestone 1: Threat Model, Attack Surface Map, and Audit Kickoff

- **Estimated Delivery:** 3 weeks from approval
- **Focus:** Key threat identification, attack surface mapping, audit plan coordination with Canton engineering
- **Deliverables:**
  - Ranked threat catalog (15–25 threats)
  - Attack surface map with targeted code modules and entry points
  - Agreed audit plan with Canton core engineering team
- **Funding:** $0 (VulSight-funded)

#### Milestone 2: Core Audit Report and Findings

- **Estimated Delivery:** 8 weeks after Milestone 1
- **Focus:** Deep manual code review. Consolidated findings with exploitation validation
- **Deliverables:**
  - Full audit report with all findings, severity ratings, root cause analysis, proof-of-concept exploits, and code-level fix recommendations
  - Executive summary for non-engineering stakeholders
  - Threat coverage matrix
- **Funding:** Pay-per-vulnerability ($20K USD Critical / $10K USD High / $5K USD Medium) Equivalent in CC

#### Milestone 3: Remediation Verification

- **Estimated Delivery:** 2 weeks after Canton engineering completes Critical/High fixes
- **Focus:** Verify all Critical and High fixes are correct and do not introduce new issues
- **Deliverables:**
  - Remediation verification results with documented pass/fail for each fix
  - Updated final report reflecting fix status
- **Funding:** $0 (included in Stage 1)

---

### Stage 2: Ecosystem Security Buildout (Milestone-Funded)

*Contingent on Stage 1 demonstrating value. Submitted for committee approval after Stage 1 completion.*

#### Milestone 4: Daml Security Framework and Research

- **Estimated Delivery:** 8 weeks after Stage 2 approval
- **Focus:** Public Daml security research knowledge base
- **Deliverables:**
  - Published Daml Security Audit Framework (v1.0, open-source)
  - Canton Vulnerability Pattern Database (20+ patterns)
  - Minimum 2 technical blog posts co-published with Canton Foundation
- **Funding:** $25,000 USD equivalent in CC upon committee acceptance

#### Milestone 5: Continuous Security Partnership — Operational

- **Estimated Delivery:** Month 6 of Stage 2
- **Focus:** Continuous coverage and ecosystem audit capacity
- **Deliverables:**
  - 2 quarterly protocol re-audits completed
  - Minimum 2 ecosystem application audits completed
  - Minimum 6 security office hours sessions delivered
  - Incident response retainer active
  - CIP security review participation documented
- **Funding:** $25,000 USD equivalent in CC upon committee acceptance

#### Milestone 6: Annual Security Review and Year 2 Proposal

- **Estimated Delivery:** Month 9 of Stage 2
- **Focus:** Year-end assessment and forward planning
- **Deliverables:**
  - Annual security report
  - Updated vulnerability pattern database
  - Third quarterly re-audit completed
  - Minimum 3 total ecosystem application audits
  - Minimum 9 total security office hours sessions
  - Year 2 engagement proposal
- **Funding:** $15,000 USD equivalent in CC upon committee acceptance

---

## Acceptance Criteria

The Tech & Ops Committee will evaluate completion based on:

**Stage 1 (Pay-Per-Vulnerability):**

- All deliverables (threat model, audit report, remediation verification) completed to professional quality regardless of vulnerability count
- Each paid finding includes a reproducible proof-of-concept exploit or detailed exploitation scenario — not theoretical concerns
- Fix recommendations are specific to affected code with suggested regression tests — not generic guidance
- Severity classifications follow the definitions specified in this proposal and are subject to committee review if disputed
- Remediation verification covers all Critical and High findings with documented re-review results
- Even if zero vulnerabilities are found, the complete audit report, threat model, and attack surface map are delivered to the Foundation as public goods

**Stage 2 (Milestone-Funded):**

- Deliverables completed as specified for each milestone
- Public Daml security research adopted by at least 3 Canton ecosystem development teams within 6 months of release
- Quarterly re-audit cadence maintained with no gaps exceeding 30 days beyond scheduled delivery
- All work aligns with Canton Foundation governance processes and responsible disclosure standards

---

## Funding

### Stage 1 — Total: Variable (Pay-Per-Vulnerability)

| Severity | Payment per Finding |
|----------|-------------------|
| Critical | $20,000 USD equivalent in CC |
| High     | $10,000 USD equivalent in CC |
| Medium   | $5,000 USD equivalent in CC |
| Low / Informational | $0 (reported but unpaid) |

- Payment triggered upon committee acceptance of each validated finding
- If zero vulnerabilities are found, Canton Foundation pays $0 and still receives the complete audit report, threat model, and attack surface map
- No cap on total Stage 1 payout — every confirmed vulnerability is paid at its severity rate
- Severity disputes resolved by Tech & Ops Committee with input from Canton core engineering

### Stage 2 — Total: $65,000 USD equivalent in CC

- Milestone 4 *(Daml Security Framework)*: $25,000 USD equivalent in CC
- Milestone 5 *(Continuous Security — Operational)*: $25,000 USD equivalent in CC
- Milestone 6 *(Annual Review)*: $15,000 USD equivalent in CC

### Combined Value Proposition

Stage 1 is zero-risk for the Foundation. Stage 2 is contingent on Stage 1 proving value. The total maximum commitment for Stage 2 is $65,000 — which delivers permanent open-source security tooling, three quarterly re-audits, minimum three ecosystem application audits, nine security office hours sessions, and incident response capability. This is the most cost-efficient path to comprehensive, continuous security coverage for the Canton ecosystem.

### Volatility Stipulation

Stage 1 payments are denominated in USD equivalent, converted to CC at the time of each finding's acceptance. Stage 2 milestone payments are denominated in USD equivalent and paid in CC. Should Stage 2 extend beyond 6 months due to Committee-requested scope changes, remaining milestones will be renegotiated to account for significant USD/CC price volatility.

---

## Co-Marketing

Upon release, VulSight will collaborate with the Canton Foundation on:

- **Joint announcement** of the security partnership through Canton Foundation and VulSight channels
- **Technical blog series** (minimum 4 posts over the engagement) covering Canton security architecture, Daml security patterns, and selected findings after responsible disclosure
- **Developer education:** Security workshops at Canton hackathons, contributions to Canton Core Academy content, and developer community participation
- **Conference presence:** Joint presentations at fintech and blockchain security conferences positioning Canton's security rigor
- **Audit transparency:** Published audit summary reports as trust signals for institutional participants evaluating Canton

---

## Motivation

Canton Network is critical infrastructure for institutional finance. The Canton Foundation launched this Development Fund under CIP-0082 specifically to invest in security as a core public good. Multiple teams are proposing security engagements for Canton — which validates the urgency. But the Foundation should carefully evaluate what each proposal actually delivers and what risk it places on the Foundation's budget.

VulSight's pay-per-vulnerability model is the only proposal in this cohort that places zero financial risk on the Foundation for the core protocol audit. We are not asking Canton to pay for our time, or our methodology. We are asking Canton to pay only for confirmed, exploitable vulnerabilities — the actual security value delivered.

We can make this offer because we have a track record that justifies the confidence:

- **CVE-2026-26314** — Responsible disclosure of a high-severity vulnerability in Ethereum's Geth client, the most widely deployed L1 execution client in production. This is protocol-layer infrastructure vulnerability research — the exact class of work Canton's Scala codebase demands. No other team proposing to audit Canton has demonstrated this capability.
- **Top 15 all-time on Cantina** — The leading competitive audit platform where researchers compete head-to-head. Consistent, verifiable performance against the world's best.
- **100+ completed security audits** across EVM, Move (Aptos/Sui), and Rust (Solana) ecosystems. Canton's hybrid architecture — UTXO-inspired contract models, BFT consensus, privacy-preserving protocols, functional smart contract language — requires exactly this breadth.
- **$500K+ in bug bounties** earned through responsible disclosure across multiple live protocols and chains.

---

## Rationale

**Why pay-per-vulnerability for Stage 1?**

Because it perfectly aligns incentives. Traditional audit pricing pays for time spent regardless of findings. Contest pricing pays for infrastructure and coordination regardless of results. Pay-per-vulnerability means VulSight is economically motivated to find every exploitable bug in the codebase — and the Foundation is economically protected if the codebase is cleaner than expected. This model eliminates the single biggest friction point in grant evaluation: "What if we pay and get nothing actionable?"

**Why continuous partnership for Stage 2?**

A point-in-time audit produces a snapshot that degrades with every subsequent code change. Canton ships continuously — CIP-0089 brought new sequencer paths, CIP-0092 introduced oracle price feeds, CIP-0094 expanded the validator set. Each change reshapes the attack surface. VulSight's Stage 2 maintains continuous coverage with retained context from Stage 1, ensuring each quarterly re-audit builds on accumulated understanding rather than restarting from zero.

**Why VulSight specifically for Canton?**

Canton sits at a unique intersection: Scala-based distributed system, functional smart contract language (Daml), privacy-preserving sub-transaction visibility, BFT consensus, and a permissioned-but-public deployment model with institutional operators. VulSight's cross-ecosystem experience spanning EVM, Move, Rust, and L1 infrastructure maps directly to Canton's hybrid architecture. Our CVE in Geth demonstrates we find bugs in foundational protocol implementations — not just application-layer contracts.

**Complementary to other security approaches:**

VulSight's model is designed to be the anchor security engagement that other activities layer on top of. Contest-based audits are valuable for broad coverage; they discover different bug classes than focused manual review. But they require a knowledgeable team to triage findings, validate severity, and ensure correct remediation. VulSight's ongoing presence provides that institutional memory and technical context — regardless of what other security programs the Foundation activates.


## Separately scoped work
Included in quarterly re-audit (covered by milestone funding):

Patch-level changes and minor bug fixes
Configuration and parameter changes
Small CIP implementations that modify existing code paths (under ~2,000 lines changed)
Regression testing of previously identified vulnerabilities against new versions

Triggers a separately scoped engagement (not covered by milestone funding):

New subsystem integrations (oracle systems, new token standards, bridge implementations)
Major version upgrades that restructure core components
CIP implementations introducing entirely new code modules (over ~2,000 lines of new code)
New consensus mechanism changes or validator architecture modifications

For separately scoped work, VulSight would submit a lightweight addendum proposal with scope, timeline, and pricing — either funded through the Development Fund as a new milestone, or paid directly by the requesting party.
