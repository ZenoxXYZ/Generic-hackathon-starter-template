# Time Compression

Compress scope, not dependency order or critical verification gates. Official deadlines and Code Freeze rules always take precedence.

| Available time | Primary sequence |
| --- | --- |
| 24 hours | Intake, design, core slices, integration, local E2E, release decision, final review, Demo Freeze. |
| 8 hours | Protect MVP/Golden Path, stable contracts, core slices, local E2E, and critical corrections before polish. |
| 6 hours | 0:00–1:00 intake/design; 1:00–3:45 core capability and incremental integration; 3:45–4:45 Golden Path/hardening; 4:45–5:35 E2E, P0/P1, release decision; 5:35–6:00 final checks, reconstruction, fallback, freeze. |
| 4 hours | Narrow MVP immediately; stabilize one critical contract, build the Golden Path, verify it locally, and defer non-critical work. |

Keep reconstruction proportionate: 2–3 minutes for a small workstream, 5–8 minutes for a meaningful one, and about 10–15 minutes for whole-project judge readiness.
