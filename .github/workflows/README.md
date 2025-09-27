# NuGet Publish Workflow

This directory contains a reusable GitHub Actions workflow for publishing .NET packages to NuGet.

## Usage

To use this workflow in your repository, create a workflow file (e.g., `.github/workflows/publish.yml`) in your project:

```yaml
name: Publish NuGet Package

on:
  release:
    types: [published]
  workflow_dispatch:
    inputs:
      dry-run:
        description: 'Perform a dry run without actually publishing'
        required: false
        type: boolean
        default: false

jobs:
  publish:
    uses: bugzyGeek/ci-templates/.github/workflows/nuget-publish.yml@main
    with:
      project-path: './src/MyProject'  # Path to your project
      dotnet-version: '8.0.x'         # .NET version
      configuration: 'Release'        # Build configuration
      package-version: ${{ github.event.release.tag_name || inputs.package-version }}
      dry-run: ${{ inputs.dry-run || false }}
    secrets:
      nuget-api-key: ${{ secrets.NUGET_API_KEY }}
```

## Input Parameters

| Parameter | Required | Default | Description |
|-----------|----------|---------|-------------|
| `project-path` | No | `'.'` | Path to the project or solution file |
| `dotnet-version` | No | `'8.0.x'` | .NET version to use |
| `configuration` | No | `'Release'` | Build configuration (Debug/Release) |
| `nuget-source` | No | `'https://api.nuget.org/v3/index.json'` | NuGet source URL |
| `package-version` | No | (project version) | Override package version |
| `skip-tests` | No | `false` | Skip running tests before publishing |
| `dry-run` | No | `false` | Perform a dry run without publishing |

## Required Secrets

| Secret | Description |
|--------|-------------|
| `nuget-api-key` | Your NuGet API key for publishing packages |

## Outputs

| Output | Description |
|--------|-------------|
| `package-name` | Name of the published package |
| `package-version` | Version of the published package |

## Features

- ✅ Builds and tests your .NET project
- ✅ Automatically detects package information
- ✅ Supports custom package versions
- ✅ Dry run mode for testing
- ✅ Uploads packages as artifacts
- ✅ Provides detailed summary output
- ✅ Supports both .csproj and .fsproj files
- ✅ Handles multiple packages in a solution

## Examples

### Basic Usage
```yaml
jobs:
  publish:
    uses: bugzyGeek/ci-templates/.github/workflows/nuget-publish.yml@main
    secrets:
      nuget-api-key: ${{ secrets.NUGET_API_KEY }}
```

### Advanced Usage with Custom Settings
```yaml
jobs:
  publish:
    uses: bugzyGeek/ci-templates/.github/workflows/nuget-publish.yml@main
    with:
      project-path: './src/MyLibrary/MyLibrary.csproj'
      dotnet-version: '6.0.x'
      configuration: 'Release'
      package-version: '1.2.3-preview'
      nuget-source: 'https://nuget.pkg.github.com/myorg/index.json'
      skip-tests: false
      dry-run: false
    secrets:
      nuget-api-key: ${{ secrets.GITHUB_TOKEN }}
```

### Dry Run for Testing
```yaml
jobs:
  test-publish:
    uses: bugzyGeek/ci-templates/.github/workflows/nuget-publish.yml@main
    with:
      dry-run: true
    secrets:
      nuget-api-key: ${{ secrets.NUGET_API_KEY }}
```