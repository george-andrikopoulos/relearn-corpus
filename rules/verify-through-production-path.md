+++
tag = "R:verify-through-production-path"
title = "Verify through the production path"
error_class = "Verifying a feature through a stand-in wiring (dev override, mock transport, alternate config channel) instead of the exact channel production uses"
home = { kind = "global" }
created = "2026-07-16"
origin = "mined"
status = { kind = "active" }
authority = { kind = "local", version = 1 }
incident = "An IP allowlist passed every smoke test through a development configuration override. The production path assembled the same setting differently and produced malformed input, so the headline security feature would have shipped silently disabled and failing open. Nothing in the test suite exercised the channel the deployment actually used; it was caught in a pre-deploy review by someone asking which line of production wiring the tests had never executed."
+++

Before declaring anything verified, run at least one check through the exact channel production uses: same env var, same startup script, same config file, same transport. A test that exercises a stand-in is evidence the stand-in works, not that the feature does. Ask: which line of production wiring did my test NOT execute? That line is where it breaks.
