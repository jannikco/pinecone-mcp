# Pinecone MCP server

List available indexes and inspect a selected index’s host and readiness before connecting a data-plane application. No index creation or destructive operation is exposed.

A direct-provider MCP server with useful local execution. No PipMCP account is required for local use. Provider API access and any provider charges are your responsibility.

## Quick start

Requires Node.js22+. Clone this repository, then run:

```sh
npm ci --ignore-scripts
npm test
npm start
```

The default command inspects the tools offline. Configure your own credentials in your environment:

- `PINECONE_API_KEY`



Credential help: https://docs.pinecone.io/reference/api/2025-10/control-plane/list_indexes

## Execute a real read

Replace example record IDs with records you are authorized to access.

```sh
npm start -- --call list_indexes '{}'
```

## Use with an MCP client

Launch `node /absolute/path/pinecone-mcp/server.mjs` using stdio transport; pass credentials through the client environment. Stdout is reserved for JSON-RPC.

## Tools

| Tool | Effect | Purpose |
| --- | --- | --- |
| list_indexes | Read | List indexes visible to the key’s project using the pinned control-plane API version. |
| describe_index | Read | Inspect index host, dimension and readiness metadata before configuring a separate data-plane client. |

## Concrete workflow

List available indexes and inspect a selected index’s host and readiness before connecting a data-plane application. No index creation or destructive operation is exposed.

1. list_indexes
2. describe_index

## Optional writes

Writes are disabled by default. Set CONNECTOR_ALLOW_WRITES=true and supply `_approval: {approved:true,idempotencyKey:"unique-request-id"}` on the specific call. Do not reuse a key for a different request. Uncertain outcomes are never automatically replayed; inspect the provider before another attempt.

## Capability evidence

Local: **Tested — HTTP fixtures and real stdio tools/call**. Managed: **Documented**. Provider authentication and live operations have not been established by these fixture tests. Evidence applies per operation and execution mode; setup discovery does not imply provider execution.

## Managed production

[Activate with PipMCP](https://pipmcp.com/github/start?app=pinecone&integration=pinecone-mcp&utm_source=github&utm_campaign=github-pinecone-mcp&utm_content=readme) when you want the hosted service.  Local credentials are not uploaded by this code. Review provider permissions in the managed onboarding. [Directory and related projects](https://jannikco.github.io/pipmcp-connectors/integrations/pinecone/).

## Provenance and maintenance

- https://docs.pinecone.io/reference/api/2025-10/control-plane/list_indexes
- https://docs.pinecone.io/reference/api/2025-10/control-plane/describe_index

Maintainer:jannikco. MIT license for this code. See connector.json for selected operations and integration.json for evidence. Runtime dependencies retain their own licenses. Report sensitive issues through https://pipmcp.com/contact; do not post credentials or customer data in public issues.
