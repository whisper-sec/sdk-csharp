# Whisper.Api.Sdk.Model.TrackedIndicator
A tracked indicator with its configuration and status

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Type** | **string** | Indicator type: ip or domain | [optional] 
**Value** | **string** | Indicator value | [optional] 
**Enabled** | **bool** | Whether tracking is currently enabled | [optional] 
**Frequency** | **string** | Check frequency: hourly, daily, weekly | [optional] 
**Fields** | **List&lt;string&gt;** | Fields being tracked | [optional] 
**CreatedAt** | **DateTime** | When tracking was started | [optional] 
**LastCheckAt** | **DateTime** | When the last check was performed | [optional] 
**NextCheckAt** | **DateTime** | When the next check is scheduled | [optional] 
**TotalChanges** | **int** | Total number of changes detected | [optional] 

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

