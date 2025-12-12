# Whisper.Api.Sdk.Model.JobSummary
Summary of a job

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**JobId** | **string** | Unique job identifier | [optional] 
**Type** | **string** | Type of job | [optional] 
**Status** | **string** | Current job status | [optional] 
**CreatedAt** | **string** | Job creation timestamp | [optional] 
**CompletedAt** | **string** | Job completion timestamp (if completed) | [optional] 
**Progress** | [**ProgressInfo**](ProgressInfo.md) | Job progress information | [optional] 
**Error** | [**ErrorInfo**](ErrorInfo.md) | Error information (if failed) | [optional] 

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

