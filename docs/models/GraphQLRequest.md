# Whisper.Api.Sdk.Model.GraphQLRequest
Request to execute a GraphQL query against the graph database.  Follows the standard GraphQL over HTTP specification.  **Available Query Operations:** - `domain(name: String!)` - Look up domain information - `ipv4(address: String!)` - Look up IPv4 address information - `ipv6(address: String!)` - Look up IPv6 address information - `asn(number: Int!)` - Look up ASN information - `searchDomains(pattern: String!, limit: Int)` - Search domains by pattern - `domainsOnIP(address: String!)` - Find domains on an IP - `domainsOnASN(asnNumber: Int!, limit: Int)` - Find domains on an ASN - `checkIndicator(indicator: String!)` - Check if indicator is listed  **Example Query:** ```graphql query GetDomainInfo($domain: String!) {   domain(name: $domain) {     name     ipAddresses {       address       country { code }     }     nameservers { name }     asns { number }   } } ``` 

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Query** | **string** | The GraphQL query or mutation to execute | 
**OperationName** | **string** | Name of the operation to execute (for documents with multiple operations) | [optional] 
**Variables** | **Dictionary&lt;string, Object&gt;** | Variables to pass to the query as key-value pairs | [optional] 

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

