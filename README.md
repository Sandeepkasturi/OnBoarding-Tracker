## Onboarding Tracker — ServiceNow Scoped App

### What it does?
Automatically generates a 6-task onboarding checklist when a new hire 
record is created, assigns tasks to the correct department with 
due dates calculated relative to the joining date, and tracks 
completion percentage in real time.

### Architecture
- OnboardingTaskGenerator (Script Include) — task template engine + completion calculator
- After BR on New Hire — triggers task generation on insert
- After BR on Onboarding Task — recalculates completion % on state change

### Skills demonstrated
- Multi-table scoped app design (parent/child relationship)
- GlideDateTime offset calculations
- Rollup field pattern (completion % from child records)
- Script Include reusability (template-driven record generation)

### Builds on
S1 — Incident Auto-Tagger (same Class.create() + Before/After BR pattern, 
applied here to HR onboarding lifecycle automation instead of ITSM classification)
### Debugging note
Initial build hit a scoped-table naming issue — GlideRecord calls referenced 
unscoped table names (u_onboarding_task) instead of the platform-generated 
scoped names (x_2064375_onboar_0_onboarding_task). Root-caused via system 
log EvaluatorException trace, fixed across the Script Include and both 
Business Rules. This is a common trap when developing inside scoped apps 
and worth knowing before you hit it in a client engagement.
