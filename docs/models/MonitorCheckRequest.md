# Whisper.Api.Sdk.Model.MonitorCheckRequest
Request to create or update a monitoring check

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Name** | **string** | Name of the monitoring check | 
**Url** | **string** | URL to monitor | 
**Type** | **string** | Type of check: api, ssl, or dns | [optional] 
**Frequency** | **int** | Check frequency in minutes | [optional] 
**Locations** | **List&lt;string&gt;** | Locations to run checks from | [optional] 
**Assertions** | [**MonitorAssertions**](MonitorAssertions.md) |  | [optional] 
**Enabled** | **bool** | Whether the check is enabled | [optional] 
**Method** | **string** | HTTP method for API checks | [optional] 
**Headers** | **Dictionary&lt;string, string&gt;** | Request headers for API checks | [optional] 
**Body** | **string** | Request body for POST/PUT API checks | [optional] 
**Valid** | **bool** |  | [optional] 

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

