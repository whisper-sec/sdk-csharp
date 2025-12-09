# Whisper.Api.Sdk.Model.ScreenshotHistoryResponse
Response containing screenshot history for a target URL

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Target** | **string** | The target domain or URL queried | [optional] 
**Schedules** | [**List&lt;ScheduleWithScreenshots&gt;**](ScheduleWithScreenshots.md) | List of schedules that captured screenshots of this target | [optional] 
**TotalScreenshots** | **int** | Total number of screenshots available for this target | [optional] 
**Limit** | **int** | Maximum number of screenshots returned (limit parameter) | [optional] 

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

