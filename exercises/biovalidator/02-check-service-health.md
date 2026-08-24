# Exercise 2 - Check service health

## Goal

You will see the health information that this Biovalidator process reports about itself.

## Prerequisites

- Start Biovalidator using the [setup instructions](../../README.md#setup).
- Open <http://localhost:3020>.

## Instructions

1. Open a browser and go to <http://localhost:3020/health>. You should see a JSON response.

2. In the response, find `status`, the Biovalidator version (e.g., `2.2.2`), its dependency versions (e.g., `node 26.7.0`), how long the process has been running (`uptime_seconds`), validation counts (`validation: ...`), and what is stored in memory (`"cache": ...`) to speed up validation requests.

## Questions

1. In general, what can `/health` tell you about this running Biovalidator server?
2. Does a successful `/health` response prove that [OLS](https://www.ebi.ac.uk/ols4/) is available?
3. Why should you not treat these counts and times as totals for _every_ Biovalidator server?

> **In the real repository:** see the [Biovalidator health endpoint rules](https://github.com/EbiEga/biovalidator/blob/main/docs/api.md#health).

<details>
<summary>Solution</summary>

1. It reports whether this process is running and some useful information for both maintainers and consumers that may rely on it.
2. No. `/health` does not contact OLS, ENA Taxonomy, identifiers.org, or other outside services to check if they are up and running.
3. The numbers belong only to this process and reset when it restarts. They are not combined with numbers from other copies of the server.

</details>

## Concept summary

A health endpoint is a URL that returns a quick report with a defined set of fields. “The server answered” does not necessarily mean that every service it uses is ready.

Check what the endpoint actually tests before you rely on it. You can take a look at the [external Continuous Integration (CI) tests](https://github.com/EbiEga/biovalidator/actions/workflows/external-integration.yml) run in EGA's Biovalidator repository to have a better idea of the status of third-party services.
