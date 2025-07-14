# AutoMerge

**AutoMerge** is a CLI tool to automate merging multiple remote Git branches into a temporary branch, tagging that branch with an environment-specific tag, pushing the tag to origin, and cleaning up afterward.

---

## Features

- Reads configuration from a YAML file defining multiple environments
- Supports wildcard patterns for included remote branches to merge
- Creates a temporary branch from a base branch before merging
- Tags the merge commit with an environment name and timestamp
- Pushes the tag to the remote repository
- Automatically cleans up the temporary branch and local tag
- Supports optional customizable tag prefix per environment

---

## Installation

Install via Composer:

```bash
composer require your-vendor/automerge
```

## Usage

```bash
vendor/bin/automerge
```

## Configuration Example (config.yaml)

Create a config.yaml file in your project root with this structure:
```yaml
staging:
  base: main
  branches:
    - "bugfix/*"
  tag_prefix: "prod-"      # Optional; Default is "automerge-" if empty or false, no prefix used

feature:
  base: develop
  branches:
    - "feature/*"
  tag_prefix: false # omitted here; no prefix will be used
```


## The script will:

- Check your working directory is clean.
- Fetch all remote branches.
- Create a temporary branch from the base branch.
- Merge all matching remote branches.
- Tag the commit with a timestamp and environment name.
- Push the tag to the remote.
- Clean up local temporary branch and tag, and restore your original branch.