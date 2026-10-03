# What is system architecture
## Defining this in term of developing software application
### System Design is somthing that makes your app scalable on basis of the architecture , langugae , dependencies and techniques.
 
'''
I will use notebookLM and Chatgpt to refine my ideas
but first I will do the brainstorm
'''

# This file is for studying the architecture only ! 

# Codebase
 (One codebase, many deploys): Track a single version-controlled repository (Git) per service. The same code is deployed across development, staging, and production environments, differing only in configuration.

# Dependencies (Explicitly declare and isolate): 
Never rely on ambient system tools or libraries. Pin all dependencies explicitly in a manifest (e.g., package.json, requirements.txt, pom.xml) and isolate them using containerization or virtual environments.

# Config (Store config in the environment):
 Separate code from configuration. Store secrets, database URLs, and environment-specific credentials in environment variables (ENV), never hardcoded in source control.

# Backing Services (Treat as attached resources):
 Treat databases, message brokers, SMTP servers, and caches as attached resources via network URLs. Switching from a local MySQL instance to an AWS RDS instance should only require a configuration string change, not a code rewrite.

Build, Release, Run (Strictly separate stages):

Build: Compiles code and packages dependencies into an immutable artifact.

Release: Combines the build artifact with environment-specific config.

Run: Launches the release in the execution environment. Releases cannot be modified at runtime.

# Processes (Execute as stateless, share-nothing processes):
 The app must run as one or more stateless processes. Any state that needs to persist (user sessions, file uploads) must be stored in a stateful backing store like Redis, PostgreSQL, or S3.

# Port Binding (Export services via port binding):
 Do not inject code into an existing web server (like Apache or Tomcat). The application should be entirely self-contained, listening on a designated port (e.g., via Express, Kestrel, or Gunicorn) to handle HTTP traffic.

# Concurrency (Scale out via the process model):
 Scale by adding more worker or web processes horizontally across machines, rather than maximizing vertical threads on a single monolithic machine.

# Disposability (Maximize robustness with fast startup and graceful shutdown): 
Processes must spin up in seconds and shut down cleanly when receiving a SIGTERM signal—finishing in-flight requests, releasing locks, and refusing new work.

# Dev/Prod Parity (Keep dev, staging, and prod identical):
 Minimize the gap between local development and production. Use the exact same backing service engines (e.g., use PostgreSQL locally instead of SQLite if production runs PostgreSQL) to prevent production-only edge cases.

# Logs (Treat logs as event streams):
 Applications should not manage log files or routing. Write unbuffered logs directly to stdout and stderr, letting log collectors (Datadog, CloudWatch, Fluentd) handle aggregation, shipping, and indexing.

# Admin Processes (Run admin/management tasks as one-off processes): 
Run maintenance tasks—such as database schema migrations, one-time scripts, or batch fixes—in an identical environment and against the exact same release release as the running application.