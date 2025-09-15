# Noctis.FrontGraph.Sdk.Model.DomainerAsyncResultDTO
Results and status information for an asynchronous domain search request (similarity or free-text)

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**RequestId** | **Guid** | Unique identifier for the request | [readonly] 
**Limit** | **int** | Maximum number of results requested | [readonly] 
**CreatedAt** | **DateTime** | Time when the request was created | [readonly] 
**Status** | **string** | Request status | [readonly] 
**DomainName** | **string** | Domain name that was searched | [optional] [readonly] 
**SimilarityType** | **DomainerSimilarityType** |  | [optional] 
**QueryString** | **string** | Query string used for the search (only for SEARCH requests) | [optional] [readonly] 
**Operator** | **string** | Default operator used between query terms (only for SEARCH requests) | [optional] [readonly] 
**Level** | **string** | Absolute domain level filter applied (only for SEARCH requests) | [optional] [readonly] 
**CompletedAt** | **DateTime** | Time when the request was completed (null if still processing) | [optional] [readonly] 
**Results** | **List&lt;string&gt;** | List of similar domains found (null if still processing) | [optional] [readonly] 
**ResultCount** | **int** | Total number of results found | [optional] [readonly] 
**ProcessingTimeMs** | **long** | Time taken to process the request in milliseconds (-1 if still processing) | [optional] [readonly] 

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

