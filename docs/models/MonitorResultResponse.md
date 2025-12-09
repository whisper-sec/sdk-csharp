# Whisper.Api.Sdk.Model.MonitorResultResponse
Result of a single check execution

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Timestamp** | **DateTime** | When the check was executed | [optional] 
**Success** | **bool** | Whether the check passed | [optional] 
**Location** | **string** | Location where check ran | [optional] 
**Attempt** | **int** | Check attempt number (for retries) | [optional] 
**CheckId** | **string** | ID of the check this result belongs to | [optional] 
**ResultId** | **string** | Unique result ID | [optional] 
**ResponseTime** | **long** | Response time in milliseconds | [optional] 
**StatusCode** | **int** | HTTP status code received | [optional] 
**ErrorMessage** | **string** | Error message if check failed | [optional] 
**HasErrors** | **bool** | Whether check ran from all locations | [optional] 

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

