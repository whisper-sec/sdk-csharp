# Whisper.Api.Sdk.Model.SubdomainInfo
Detailed information about a discovered subdomain

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Subdomain** | **string** | The full subdomain name | 
**IpAddresses** | **List&lt;string&gt;** | IP addresses associated with the subdomain | [optional] 
**FirstSeen** | **DateTime** | First time this subdomain was observed | [optional] 
**LastSeen** | **DateTime** | Last time this subdomain was observed | [optional] 
**RecordType** | **string** | Type of subdomain record | [optional] 
**Status** | **string** | Current status of the subdomain | [optional] 
**Technologies** | **List&lt;string&gt;** | Technology stack detected on this subdomain | [optional] 
**RiskScore** | **int** | Risk score for this subdomain (0-100) | [optional] 

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

