---
authors:
- "ernail"

date: 2025-08-21
---

# Stop Tracking Version Numbers in Git

I still see a lot of projects that maintain their version number in one or multiple files.
In my opinion, this provides absolutely no benefit.
You only get the additional work of updating the version with every release (or forgetting to).

> But the tooling I use requires setting the version in files checked into git
> (e.g. `package.json` for Node.js, `pyproject.toml` for Python, or `Chart.yaml` for Helm)

This is correct. And I'm not saying that the version should not be set in these files.
I'm saying there is no need to maintain the version in git.
Instead, it should be set before or during the build.
Because in the end, the version is only relevant for the package/artifact you are publishing.

<!-- more -->

Let's take Node.js with `npm` as an example.
In my `package.json`, I always set the version to `0.0.0`:

```json
{
  "name": "my-project",
  "version": "0.0.0"
}
```

In my CI/CD process, before the package is built, the following command will run:

```shell
npm --no-git-tag-version version "1.0.0"
```

This sets the version to `1.0.0` in the `package.json`.
But the change will not be committed to git.
It's only set in the CI/CD process, so the built package will contain the `package.json` with the correct version.

The same works for Helm Charts:

```shell
helm package my-chart --version "1.0.0"
```

Combine this with a CI/CD process that determines the next version number and generates the release notes
based on conventional commits,
creates a git tag, sets the version number in required files, publishes your packages/artifacts,
and creates something like a GitHub Release or GitLab Release,
and you'll never have to manually perform a release again.

As always in software engineering, there is no single truth.
Maybe you have valid reasons for having version-controlled version numbers in files.
But I would wager that in most cases, it is not needed.
