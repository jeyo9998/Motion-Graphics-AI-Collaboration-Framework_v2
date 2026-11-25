# Motion Graphics AI Collaboration Framework

An open-source project to help compatible AI agents understand, plan, execute, and evaluate real Motion Graphics work across **Alight Motion** and **Adobe After Effects**.

The framework is designed for active AI collaborators—not just assistants that explain workflows. Agents should take useful initiative, work within the tools and permissions actually available, respect each application's own logic, and verify outcomes instead of claiming success without evidence.

> **Project status:** Early development. All seven initial Skills now have draft files. Two have behavioral run records: `project-understanding` (all five cases scored: PU-01 88/100, PU-02 85/100, PU-03 90/100 by the project owner — the governing human score, with reviewer A at 83 and reviewer B at 90 recorded alongside — PU-04 80/100 by the project owner — the governing human score, with reviewer A at 83 and reviewer B at 87 recorded alongside — and PU-05 94/100) and `motion-graphics-principles` (MP-01 95/100, MP-02 90/100, MP-03 93/100). Owner-supplied Alight Motion and After Effects fixtures now live in `evals/fixtures/` under read-only rules. Application procedures, execution integrations, and cross-agent compatibility remain unverified.

## Goals

- Build reusable, portable Agent Skills for Motion Graphics work.
- Support Alight Motion and Adobe After Effects as equal initial application targets.
- Share general Motion Graphics knowledge without forcing identical application workflows.
- Enable active collaboration through a hybrid execution approach: direct file manipulation, scripting/API access where supported, and application interaction where available.
- Evaluate skills with practical tasks and evidence from both target applications.
- Preserve user control, project integrity, and clear permission boundaries.

## Repository map

```text
motion-graphics-ai-framework/
├── AGENTS.md
├── LICENSE
├── README.md
├── PROJECT-SPECIFICATION.md
├── SKILL-ARCHITECTURE.md
├── requirements-dev.txt
├── skills/
│   ├── project-understanding/SKILL.md
│   ├── motion-graphics-principles/SKILL.md
│   ├── application-adaptation/
│   │   ├── SKILL.md
│   │   └── references/
│   │       ├── EVIDENCE-TEMPLATE.md
│   │       ├── alight-motion/README.md
│   │       └── after-effects/README.md
│   ├── motion-graphics-execution/SKILL.md
│   ├── hybrid-execution/SKILL.md
│   ├── visual-evaluation/SKILL.md
│   └── error-analysis/SKILL.md
├── evals/
│   ├── README.md
│   ├── fixtures/
│   │   ├── README.md
│   │   ├── alight-motion/{Motion_Graphics_unik.xml,movement_1.xml,movement_2.xml}
│   │   └── after-effects/{Motion_Graphics_Unik.aep,Motion_Graphics_Unik_Camera.aep,movement_1.aep,movement_2.aep}
│   ├── project-understanding/
│   │   ├── README.md
│   │   ├── cases.md
│   │   ├── scorecard.md
│   │   ├── review-log.md
│   │   ├── scripts/count-extensions.sh
│   │   └── results/
│   │       ├── PU-01/{prompt.md,response.md,evaluation.md,retest-2026-11-24.md}
│   │       ├── PU-02/{prompt.md,response.md,evaluation.md,retest-2026-11-24.md}
│   │       ├── PU-03/{prompt.md,response.md,evaluation.md}
│   │       ├── PU-04/{prompt.md,response.md,evaluation.md}
│   │       └── PU-05/{prompt.md,response.md,evaluation.md,retest-2026-11-24.md}
│   ├── motion-graphics-principles/
│   │   ├── README.md
│   │   ├── cases.md
│   │   ├── scorecard.md
│   │   └── results/
│   │       ├── MP-01/{prompt.md,response.md,evaluation.md}
│   │       ├── MP-02/{prompt.md,response.md,evaluation.md,retest-2026-11-24.md}
│   │       └── MP-03/{prompt.md,response.md,evaluation.md}
│   └── self-review/
│       ├── README.md
│       ├── cases.md
│       ├── scorecard.md
│       ├── fixture-inventory.md
│       └── results/assessment-2026-11-24.md
└── tests/
    ├── README.md
    ├── validate_skills.py
    └── test_count_extensions.sh
```

This is intentionally a small starting structure. `SKILL-ARCHITECTURE.md` defines the responsibility boundaries and handoffs for the planned Skills. Additional skills, application references, collaboration protocols, and benchmark cases will be added incrementally when their responsibilities and tests are clear.

## Skills

