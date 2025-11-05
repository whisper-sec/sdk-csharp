# Whisper.Api.Sdk.Model.JobResponse
Response returned when an asynchronous job is created. Contains the job ID and status URL for polling.

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**JobId** | **string** | Unique identifier for the job. Use this ID to poll for job status and results. | 
**Status** | **string** | Current status of the job | 
**StatusUrl** | **string** | URL endpoint to poll for job status and results. Typically &#x60;/v1/ops/jobs/{jobId}&#x60;. | 
**Message** | **string** | Human-readable message describing the job acceptance or current state | [optional] 

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

