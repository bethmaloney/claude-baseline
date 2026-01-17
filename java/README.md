# Java Baseline

Claude Code permissions template for Java projects.

## Allowed Commands

| Command | Purpose |
|---------|---------|
| `java` | Run Java applications |
| `javac` | Java compiler |
| `javadoc` | Documentation generator |
| `jar` | Archive tool |
| `mvn` / `./mvnw` | Maven build tool |
| `gradle` / `./gradlew` | Gradle build tool |
| `ant` | Apache Ant build tool |
| `jshell` | Java REPL |
| `jdeps` | Dependency analyzer |
| `jlink` | Custom runtime image creator |
| `jpackage` | Native package creator |
| `checkstyle` | Code style checker |
| `spotbugs` | Static analysis for bugs |
| `pmd` | Source code analyzer |

## Denied Patterns

| Pattern | Reason |
|---------|--------|
| `.env` / `.env.*` | Environment variables with secrets |
| `secrets/**` / `**/secrets/**` | Explicit secrets directories |
| `~/.m2/settings.xml` | Maven settings with repository credentials |
| `~/.m2/settings-security.xml` | Maven encrypted credentials |
| `~/.gradle/gradle.properties` | Gradle properties with credentials |
| `gradle.properties` | Local Gradle properties may contain tokens |

## Usage

```bash
mkdir -p .claude
curl -o .claude/settings.json https://raw.githubusercontent.com/YOUR_USERNAME/claude-baseline/main/java/settings.json
```

## Customization Ideas

- Add `jbang` for scripting with Java
- Add `quarkus` for Quarkus CLI
- Add `spring` for Spring Boot CLI
- Add `micronaut` for Micronaut CLI
- Add `scala` / `sbt` for Scala projects
- Add `kotlin` / `kotlinc` for Kotlin projects
- Add `bazel` for Bazel build system
