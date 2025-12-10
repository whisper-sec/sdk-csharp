# Whisper.Api.Sdk.Model.ScheduleConfig
Configuration for scheduling recurring screenshot captures

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Cron** | **string** | Cron expression for scheduling | [optional] 
**Frequency** | **string** | Frequency of captures. Use one of the preset values or provide a cron expression for custom schedules. | [optional] 
**Timezone** | **string** | Timezone for scheduled captures | [optional] [default to "UTC"]
**RetentionCount** | **int** | Maximum number of captures to retain | [optional] [default to 30]
**Enabled** | **bool** | Enable/disable the schedule | [optional] [default to true]

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

