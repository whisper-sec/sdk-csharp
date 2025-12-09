# Whisper.Api.Sdk.Model.InvestigateContext
Additional context to guide and enhance the investigation. This is an OBJECT, not a string. All fields are optional. 

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**RelatedIndicators** | **List&lt;string&gt;** | Related indicators (IPs, domains, hashes) to include in the investigation scope. Helps identify connections between indicators. | [optional] 
**Hypothesis** | **string** | Initial hypothesis or suspicion to focus the investigation. The AI will attempt to prove or disprove this theory. | [optional] 
**TimeRange** | **string** | Time range for historical analysis. Format: number + unit (d&#x3D;days, w&#x3D;weeks, m&#x3D;months). Examples: 7d, 2w, 3m, 90d | [optional] 

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

