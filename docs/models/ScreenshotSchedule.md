# Whisper.Api.Sdk.Model.ScreenshotSchedule
A scheduled screenshot configuration

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Id** | **string** | Unique identifier for this schedule | [optional] 
**Url** | **string** | The URL to capture screenshots of | [optional] 
**Username** | **string** | Username/API key owner of this schedule | [optional] 
**Cron** | **string** | Cron expression for scheduling (mutually exclusive with frequency) | [optional] 
**Frequency** | **string** | Frequency preset (mutually exclusive with cron). Use one of the preset values for simplified scheduling. | [optional] 
**Timezone** | **string** | Timezone for the schedule | [optional] 
**Enabled** | **bool** | Whether this schedule is currently active | [optional] 
**Options** | [**ScreenshotOptions**](ScreenshotOptions.md) | Screenshot options (width, height, format, etc.) | [optional] 
**CreatedAt** | **DateTime** | When this schedule was created | [optional] 
**UpdatedAt** | **DateTime** | When this schedule was last updated | [optional] 
**LastCaptureAt** | **DateTime** | When the last screenshot was captured | [optional] 
**NextCaptureAt** | **DateTime** | When the next screenshot is scheduled | [optional] 
**CaptureCount** | **int** | Total number of screenshots captured by this schedule | [optional] 

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

