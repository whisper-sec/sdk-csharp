# Whisper.Api.Sdk.Model.TrackingConfig
Change tracking configuration for an indicator

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Enabled** | **bool** | Whether tracking is currently enabled | [optional] 
**Fields** | **List&lt;string&gt;** | Fields being tracked for changes | [optional] 
**Frequency** | **string** | Check frequency: hourly, daily, or weekly | [optional] 
**CreatedAt** | **DateTime** | When tracking was first started | [optional] 
**LastCheck** | **DateTime** | When the last check was performed | [optional] 
**NextCheck** | **DateTime** | When the next check is scheduled | [optional] 
**Username** | **string** | Username of the owner | [optional] 
**Type** | **string** | Indicator type: ip or domain | [optional] 
**Value** | **string** | Indicator value | [optional] 

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

