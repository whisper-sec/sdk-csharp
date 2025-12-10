# Whisper.Api.Sdk.Model.AttributionContext
Context information to improve threat actor attribution accuracy. This is an OBJECT, not a string. All fields are optional but provide better results. 

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**ObservedTTPs** | **List&lt;string&gt;** | Observed MITRE ATT&amp;CK technique IDs. See https://attack.mitre.org for reference. | [optional] 
**TargetedSector** | **string** | Targeted industry sector. Common values: financial, healthcare, government, technology, energy, retail, manufacturing | [optional] 
**TargetRegion** | **string** | Geographic region of targets. Use ISO country codes or region names. | [optional] 
**Timeframe** | **string** | Campaign timeframe for attribution. Format: &#39;YYYY-MM-DD to YYYY-MM-DD&#39; or descriptive like &#39;Q1 2024&#39; | [optional] 
**MalwareFamilies** | **List&lt;string&gt;** | Known malware families observed in the campaign. Helps narrow down threat actor candidates. | [optional] 

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

