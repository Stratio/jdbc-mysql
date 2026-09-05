# jdbc-mysql — Agent Instructions

Packages the **MySQL JDBC driver** into a single fat JAR, with the driver version baked into the
qualified class names so **several driver versions can coexist on one classpath** (artifact
`com.stratio.connectors:mysql-jdbc-<version>`). CI builds on
`stratio/connectors-maven-builder-openjdk-8`.

## Scope — the shared harness barely applies here

The connectors team harness (`connectors-internal-docs/agents/CLAUDE.md`) is written for the Scala
`sscc-*` connectors: SDK parent POM, ScalaTest suites, scoverage floors, connector test environments.
**None of that is about this repo** — do not go looking for it here.

What does apply is the git and GitHub conventions: remote setup (`origin` = your fork, `upstream` =
`Stratio/jdbc-mysql`), branch naming, the `[TICKET-ID] type: description` commit format, and how PRs are
opened and merged. Those live in the harness under the `connectors-dev:git-conventions` skill. Read it
from `../connectors-internal-docs/agents/CLAUDE.md` if the sibling checkout is there, otherwise:

```bash
H=/tmp/connectors-agents; mkdir -p "$H"
TOK="${GITHUB_TOKEN:-${GH_TOKEN:-}}"
[ -z "$TOK" ] && [ -f ~/credentials/github.sh ] && { . ~/credentials/github.sh; TOK="$ACTION_USER_TOKEN"; }
[ -z "$TOK" ] && command -v gh >/dev/null 2>&1 && TOK=$(gh auth token)
curl -fsSL -H "Authorization: Bearer $TOK" -H "Accept: application/vnd.github.raw" \
  https://api.github.com/repos/Stratio/connectors-internal-docs/contents/agents/CLAUDE.md \
  -o "$H/CLAUDE.md"
```

Plain `curl`, no `gh` binary needed. `connectors-internal-docs` is **private**, so a token is required —
`$GITHUB_TOKEN`/`$GH_TOKEN`, `~/credentials/github.sh`, or `gh auth token` where `gh` happens to be
installed.

## Specific to this repo

- **The version-in-the-class-name is the whole point.** The shade plugin relocates `com.mysql` into a
  package carrying the driver version, which is what lets two MySQL drivers load side by side. Do not
  "simplify" the relocation away — that is the feature, and `sscc-mysql` depends on it to test 5.x and
  8.x in the same reactor.
- Because the class names move, a consumer cannot hardcode `com.mysql.cj.jdbc.Driver`; it registers the
  relocated name. Check the README before changing anything about registration.
- Like `jdbc-hive`, the repo keeps **one release branch per driver version** (`branch-8.3.0-1.0`,
  `branch-5.1.49-1.0`, …) — check which branch a change belongs on before starting.
- All dependencies ship inside the JAR.

Consumer: the `sscc-mysql` connector. A change here can break it, and nothing in this repo's CI will
tell you.

*Last Updated: 2026-09-05*
