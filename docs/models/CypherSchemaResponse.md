# Whisper.Api.Sdk.Model.CypherSchemaResponse
Graph database schema information including available node types, relationship types, and their properties.  Use this to discover what data is available for querying. 

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**NodeLabels** | **List&lt;string&gt;** | Available node labels in the graph.  Common node types: - &#x60;DomainName&#x60;: Domain names (e.g., google.com) - &#x60;A_ADDRESS&#x60;: IPv4 addresses - &#x60;AAAA_ADDRESS&#x60;: IPv6 addresses - &#x60;ASN&#x60;: Autonomous System Numbers - &#x60;ANNOUNCED_PREFIX_4&#x60;: IPv4 prefixes announced via BGP - &#x60;ANNOUNCED_PREFIX_6&#x60;: IPv6 prefixes announced via BGP - &#x60;Organisation&#x60;: Organizations owning ASNs - &#x60;Country&#x60;: Country information - &#x60;LIST&#x60;: Blocklist/whitelist entries - &#x60;LISTCATEGORY&#x60;: Categories of lists - &#x60;TLD&#x60;: Top-level domains - &#x60;TLSCA&#x60;: TLS Certificate Authorities - &#x60;TLSCert&#x60;: TLS Certificates  | [optional] 
**RelationshipTypes** | **List&lt;string&gt;** | Available relationship types in the graph.  Common relationships: - &#x60;hasIP&#x60;: Domain → A_ADDRESS (DNS A record) - &#x60;hasIPv6&#x60;: Domain → AAAA_ADDRESS (DNS AAAA record) - &#x60;hasNameserver&#x60;: Domain → DomainName (NS record) - &#x60;hasMailHost&#x60;: Domain → DomainName (MX record) - &#x60;hasTLD&#x60;: Domain → TLD - &#x60;announces&#x60;: ASN → ANNOUNCED_PREFIX - &#x60;inASN&#x60;: IP_PREFIX → ASN - &#x60;isListed&#x60;: IP/Domain → LIST (blocklist membership) - &#x60;hasCA&#x60;: TLSCert → TLSCA - &#x60;isIssuer&#x60;: TLSCA → TLSCert - &#x60;isSubjectOf&#x60;: DomainName → TLSCert  | [optional] 
**NodeProperties** | **Dictionary&lt;string, List&lt;string&gt;&gt;** | Properties available on each node type, keyed by node label | [optional] 
**RelationshipProperties** | **Dictionary&lt;string, List&lt;string&gt;&gt;** | Properties available on each relationship type, keyed by relationship type | [optional] 
**NodeCount** | **long** | Total number of nodes in the graph | [optional] 
**RelationshipCount** | **long** | Total number of relationships in the graph | [optional] 

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

