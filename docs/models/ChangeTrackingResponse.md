# Whisper.Api.Sdk.Model.ChangeTrackingResponse
Change tracking response with configuration and detected changes

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Indicator** | **string** | The indicator value (IP or domain) | [optional] 
**Type** | **string** | Indicator type: ip or domain | [optional] 
**Tracking** | [**TrackingConfig**](TrackingConfig.md) |  | [optional] 
**Changes** | [**List&lt;ChangeEvent&gt;**](ChangeEvent.md) | List of detected changes | [optional] 
**Baseline** | **Object** |  | [optional] 
**BaselineCapturedAt** | **DateTime** | When the baseline was captured | [optional] 
**TotalChanges** | **int** | Total number of changes detected | [optional] 
**Error** | **string** | Error message if operation failed | [optional] 
**Success** | **bool** | Whether the operation was successful | [optional] 

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

