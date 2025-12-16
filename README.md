# Probitas CLI

Command-line interface for
[Probitas](https://github.com/jsr-probitas/probitas) - a scenario-based testing
& workflow execution framework.

## Installation

```bash
curl -fsSL https://raw.githubusercontent.com/jsr-probitas/cli/main/install.sh | bash
```

Options via environment variables:

```bash
# Install specific version
curl -fsSL https://raw.githubusercontent.com/jsr-probitas/cli/main/install.sh | PROBITAS_VERSION=0.7.1 bash

# Install to custom directory
curl -fsSL https://raw.githubusercontent.com/jsr-probitas/cli/main/install.sh | PROBITAS_INSTALL_DIR=/usr/local/bin bash
```

## Usage

```bash
# Run all scenarios
probitas run

# Run scenarios with specific tag
probitas run -s tag:example

# Run with JSON reporter
probitas run --reporter json

# List scenarios without running
probitas list

# Show help
probitas --help
```

## Commands

### `probitas run [paths...] [options]`

Execute scenario files and report results.

**Options:**

- `--select, -s <pattern>` - Filter scenarios by selector (can repeat)
- `--reporter, -r <type>` - Output format: list, json (default: list)
- `--concurrency, -c <n>` - Max parallel scenarios (0 = unlimited)
- `--max-failures, -f <n>` - Stop after N failures (0 = continue all)
- `--log-level, -l <level>` - Log verbosity: fatal, warning, info, debug
- `--include <glob>` - Include files matching pattern
- `--exclude <glob>` - Exclude files matching pattern
- `--timeout <duration>` - Scenario timeout (e.g., "30s", "5m")

### `probitas list [paths...] [options]`

List discovered scenarios without running them.

**Options:**

- `--select, -s <pattern>` - Filter scenarios by selector
- `--json` - Output as JSON

## Selectors

Selectors filter scenarios by name or tags:

- `login` - Match scenarios with "login" in name
- `tag:api` - Match scenarios tagged with "api"
- `!tag:slow` - Exclude scenarios tagged with "slow"
- `tag:api,tag:critical` - Match both tags (AND)
- Multiple `-s` flags combine with OR logic

## Exit Codes

- `0` - Success (all scenarios passed)
- `1` - Failure (one or more scenarios failed)
- `2` - Usage error (invalid arguments)
- `4` - No scenarios found

## Configuration

Create a `probitas.json` file in your project root:

```json
{
  "includes": ["probitas/**/*.probitas.ts"],
  "excludes": ["**/*.skip.probitas.ts"],
  "reporter": "list",
  "maxConcurrency": 4,
  "timeout": "30s",
  "selectors": ["!tag:wip"]
}
```

## Development

```bash
# Run tests
deno task test

# Run all checks
deno task verify
```

## License

See [LICENSE](LICENSE) file for details.
