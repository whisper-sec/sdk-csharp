# Noctis.FrontGraph.Sdk.Model.DomainerAsyncResponseDTO
Response object for an asynchronous domain similarity search request submission

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**RequestId** | **Guid** | Unique identifier for tracking the request | [readonly] 
**DomainName** | **string** | Domain name being searched | [readonly] 
**Message** | **string** | Status message providing information about the request | [readonly] 
**StatusUrl** | **string** | URL to check for results (can be polled to monitor progress and get results) | [readonly] 
**QueryString** | **string** | Query string submitted for free-text search (if applicable) | [optional] [readonly] 

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

