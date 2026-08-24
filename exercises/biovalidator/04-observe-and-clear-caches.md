# Exercise 4 - Observe and clear caches

## Goal

You will see how Biovalidator saves built validators, downloaded `$ref` files, and answers from online services.

## Prerequisites

- Start a fresh Biovalidator server using the [setup instructions](../../README.md#setup).
- Ensure access to GitHub and OLS.

## Safety

Use `DELETE /cache` **only on a server you own** (i.e., one you have deployed yourself). A public server may turn these routes off and return `404`.

## Instructions

1. [Deploy Biovalidator](../../README.md#setup). It is important to start a fresh server, so that the exercise is deterministic.

2. Open <http://localhost:3020/cache> and check if there are any references stored in cache (_hint: look at ``referenced`` or ``urls``, are they empty?_). 

   Keep the tab open, to compare later on.

3. In [Biovalidator](http://localhost:3020/), choose **Fetch examples**, select `DAC-valid-minimal.json`, and choose **Load example**. Then click on **validate**.

4. Once validation ends, open <http://localhost:3020/cache> again and check if something changed because of your validation request to the server.

   Why is Biovalidator keeping track of the reference schemas?

5. In a different terminal, clear only the temporary saved schema data:

   ```bash
   curl --fail --silent --show-error --request DELETE \
   'http://localhost:3020/cache?scope=schemas'
   ```
6. Open the `/cache` endpoint again, and notice what your command did to the server's memory.

   Keep the tab open, to compare later on.

7. Go back to [Biovalidator's UI](http://localhost:3020/), choose the example `biomaterial-valid-minimal-organism.json`, **Load example** and then **Validate**.

   Notice the time it takes for the validation to appear. If, after it is finished, you click on **Validate** again, it is much faster, is it not?

8. Open the `/cache` endpoint again, and compare the content of `api.entries.ols` (search for ``ols`` with ``Ctrl+F``).

   Why are there OLS entries now? Why were there none after validating the DAC example?

9. Similar to above, remove the cache, this time with the scope of API calls, instead of the schemas:

   ```bash
   curl --fail --silent --show-error --request DELETE \
     'http://localhost:3020/cache?scope=api'
   ```

10. See the `/cache` content again and notice how the schema entries remain, but the API data was erased.

## Questions

1. What does it mean that information is retained in _cache_?
2. What happens when you repeat a validation request while its saved data (e.g., OLS API calls and GitHub schemas) are cached?
3. In what scenarios would we want to erase the cache of the Biovalidator server, as opposed to just deploying it again?

> **In the real repository:** see the [cache endpoint rules](https://github.com/EbiEga/biovalidator/blob/main/docs/api.md#cache) and the [Biovalidator cache README section](https://github.com/EbiEga/biovalidator/blob/main/README.md#interacting-with-biovalidator-cache).

<details>
<summary>Solution</summary>

1. Information retained in cache means that previously downloaded schemas, built validators, and API responses are stored in server memory, so they don't need to be fetched or computed again.

2. When you repeat a validation request with cached data, the validation completes much faster because Biovalidator reuses the saved schemas and API responses instead of downloading and processing them again.

3. You would want to erase the cache when you need to refresh outdated information (e.g., if a referenced schema was updated on GitHub or a used ontology like EFO released a new update), when you want to free up server memory for other tasks, or when troubleshooting issues related to stale cached data, **without** needing to restart the entire server.

</details>

## Concept summary

Caching means saving work so you do not have to repeat it. Biovalidator can save downloaded rules and the validator it built from them.

Answers from an outside ontology/API service are saved separately.
