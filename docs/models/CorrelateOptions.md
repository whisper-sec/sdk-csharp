# Whisper.Api.Sdk.Model.CorrelateOptions
Configuration options for correlation analysis. This is an OBJECT, not a string. All fields are optional. 

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**TimeWindow** | **string** | Time window for temporal correlation. Format: number + unit (d&#x3D;days, w&#x3D;weeks, m&#x3D;months). Examples: 7d, 2w, 3m | [optional] 
**CorrelationTypes** | **List&lt;string&gt;** | Types of correlation to analyze. Possible values: infrastructure, campaign, actor, malware, technique | [optional] 
**MinConfidence** | **double** | Minimum confidence threshold for correlations (0.0 to 1.0). Higher values return fewer but more confident results. | [optional] 
**IncludeIndustryBreakdown** | **bool** | Include breakdown of indicator prevalence by industry sector in the response. | [optional] 

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

