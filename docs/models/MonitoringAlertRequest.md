# Whisper.Api.Sdk.Model.MonitoringAlertRequest
Configuration for creating monitoring alert rules with notification channels

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Type** | **string** | Type of alert condition to monitor | 
**ThresholdDays** | **int** | Threshold in days (for ssl_expiring alerts). Alert triggers when SSL cert expires within this many days. | [optional] 
**Channels** | **List&lt;string&gt;** | Notification channels to use for alerts | [optional] 
**Email** | **string** | Email address for alert notifications | [optional] 
**SlackWebhook** | **string** | Slack webhook URL for notifications | [optional] 
**WebhookUrl** | **string** | Custom webhook URL for notifications (will receive POST with alert data) | [optional] 
**PagerdutyKey** | **string** | PagerDuty integration key for incident creation | [optional] 

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

