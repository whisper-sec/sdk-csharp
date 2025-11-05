# Whisper.Api.Sdk.Model.BulkRequest
Request payload for bulk enrichment of multiple IP addresses and domains

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Indicators** | **List&lt;string&gt;** | List of indicators (IP addresses or domains) to enrich. Mix of IPs and domains is supported. | 
**Include** | **HashSet&lt;BulkRequest.IncludeEnum&gt;** | Additional data modules to include for each indicator. Same options as single indicator endpoint. | [optional] 
**Options** | [**BulkOptions**](BulkOptions.md) |  | [optional] 

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

