# Whisper.Api.Sdk.Model.SearchResponse
Result returned when a WHOIS search job completes. Access this via GET /v1/ops/jobs/{jobId} after the job status becomes COMPLETED.

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Source** | **string** | The data source that was searched | 
**QueryType** | **string** | The type of query that was performed | 
**Items** | [**List&lt;DomainItem&gt;**](DomainItem.md) | List of matching domains | 
**Total** | **int** | Total number of matching records across all pages | 
**PageNumber** | **int** | Current page number (0-indexed) | 
**PageSize** | **int** | Number of results per page | 
**TotalPages** | **int** | Total number of pages available | 
**Error** | **bool** | Error flag, present only when the search failed | [optional] 
**Message** | **string** | Error message, present only when the search failed | [optional] 

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

