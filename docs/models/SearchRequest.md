# Whisper.Api.Sdk.Model.SearchRequest
Search query for finding indicators matching specific criteria. Powerful for threat hunting and infrastructure discovery.

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Query** | **string** | Search query using field:value syntax. Supports multiple fields combined with logical operators.  **Supported Fields:** - WHOIS: &#x60;registrantCompany&#x60;, &#x60;registrantName&#x60;, &#x60;registrantEmail&#x60;, &#x60;registrar&#x60; - Network: &#x60;asn&#x60;, &#x60;network&#x60;, &#x60;country_code&#x60;, &#x60;city&#x60; - Domain: &#x60;tld&#x60;, &#x60;domain_length&#x60;, &#x60;creation_date&#x60;  **Examples:** - &#x60;registrantCompany:EvilCorp&#x60; - Find domains by registrant - &#x60;asn:15169 AND country_code:US&#x60; - Complex query with AND - &#x60;registrantEmail:admin@example.com&#x60; - Find domains by email  | 
**Filters** | **Dictionary&lt;string, string&gt;** | Additional filters to narrow down search results. Applied after query matching. | [optional] 
**Limit** | **int** | Maximum number of results to return per page | [optional] [default to 100]
**Offset** | **int** | Number of results to skip for pagination. Use with limit for paginated results. | [optional] [default to 0]
**SortBy** | **string** | Field to sort results by | [optional] 
**SortOrder** | **string** | Sort order | [optional] [default to SortOrderEnum.Asc]

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

