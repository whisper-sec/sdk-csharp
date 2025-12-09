# Whisper.Api.Sdk.Model.SimilarDomainsResponse
Result returned when a similar domains job completes. Access this via GET /v1/ops/jobs/{jobId} after the job status becomes COMPLETED.

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Domain** | **string** | The input domain that was analyzed | 
**Status** | **string** | Job completion status | 
**SimilarDomains** | [**List&lt;SimilarDomainEntry&gt;**](SimilarDomainEntry.md) | List of similar domains found | 
**TotalCount** | **int** | Total number of similar domains found | 
**Analysis** | [**AnalysisMetadata**](AnalysisMetadata.md) | Analysis metadata about the search | 
**Error** | **bool** | Error flag, present only when status is &#39;failed&#39; | [optional] 
**Message** | **string** | Error message, present only when status is &#39;failed&#39; | [optional] 

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

