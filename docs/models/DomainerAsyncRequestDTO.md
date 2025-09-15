# Noctis.FrontGraph.Sdk.Model.DomainerAsyncRequestDTO
Parameters for an asynchronous domain search (either similarity or free-text)

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**CallbackUrl** | **string** | URL to call with results when the search is complete (must be accessible from the server) | 
**DomainName** | **string** | (Required for SIMILARITY requests) Domain name to search for similar domains | [optional] 
**SimilarityType** | **string** | (Required for SIMILARITY requests) Type of similarity to use: CONTAINS, SOUNDING, PREFIX, SUFFIX, TYPO, UTFVARS | [optional] 
**QueryString** | **string** | (Required for SEARCH requests) Query string (supports standard query syntax) | [optional] 
**Operator** | **string** | (Optional for SEARCH requests) Default operator between query terms if not specified | [optional] [default to OperatorEnum.AND]
**Level** | **string** | (Optional for SEARCH requests) Filter results by absolute domain level (dot count) | [optional] [default to LevelEnum.ALL]
**FindAvailable** | **bool** | Set to true to find AVAILABLE similar domains (typo/sounding) instead of existing ones. Requires domainName, ignores similarityType/queryString/operator/level. | [optional] [default to false]
**Limit** | **int** | Maximum number of results to return (use a reasonable limit to prevent excessive processing) | [optional] [default to 100]

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

