# Whisper.Api.Sdk.Model.SubdomainResponse
Response containing discovered subdomains and related metadata

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Domain** | **string** | The root domain that was queried | 
**TotalCount** | **int** | Total number of subdomains discovered | 
**Subdomains** | [**List&lt;SubdomainInfo&gt;**](SubdomainInfo.md) | List of discovered subdomains | 
**Timestamp** | **DateTime** | Timestamp of when the data was retrieved | 
**Sources** | **List&lt;string&gt;** | Data sources used for subdomain discovery | [optional] 

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

