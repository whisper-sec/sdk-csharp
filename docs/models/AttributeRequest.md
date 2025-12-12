# Whisper.Api.Sdk.Model.AttributeRequest
Request for threat actor attribution and campaign clustering

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Indicators** | **List&lt;string&gt;** | List of indicators (IPs, domains, hashes, URLs) for attribution analysis. Maximum 500 indicators per request. | 
**Context** | [**AttributionContext**](AttributionContext.md) | Optional context object to enhance attribution accuracy. NOT a string - must be an object with fields like observedTTPs, targetedSector, etc. | [optional] 

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

