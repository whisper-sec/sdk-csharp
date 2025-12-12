# Whisper.Api.Sdk.Model.InvestigateRequest
Request for comprehensive AI-powered threat investigation. Analyzes indicators and returns verdict, timeline, and recommendations.

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Indicator** | **string** | The indicator to investigate (IP address, domain name, or file hash) | 
**IndicatorType** | **string** | Type of indicator being investigated | 
**Depth** | **string** | Investigation depth level. &#39;quick&#39; (30-60s) for basic checks, &#39;standard&#39; (60-120s) for typical investigations, &#39;comprehensive&#39; (120-300s) for deep analysis. | [optional] [default to DepthEnum.Standard]
**Context** | [**InvestigateContext**](InvestigateContext.md) | Optional context object to guide the investigation. Provides additional information like hypothesis, related indicators, and time range. | [optional] 

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

