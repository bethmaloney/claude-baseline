# .NET Baseline

Claude Code permissions template for .NET/C# projects.

## Allowed Commands

| Command | Purpose |
|---------|---------|
| `dotnet restore` | Restore NuGet packages |
| `dotnet build` | Build the project |
| `dotnet test` | Run tests |
| `dotnet run` | Run the application |
| `dotnet watch` | Hot reload during development |
| `dotnet ef` | Entity Framework Core migrations |
| `dotnet format` | Code formatting |
| `dotnet clean` | Clean build outputs |
| `dotnet publish` | Publish for deployment |
| `dotnet add` | Add package or project references |
| `dotnet remove` | Remove package or project references |
| `dotnet list` | List project references or packages |
| `dotnet new` | Create new projects from templates |
| `dotnet tool` | Manage .NET CLI tools |
| `dotnet nuget` | NuGet package management |

## Denied Patterns

| Pattern | Reason |
|---------|--------|
| `appsettings.*.json` | Environment-specific config with connection strings |
| `appsettings.Development.json` | Development configuration (explicit) |
| `appsettings.Production.json` | Production configuration (explicit) |
| `**/appsettings.*.json` | Nested config files in multi-project solutions |
| `.env` / `.env.*` | Environment variables |
| `secrets/**` | Explicit secrets directory |
| `~/.microsoft/usersecrets/**` | .NET User Secrets storage location |

### Why not deny `appsettings.json`?

The base `appsettings.json` typically contains non-sensitive defaults and schema definitions. Secrets should be in environment-specific files (`appsettings.Development.json`) or User Secrets. If your project stores secrets in the base file, add it to your deny list.

## Usage

```bash
mkdir -p .claude
curl -o .claude/settings.json https://raw.githubusercontent.com/YOUR_USERNAME/claude-baseline/main/dotnet/settings.json
```

## Customization Ideas

- Add `dotnet user-secrets` if you need to manage User Secrets directly
- Add `dotnet sln` for solution file management
- Add `dotnet pack` for creating NuGet packages
- Add `dotnet migrate` for legacy project migration
