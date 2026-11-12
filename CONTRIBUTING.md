# Contributing to Obsrv

Contributions take many forms. Answering a question in the forum, reporting a bug, improving the documentation and writing code all help.

Everyone taking part is expected to follow our [Code of Conduct](CODE_OF_CONDUCT.md).

## Where things happen

Questions, ideas and installation problems go to the [discussion forum](https://github.com/orgs/Sunbird-Obsrv/discussions). Agreed work is tracked in [Jira under project OB](https://project-sunbird.atlassian.net/jira/software/c/projects/OB/issues). For quick questions there is [Discord](https://discord.gg/Q5mvw2mGC8), and the documentation is at [obsrv.sunbird.org](https://obsrv.sunbird.org).

## Before you start

1. Search the [forum](https://github.com/orgs/Sunbird-Obsrv/discussions) and the [issue tracker](https://project-sunbird.atlassian.net/jira/software/c/projects/OB/issues) so you are not duplicating work already under way.
2. Check that it still happens on the latest version. See the [release notes](https://obsrv.sunbird.org/release-notes).
3. Raise what you have found in the forum and reach agreement with the community before it becomes a tracked issue. This applies to bugs, documentation gaps, installation problems, new features and enhancements.

Full detail on the issue workflow is in the pinned [Raise an Issue](https://github.com/orgs/Sunbird-Obsrv/discussions/14) post.

## Making a change

1. Fork the repository and clone your fork.
2. Create a branch for your change.
3. Make the change, and add or update tests where the project has them.
4. Open a pull request against `main`, describing what you changed and why, and linking the discussion or Jira issue.

The [Developer Guide](https://obsrv.sunbird.org/guides/developer-guide) has setup instructions for each repository, covering prerequisites, build commands, and how to produce and publish container images.

If you are building a connector, start with the [Connectors Developer Guide](https://obsrv.sunbird.org/guides/connectors-developer-guide).

## Contributing documentation

The documentation site is built from this repository and published to [obsrv.sunbird.org](https://obsrv.sunbird.org). Edit the relevant Markdown file, add the page to `SUMMARY.md` if it is new, and open a pull request.

## Reporting a security vulnerability

Do not use public issues or the forum. Follow the [Security Policy](SECURITY.md).

## Who reviews your work

The [Obsrv Working Group](https://github.com/orgs/Sunbird-Obsrv/discussions/27) reviews and accepts pull requests. You can reach them by tagging `@Sunbird-Obsrv/sunbirdobsrv_workinggroup` in a discussion thread.
