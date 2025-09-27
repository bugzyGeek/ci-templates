# ci-templates

A collection of reusable GitHub Actions workflows for common CI/CD tasks.

## Available Workflows

### 🚀 NuGet Publish Workflow

A comprehensive reusable workflow for building, testing, and publishing .NET packages to NuGet.

**Location:** `.github/workflows/nuget-publish.yml`

**Quick Usage:**
```yaml
jobs:
  publish:
    uses: bugzyGeek/ci-templates/.github/workflows/nuget-publish.yml@main
    secrets:
      nuget-api-key: ${{ secrets.NUGET_API_KEY }}
```

[📖 Full Documentation](.github/workflows/README.md)

## Features

- ✅ Supports multiple .NET versions
- ✅ Automatic project detection
- ✅ Build and test validation
- ✅ Configurable parameters
- ✅ Dry run support
- ✅ Artifact uploads
- ✅ Detailed summaries

## Getting Started

1. Add the required secrets to your repository (e.g., `NUGET_API_KEY`)
2. Create a workflow file in your project that references these templates
3. Customize the parameters as needed

See the individual workflow documentation for detailed usage instructions.