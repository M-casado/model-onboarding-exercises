# Exercise 3 - Validate through the API

## Goal

You will send a validation request straight to Biovalidator instead of using the browser page. An API is a URL that lets another program ask the server to do something.

We will use `curl` to send that request from your terminal, but you can use your preferred method (e.g., postman).

## Prerequisites

Start the Biovalidator server using the [workshop setup](../../README.md#setup).

## Instructions

1. Instead of interacting with the server through the UI like up until now, run the following request, which is similar to what the browser page does when you click **Validate**:

    ```bash
    curl --fail --silent --show-error \
      --request POST http://localhost:3020/validate \
      --header 'Content-Type: application/json' \
      --data '{
        "schema": {
          "$schema": "https://json-schema.org/draft/2020-12/schema",
          "type": "object",
          "required": ["name"],
          "properties": {"name": {"type": "string"}}
        },
        "data": {"name": "Rare disease cohort"}
      }' \
      --write-out '\nHTTP status: %{http_code}\n'
    ```

    Notice how the response is a simple ``[]`` (i.e., empty list), because the server's endpoing ``/validate`` did not find any errors. Whether the "request" was valid comes defined by the HTTP status code (e.g., ``200`` for a valid request) we print right after.

2. Run this second request with an invalid number for `name`:

    ```bash
    curl --fail --silent --show-error \
      --request POST http://localhost:3020/validate \
      --header 'Content-Type: application/json' \
      --data '{
        "schema": {
          "$schema": "https://json-schema.org/draft/2020-12/schema",
          "type": "object",
          "required": ["name"],
          "properties": {"name": {"type": "string"}}
        },
        "data": {"name": 12}
      }' \
      --write-out '\nHTTP status: %{http_code}\n'
    ```

    Notice how the returned list of errors is no longer empty.

## Questions

1. What does an empty list in the response mean?
2. How is "the data is invalid" different from "the request itself is broken"?
3. Why is the API useful when we have the [user-friendly UI](http://localhost:3020/) already?

> **In the real repository:** see the [Biovalidator `/validate` API documentation](https://github.com/EbiEga/biovalidator/blob/10dd3d688398813be2c2bcb57a779cea2c056a9b/docs/api.md#validation).

<details>
<summary>Solution</summary>

1. A response with status `200` means the request succeeded. If its body is `[]`, the data passed the rules.
2. A status `200` with an error list (``[ ... ]``) means the check finished and found problems. A broken request or a server/security problem returns another status (e.g., ``404``) instead of a normal validation result.
3. A direct request can be put in a script, called by another program, or repeated while investigating a result. The browser page is just one client of the same service.

</details>

## Concept summary

Browser pages are convenient when you are trying a check. An API lets your script or another program do the same check.

Both use the same request and response format. You can therefore move from trying things by hand to automating them without changing the rules.
