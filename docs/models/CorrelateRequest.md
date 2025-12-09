# Whisper.Api.Sdk.Model.CorrelateRequest
Request for cross-customer indicator correlation analysis

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Indicators** | **List&lt;string&gt;** | List of indicators (IPs, domains, hashes) to correlate across global threat intelligence. Maximum 100 indicators per request. | 
**Options** | [**CorrelateOptions**](CorrelateOptions.md) | Optional configuration object for correlation analysis. NOT a string - must be an object with fields like timeWindow, minConfidence, etc. | [optional] 

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

