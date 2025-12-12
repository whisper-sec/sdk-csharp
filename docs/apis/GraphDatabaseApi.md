# Whisper.Api.Sdk.Api.GraphDatabaseApi

All URIs are relative to *https://api.whisper.security*

| Method | HTTP request | Description |
|--------|--------------|-------------|
| [**ExecuteCypherQuery**](GraphDatabaseApi.md#executecypherquery) | **POST** /v1/ops/graph/cypher | Execute Cypher Query |
| [**ExecuteGraphQL**](GraphDatabaseApi.md#executegraphql) | **POST** /v1/ops/graph/graphql | Execute GraphQL Query |
| [**GetGraphiQL**](GraphDatabaseApi.md#getgraphiql) | **GET** /v1/ops/graph/graphiql | GraphiQL Interactive Explorer |
| [**GetHealth**](GraphDatabaseApi.md#gethealth) | **GET** /v1/ops/graph/health | Graph Database Health Check |
| [**GetSchema**](GraphDatabaseApi.md#getschema) | **GET** /v1/ops/graph/schema | Get Graph Schema |

<a id="executecypherquery"></a>
# **ExecuteCypherQuery**
> CypherQueryResponse ExecuteCypherQuery (string authorization, CypherQueryRequest cypherQueryRequest)

Execute Cypher Query

Execute a read-only Cypher query against the FalkorDB graph database.  **Security:** Only read operations (MATCH, RETURN) are allowed. Write operations are blocked.  **Example Queries:** ```cypher // Find all IPs for a domain MATCH (d:DomainName {name: $domain})-[:hasIP]->(ip:A_ADDRESS) RETURN ip.name AS ip  // Find domains on blocklists MATCH (d:DomainName)-[:isListed]->(l:LIST) RETURN d.name, l.name LIMIT 10  // Get ASN and announced prefixes MATCH (asn:ASN {number: 15169})-[:announces]->(p:ANNOUNCED_PREFIX_4) RETURN p.name AS prefix ```  **Performance Tips:** - Always use LIMIT to restrict result size - Use parameters for variable values - Filter early in the query with WHERE clauses 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **authorization** | **string** |  |  |
| **cypherQueryRequest** | [**CypherQueryRequest**](CypherQueryRequest.md) |  |  |

### Return type

[**CypherQueryResponse**](CypherQueryResponse.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Query executed successfully |  -  |
| **400** | Invalid query syntax |  -  |
| **401** | Authentication required |  -  |
| **500** | Query execution failed |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="executegraphql"></a>
# **ExecuteGraphQL**
> void ExecuteGraphQL (string authorization, GraphQLRequest graphQLRequest)

Execute GraphQL Query

Execute a GraphQL query against the graph database.  GraphQL provides a type-safe, structured alternative to Cypher for querying the graph data.  **Available Query Operations:** - `domain(name: String!)` - Look up domain information - `ipv4(address: String!)` - Look up IPv4 address information - `ipv6(address: String!)` - Look up IPv6 address information - `asn(number: Int!)` - Look up ASN information - `searchDomains(pattern: String!, limit: Int)` - Search domains by pattern - `domainsOnIP(address: String!)` - Find domains on an IP - `domainsOnASN(asnNumber: Int!, limit: Int)` - Find domains on an ASN - `checkIndicator(indicator: String!)` - Check if indicator is listed  **Example Query:** ```graphql {   domain(name: \"google.com\") {     name     ipAddresses {       address       country { code }     }     nameservers { name }     asns { number }   } } ```  Use the `/v1/ops/graph/graphiql` endpoint for an interactive query explorer with schema documentation. 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **authorization** | **string** |  |  |
| **graphQLRequest** | [**GraphQLRequest**](GraphQLRequest.md) |  |  |

### Return type

void (empty response body)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Query executed successfully |  -  |
| **400** | Invalid query syntax |  -  |
| **401** | Authentication required |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="getgraphiql"></a>
# **GetGraphiQL**
> void GetGraphiQL ()

GraphiQL Interactive Explorer

Access the GraphiQL interactive query explorer.  GraphiQL provides: - Interactive query editor with syntax highlighting - Auto-complete for types and fields - Schema documentation browser - Query history  **No authentication required** - the UI itself is public, but queries still require a valid API key. 


### Parameters
This endpoint does not need any parameter.
### Return type

void (empty response body)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: text/html


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | GraphiQL HTML page |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="gethealth"></a>
# **GetHealth**
> Object GetHealth ()

Graph Database Health Check

Check the health and connectivity of the graph database.  **No authentication required** - this is a public health endpoint.  Returns database status, connection info, and basic statistics. 


### Parameters
This endpoint does not need any parameter.
### Return type

**Object**

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: */*


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Health status retrieved |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="getschema"></a>
# **GetSchema**
> CypherSchemaResponse GetSchema (string authorization)

Get Graph Schema

Retrieve the graph database schema including available node labels, relationship types, and their properties.  Use this to discover what data is available for querying before writing Cypher or GraphQL queries.  **Response includes:** - Node labels (e.g., DomainName, A_ADDRESS, ASN) - Relationship types (e.g., hasIP, isListed, announces) - Properties available on each node and relationship type - Graph statistics (node and relationship counts) 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **authorization** | **string** |  |  |

### Return type

[**CypherSchemaResponse**](CypherSchemaResponse.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Schema retrieved successfully |  -  |
| **401** | Authentication required |  -  |
| **500** | Failed to retrieve schema |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