| Skill | Responsibility | Status |
|---|---|---|
| `project-understanding` | Understand the user's intent, project context, requirements, constraints, and acceptance criteria before work proceeds. | Draft; all five cases (PU-01–PU-05) run and scored at the current revision |
| `motion-graphics-principles` | Shared creative and motion-design concepts independent of a specific application. | Draft; MP-01/MP-02/MP-03 run and scored, MP-02 re-run after revision |
| `application-adaptation` | Apply verified, application-specific knowledge for Alight Motion and After Effects. | Draft; reference scaffolding only, no verified procedures |
| `motion-graphics-execution` | Coordinate the actual creative task from plan through verified result. | Draft; not tested |
| `hybrid-execution` | Select and coordinate the available file, scripting/API, and application-interaction methods. | Draft; not tested |
| `visual-evaluation` | Evaluate visual and technical outcomes against the task's acceptance criteria. | Draft; not tested |
| `error-analysis` | Diagnose issues, separate evidence from hypotheses, and verify corrections. | Draft; not tested |

## Instructions for AI contributors

AI coding agents working in this repository should read [`AGENTS.md`](AGENTS.md) first. It explains the project boundaries, repository structure, evidence standards, incremental development workflow, and local validation commands. `AGENTS.md` guides work on the repository; individual files under `skills/` define task-specific Agent Skills.

## How to use a skill

Each skill is a self-contained directory with a required `SKILL.md` file. Use the skill with an AI-agent client that supports the Agent Skills format, following that client's current installation and discovery instructions. Support and loading behavior vary by agent implementation; the presence of a skill in this repository does not guarantee that every agent can use it identically.

Start with [`project-understanding`](skills/project-understanding/SKILL.md). It helps the agent form a reliable understanding of the task and prepare a concise handoff for the next relevant skill.

## Evaluate a skill

Scenario-based evaluation packs live in `evals/`. See [`evals/README.md`](evals/README.md) for the status matrix. [`evals/project-understanding/`](evals/project-understanding/README.md) and [`evals/motion-graphics-principles/`](evals/motion-graphics-principles/README.md) both hold scored run records with the raw prompt and response preserved. Owner-supplied application projects are stored under [`evals/fixtures/`](evals/fixtures/README.md) with SHA-256 records and read-only rules; PU-03 and PU-04 ran against them on 2026-11-24 (PU-04 on the fixtures plus screen recordings kept outside the repository, referenced by path and hash). These evaluations require an AI-agent client that can load the skill; the repository validator does not test semantic behavior.

## Validate the current skills

Python 3.10 or newer is recommended.

```bash
python -m pip install -r requirements-dev.txt
python tests/validate_skills.py
bash tests/test_count_extensions.sh
```

The validator checks basic Agent Skills frontmatter and repository naming conventions. It is a local project check, not a replacement for the official Agent Skills reference validator or platform-specific testing.

## Development principles

1. **Simple** — use the least complicated approach that meets the user's goal.
2. **Structured** — make responsibilities, inputs, outputs, and handoffs clear.
3. **Evaluated** — test outcomes against observable criteria and available evidence.
4. **Improved** — refine skills using verified findings and practical feedback.

We develop incrementally: design one skill, implement it, validate its structure, test it with realistic scenarios, review the evidence, then proceed to the next skill.

On 2026-11-24 the project owner directed drafting of all seven Skills in one continuation pass. The draft files were created to preserve the agreed architecture, but this does not satisfy each Skill's behavioral evaluation gate. Skills other than `project-understanding` remain untested.

## Safety and project integrity

Agents must be honest about tool and application access. They must not claim to have inspected, changed, rendered, or verified files unless they actually did so. Preserve original user work where practical. Obtain appropriate authorization before destructive, overwriting, publishing, or otherwise consequential actions.

## License

**MIT** — see [`LICENSE`](LICENSE). Selected 2026-11-24 by the project owner: MIT is short, OSI-approved, and maximally compatible, which matches the framework's stated goal of reusable, portable Skills that other agents and teams can adopt without friction. It also follows the project's first development principle, *Simple*.

Scope: the license covers the framework's original work — the seven Skills, this documentation, the evaluation packs, and the test code. It does **not** cover:

- the application projects under `evals/fixtures/` — these are the project owner's own work, included as test material only and not offered under any license;
- the screen recordings — they live outside the repository, are not distributed, and are referenced by path and hash only.

If a different license ever becomes preferable (for example, Apache-2.0 if a formal patent grant is wanted), that is a release-level decision to be recorded in `AGENTS.md` and `SKILL-ARCHITECTURE.md` before it is changed.

## Contributing

Contribution guidance will be added before the first public contribution cycle. In the meantime, proposed changes should preserve the project goals, keep application-specific claims evidence-based, and include relevant validation or test notes.

## Agent Skills format

The skills are authored to follow the open Agent Skills format: a skill directory contains a `SKILL.md` with YAML frontmatter including `name` and `description`; optional resources can be added when needed. See the [Agent Skills specification](https://agentskills.io/specification) for the current format details.
