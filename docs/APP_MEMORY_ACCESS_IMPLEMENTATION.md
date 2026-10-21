# Application memory access implementation

Scope: expose explicit remember/correct/forget requests and existing document
promotion through OUP, without a turn or a foreground model call. Memory
processing remains in the existing background consolidator. This serves the
application-access follow-up to #2355; it adds no product-specific concepts.

Baseline: origin/main f28aeebc. The earlier seven pipeline tests are retained
as a separate prerequisite commit (rebased from 29471385).

Review slices:

1. Durable host-request admission and focused recovery/replay tests.
2. Source-filtered promotion and serialization of concurrent nomination, with
   existing callers retaining their defaults.
3. OUP types, codecs, capability and permission wiring, authenticated handlers,
   protocol/authorization tests, specification and wire-inventory updates.

Acceptance: the same request id/body is admitted once even after consumption
or restart; conflicting bodies fail; target validation uses the authenticated
profile; restricted credentials cannot invoke either method; promotion filters
before limiting and preserves real-load eligibility. Acknowledgements mean
accepted/staged, never model completion. Tests must exercise the actual handlers
and existing consolidation, not just parameter helpers.

No permanent app record ledger, consumer revision changes, teacher policy,
background model scheduler, deployment or publication is included. Full product
integration and model-quality/latency acceptance remain separate work. Handling
arbitrary in-flight regeneration of deleted information is not a requirement.
