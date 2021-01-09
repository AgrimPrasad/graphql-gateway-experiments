# graphql-gateway-experiments

Experiments with GraphQL Gateway backed by RESTful APIs

We will use the `graphql-mesh` library which allows us to mesh together different OpenAPI (aka swagger) specs together using namespacing transforms. We can also implement GraphQL subscriptions by extending the generated stitched schema. Note that `graphql-mesh` can be used to combine not just `OpenAPI`, but also grpc, Postgres (PostGraphile) schemas etc.

## Setup

1. `yarn init` and setup `package.json`
2. Install `graphql` and `graphql-mesh` tools used to generate the graphql schema from the OpenAPI specs.

a. Install the `graphql-mesh` CLI

```bash
yarn add graphql @graphql-mesh/cli
```

b. Add the `OpenAPI` handler:

```bash
yarn add graphql @graphql-mesh/openapi
```

3. Test with converting a basic RESTful API to GraphQL. Add the following GraphQL Mesh Configuration file which tells GraphQL Mesh how to convert an OpenAPI spec to GraphQL schema. We are using the Wikipedia OpenAPI file as the source.

```yaml
sources:
  - name: Wiki
    handler:
      openapi:
        source: https://api.apis.guru/v2/specs/wikimedia.org/1.0.0/swagger.yaml
```

4. Run a local GraphQL server based on the generated schema

```bash
yarn graphql-mesh serve
```
