# Whisper.Api.Sdk.Model.ErrorResponse
Standard error response returned when an API request fails

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Status** | **int** | The HTTP status code of the error | 
**Error** | **string** | A short, machine-readable error code | 
**Message** | **string** | A human-readable error message providing more detail | 
**Timestamp** | **DateTime** | The timestamp when the error occurred | 
**Details** | **Object** |  | [optional] 
**TraceId** | **string** | A unique trace ID for this request, useful for debugging | [optional] 
**Path** | **string** | The API path that generated this error | [optional] 

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

