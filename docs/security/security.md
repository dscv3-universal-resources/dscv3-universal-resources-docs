---
nav_order: 3
permalink: docs/security
---

# Security

DSC v3 universal resources are DSC resources designed to interact with
Microsoft's DSC v3 engine. Each DSC resources in the DSC v3 universal
resources repository are build as executable and packaged into a `.zip`
file. This presents security considerations, as executables must be trusted
by the user before execution.

## Resources

Only install trusted DSC resources.

DSC v3 universal resources aren't signed (currently). Resources itself don't
perform any validation or virus scan checks. However, the resources are
open-source and hosted on GitHub. You can review the source code to perform
your own security analysis.
