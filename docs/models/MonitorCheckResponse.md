# Whisper.Api.Sdk.Model.MonitorCheckResponse
Monitoring check details

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Id** | **string** | Unique identifier for the check | [optional] 
**Name** | **string** | Name of the monitoring check | [optional] 
**Url** | **string** | URL being monitored | [optional] 
**Type** | **string** | Type of check | [optional] 
**Status** | **string** | Current status | [optional] 
**Enabled** | **bool** | Whether the check is enabled | [optional] 
**Frequency** | **int** | Check frequency in minutes | [optional] 
**Locations** | **List&lt;string&gt;** | Locations where check runs | [optional] 
**Muted** | **bool** | Whether the check is muted (no alerts) | [optional] 
**Method** | **string** | HTTP method used for API checks | [optional] 
**Assertions** | [**MonitorAssertions**](MonitorAssertions.md) | Assertions configured for this check | [optional] 
**LastRunAt** | **DateTime** | Last time the check ran | [optional] 
**CreatedAt** | **DateTime** | When the check was created | [optional] 
**UpdatedAt** | **DateTime** | When the check was last updated | [optional] 
**Uptime24Hours** | **double** | Uptime percentage over the last 24 hours | [optional] 
**Uptime7Days** | **double** | Uptime percentage over the last 7 days | [optional] 
**Uptime30Days** | **double** | Uptime percentage over the last 30 days | [optional] 
**ResponseTime** | **long** | Average response time in milliseconds | [optional] 

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

