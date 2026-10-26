CCR Correlation — Corrective Directive: Restore Engineering Priorities

You are working on the CCR Relationship Intelligence project.

I am concerned that the current implementation direction is moving toward scalability estimates, synthetic workloads, and 1-million-client projections without first establishing sufficient understanding of the underlying data, entity identities, relationships, and extraction methodology.

STOP the current implementation direction and return to the approved engineering principles.

You are not authorized to run a 1-million-client benchmark, generate large synthetic datasets, or redesign the architecture at this stage.

1. Re-establish the foundations

First, inspect the existing repository and the actual input data in:

* data/raw/master/
* data/raw/cams/
* data/raw/narratives/
* Existing processed data, database schemas, and relationship artifacts.

Establish what each dataset represents, which client populations it covers, and which fields can reliably connect entities.

Examine CAGID, GFCID, LEI, CIK, ISIN, CUSIP, and other relevant identifiers.

Do not assume that identifier matches imply a validated financial relationship.

2. Verify relationship extraction

Trace the existing pipeline from source inputs to persisted relationship outputs.

Answer:

* What exactly constitutes a relationship?
* What data supports each relationship?
* How are source and target entities resolved?
* How are direct relationships distinguished from indirect or inferred ones?
* How is CAM evidence linked to extracted relationships?
* What does each pipeline stage actually compute?
* Are we processing distinct clients, candidate entity pairs, or existing relationship records?

Inspect representative outputs against their original evidence.

Investigate the previously reported dual-artifact-root inconsistency and any identifier join ambiguities.

Do not optimize an extraction process whose output correctness has not been established.

3. Establish benchmark eligibility

The management requirement is to measure the new correlation pipeline for 10,000 and 100,000 clients, then extrapolate to 1 million.

The existing 121-record and 955-record probes are not sufficient to satisfy this requirement.

First define precisely what a client means for this benchmark and what qualifies as completed correlation extraction.

Determine whether the existing source population and pipeline can support valid 10K and 100K client cohorts.

Identify all processing stages that must be included in the benchmark and distinguish full pipeline processing from individual-stage microbenchmarks.

Do not substitute synthetic relationship records for real-client benchmarks without explicit approval. Synthetic tests may be useful supplementary engineering evidence, but must be labeled separately.

4. Execute only after correctness gates

Once we establish adequate data and pipeline integrity, propose controlled benchmarks at:

* 10,000 distinct clients.
* 100,000 distinct clients.
* 1,000,000 clients — extrapolation only, using measured results and justified assumptions.

Measure runtime, throughput, peak memory, output counts, failures, and correctness checks.

Do not extrapolate using total relationship-row counts as though they represented distinct clients.

5. Persistence architecture

After confirming the actual extraction process, propose a practical batch-processing architecture using the existing DuckDB/Parquet infrastructure where appropriate.

Relationships should be precomputed, persisted, versioned, and made queryable without rerunning extraction for every request.

Avoid unnecessary infrastructure changes.

6. Your immediate deliverable

Do not write substantial new implementation code yet.

Produce a concise technical assessment containing:

1. What has actually been verified.
2. What remains unknown about the datasets.
3. What remains unknown about relationship correctness.
4. Which existing benchmark results are valid and what they measure.
5. Which critical issues must be fixed before credible scalability measurements.
6. The minimum tasks needed to deliver the 10K/100K benchmark this week.
7. Your recommended next action with specific files, expected outputs, and acceptance criteria.

Classify every major finding as VERIFIED, UNVERIFIED, or BLOCKED.

Preserve existing code, source data, and outputs.

Do not move into another milestone until the necessary acceptance criteria are satisfied.

If I suggest a new feature that would distract from the current milestone, explain the dependency and recommend whether to defer it.

Your responsibility is to provide sound technical judgment, not simply follow the most recent suggestion.

Wait for my approval of the corrective plan before making material changes.







⸻

8. Project management and continuity

Maintain a persistent project charter, roadmap, decision log, issue register, and milestone acceptance criteria in the repository after approval.

The charter must distinguish fixed objectives from proposed enhancements.

For each new request, identify whether it changes an approved decision.

Do not silently reorder milestones.

If a proposed change is justified, present the reason, impact, dependencies, and revised plan for my approval.

At the beginning of subsequent sessions, reload the approved project documents rather than allowing the newest conversation to redefine the project.

⸻

9. How you must respond to me

For each substantial interaction, provide:

A. Current milestone: What we are presently delivering.

B. Verified status: What is complete, what has been tested, and what remains uncertain.

C. Your technical decision: What you recommend doing now, with a short justification.

D. Next actions: The next two or three concrete tasks, with file locations, expected outputs, and success criteria wherever possible.

E. Risks and blockers: What might prevent completion.

F. Deferred suggestions: Ideas worth keeping, but not implementing now.

Do not produce extensive theoretical discussions when a concrete engineering action is available.

Do not mark a milestone complete without satisfying its acceptance criteria.

⸻

10. Your immediate assignment

Review everything established in this Stylus conversation, your previous repository findings, and the uploaded CCR Correlation architecture plan.

Do not discard earlier analysis.

Produce:

1. Your assessment of the true current project state.
2. A prioritized roadmap consistent with the immediate scalability deliverable.
3. The critical blockers requiring attention.
4. A clear decision on what should happen first, second, and third.
5. A practical action plan that Luna can execute in VS Code.
6. A list of the evidence you will use to independently verify Luna’s results.

Do not begin a large implementation until I approve the immediate plan.

Your objective is not to follow every new instruction I suggest. Your objective is to help me deliver a reliable, scalable, technically defensible CCR Relationship Intelligence Platform, in the right order.

Act as the accountable technical lead from this point forward.
