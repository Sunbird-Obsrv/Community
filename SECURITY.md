# Security Policy

## Reporting a vulnerability

**Please do not report security vulnerabilities through public GitHub issues, discussion threads, or the Discord channel.** A public report tells everyone about the weakness before there is a fix available.

Report vulnerabilities privately using GitHub's **"Report a vulnerability"** button, under the **Security** tab of the affected repository. This opens a private advisory visible only to you and the maintainers.

Include as much as you can:

* The component affected and the version or commit you tested against
* What an attacker could do with the issue
* Steps to reproduce it, including configuration or sample data where relevant
* Any logs, stack traces or proof-of-concept code

You do not need a working exploit to report something. If you think a behaviour looks wrong, tell us.

## What happens next

| When | What |
| --- | --- |
| Within 3 working days | We acknowledge your report |
| Within 10 working days | We confirm whether we can reproduce it and give you an initial assessment |
| Thereafter | We keep you updated at least every 2 weeks until it is resolved |

Once a fix is ready we publish it as a release and note the issue in the release notes. We will credit you by name unless you ask us not to.

We ask that you give us a reasonable chance to fix the issue before describing it publicly.

## Supported versions

Security fixes are applied to the latest released version of each component. If you are running an older version, the fix will be to upgrade.

See the [release notes](https://obsrv.sunbird.org/release-notes) for the current versions.

## Scope

This policy covers the Obsrv components published under the [Sunbird-Obsrv organisation](https://github.com/orgs/Sunbird-Obsrv/repositories).

Obsrv is deployed into infrastructure that you operate. Vulnerabilities in the underlying components Obsrv builds on — Apache Kafka, Flink, Spark, Druid, PostgreSQL and the rest — should go to those projects directly. If you are not sure which applies, report it to us and we will route it.

The published version lives at <https://obsrv.sunbird.org/engage/security>.
