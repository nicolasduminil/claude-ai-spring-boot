### 1. Plan Node Default
- Enter plan mode for ANY not-trivial task (3+ steps or architectural decisions)
- Use plan mode for verification steps, not just building
- Write detailed specs upfront to reduce ambiguity

### 2. Self-Improvement Loop
- After ANY correction from the user: update `tasks/lessons.md` with the pattern
- Write rules for yourself that prevent the same mistake
- Ruthlessly iterate on these lessons until the mistake rate drops
- Review lessons at session start for a project

### 3. Verification Before Done
- Never mark a task complete without proving it works
- Diff behavior between main and your changes when relevant
- Ask yourself: "Would a staff engineer approve this?"
- Run tests, check logs, demonstrate correctness

### 4. Demand Elegance (Balanced)
- For non-trivial changes: pause and ask "is there a more elegant way?"
- If a fix feels hacky: "Knowing everything I know now, implement the elegant solution"
- Skip this for simple, obvious fixes. Don't overengineer
- Challenge your own work before presenting it

### 5. Skills usage
- Skills live at **user scope** in `~/.claude/skills/`, NOT in this repository
- Invoke the matching skill with the Skill tool BEFORE writing the code, not after:

  | Working on | Invoke |
  |---|---|
  | Spring Boot code | `spring-boot-patterns`, `spring-boot-engineer` |
  | Quarkus code | `quarkus-patterns`, `quarkus-engineer` |
  | Camel routes | `camel-sb-patterns` or `camel-quarkus-patterns` |
  | JPA / Hibernate | `jpa-patterns` |
  | Dockerfile, Compose | `docker-patterns` |
  | Kubernetes manifests | `kubernetes-patterns` |
  | CI pipeline | `circleci-patterns` |
  | Logging | `logging-patterns` |
  | REST contract | `api-contract-review` |
  | Refactoring | `clean-code`, `design-patterns` |
  | Before declaring Java work done | `java-code-review` |

- **Never choose a library, framework or test tool** before checking the relevant skill and
  `~/.claude/agents/java-architect.md`. "Fewer dependencies" or "more elegant" does not outrank a
  stated convention. If one genuinely should not apply, say so and get agreement first
- If you skip a skill that applies, say so explicitly in your reply - never skip silently

### 6. Subagents usage
- Agents live at **user scope** in `~/.claude/agents/`, NOT in this repository
- **This section is a standing authorization: spawn subagents without asking each time.** Some
  harness configurations tell Claude not to use the Agent tool unless the user requested it - this
  instruction IS that request, granted in advance for any project built from this template
- Use subagents liberally to keep the main context window clean
- For complex problems, throw more compute at it via subagents
- One task per subagent for focused execution on a given tech stack
- Exception: when the user is actively reviewing work in the conversation, prefer working in-context
  so the reasoning stays visible to them

## Core Principles
- **Simplicity First**: Make every change as simple as possible. Impact minimal code
- **No Laziness**: Find root causes. No temporary fixes. Senior developer standards

## Project General Instructions

- Always use the latest versions of dependencies.
- Always write Java code as either Jakarta EE, Quarkus or Spring Boot application.
- When in doubt, ask for confirmation whether Jakarta EE, Quarkus or Spring Boot is prefered.
- Always consider using Apache Camel integrated to Jakarta EE, Quarkus or Spring Boot when it makes sense.
- Always use Maven for dependency management.
- Always try to structure the Maven project with a parent POM and as many Maven modules as necessary.
- Always maximize the code sharing by including functionalities common to several module in a common module.
- Always create test cases for the generated code both positive and negative.
- Always prefer integration tests, using testcontainers, to mocking based unit ones.
- Always generate the CircleCI pipeline in the .circleci directory to verify the code.
- Minimize the amount of code generated.
- The Maven artifact name must be the same as the parent directory name.
- Use semantic versioning for the Maven project. Each time you generate a new version, bump the PATCH section of the version number.
- Use `fr.simplex-software.workshop` as the group ID for the Maven project and base Java package.
- Do not use the Lombok library.
- When the application consists in several services, generate the Docker Compose file to run them.
- Optionally, after confirmation, provide the required artifacts (YAML files, plugins, extensions, etc.) to run the final app on Minikube.
- For Spring Boot applications, systematically use Cloud Native Buildpack.
- For Quarkus applications, systematically use Quarkus quarkus-container-image-docker or / and quarkus-minikube extensions.
- Update README.md each time you generate a new version.
- Keep git commit/push messages short: a one-line subject followed by the `Co-Authored-By` and `Claude-Session` trailers. Do not write a multi-paragraph body; put detailed rationale in the code, README or lessons.md instead.
