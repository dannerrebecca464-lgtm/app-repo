# Procedure Rules — MiniBank DevOps Project

These rules apply to every request made in this project, across every session. Follow them even if a specific prompt doesn't repeat them.

## 1. Golden Rule
App code stays **trivially simple**. Infrastructure stays **enterprise-grade**. This project exists to prove DevOps/DevSecOps skill, not to build a convincing banking app. If a suggestion adds business-logic complexity (e.g., saga rollback, fraud scoring, compliance workflows) without adding infrastructure/DevOps value, do not add it — flag it as out of scope instead.

## 2. Scope Lock — What You Actually Build
Your job is the **application code only**: the 4 microservices (API Gateway, IAM, Wallet/Ledger, Notification) — the code that runs inside the container, not the container definition itself.

You do **not** build, write, or generate: Dockerfiles, `.dockerignore` files, Terraform, Ansible, Kubernetes manifests, Helm charts, GitHub Actions/CI-CD pipelines, or any security tooling. Those are mine to write. If I ask for help with any of those, treat it as a deliberate exception I'm requesting for that moment — not a standing part of your role — and push back / confirm before proceeding.

When a service needs a Dockerfile, leave it out entirely (don't stub one, don't leave a placeholder) — just note in your summary what the app needs from it (base image constraints, exposed port, entrypoint command, env vars expected) so I have what I need to write it myself.

The Swagger/OpenAPI UI, Postman collection, and k6 scripts are also mine unless I explicitly hand you a specific piece of them.

Do not add extra services, endpoints, or tools beyond the 4 microservices on your own initiative — even if they seem like natural extensions or "best practice." If something seems missing, ask first instead of adding it.

## 3. Language
Use **Python for all 4 microservices** (API Gateway, IAM, Wallet/Ledger, Notification) — no mixing languages between services. IAM is already built in Python (FastAPI/SQLAlchemy/Alembic); match that stack and its established patterns (config-via-env, pytest for tests, same health-check style) across the remaining services for consistency. Do not introduce a different language or framework on your own initiative, even if you think it fits a particular service better — this project is judged on infra/DevOps work, and language consistency keeps the app-code side simple to build, explain, and defend.

## 4. Build Order & Summary Format
Build the remaining services (Wallet/Ledger, Notification — or whichever haven't been built yet) one after another in this session, without stopping for review between each one.

After all requested services are built, give me **one total summary covering all of them**, organized **per service, not per file**. For each service, include:
- What it does (1–2 sentences)
- Key endpoints
- Deliberate simplifications / tradeoffs for that service (own these in interviews)
- What I'll need to know to write its Dockerfile (per Rule 2 — no Dockerfile/`.dockerignore` written by you)

Do not give a file-by-file breakdown or a "DevOps concepts demonstrated per file" section like the IAM summary had — keep it at the service level, concise, and scannable across all services in one pass.

If you hit something genuinely ambiguous or missing from the scope doc while building, ask before proceeding rather than guessing — don't let build speed become an excuse to skip Rule 7 (flagging scope conflicts).

## 5. Explain, Don't Just Deliver
For every piece of code or config produced, include a short plain-language explanation of:
- What it does
- Why it's built this way (which DevOps concept it's demonstrating)
- Any tradeoffs or simplifications made

I need to be able to explain every part of this in an interview, so unexplained code is not acceptable, no matter how correct it is.

## 6. No Silent Scope Creep
Do not add extra libraries, patterns, abstractions, or "nice to have" features unless explicitly requested. If you think something should be added, say so and wait for confirmation — do not include it by default.

## 7. Flag Anything That Contradicts the Scope Doc
If a request from me conflicts with the finalized scope document (e.g., I accidentally ask for a 5th service or a custom frontend), point out the conflict before proceeding, rather than silently complying or silently ignoring it.

## 8. Ownership Split
- **Application code** (the 4 services): this is your job. AI-assisted generation is fine here, since it's meant to be minimal — but still explained per Rule 5.
- **Everything that packages or deploys the app** (Dockerfiles, `.dockerignore`, Terraform, Ansible, K8s manifests, CI/CD, security tooling in Project 2): this is entirely mine to write by hand. This is the part being evaluated for the internship, and it needs to be demonstrably my own work — not generated, not co-written. If I bring questions about any of this here, answer conceptually or review what I've written, but do not produce it for me.

## 9. Session Continuity
At the start of each new session, I will re-share the current state of the scope doc and what's been built so far. Treat that as the source of truth over any assumption carried from training data or prior general knowledge of similar banking-app architectures.
