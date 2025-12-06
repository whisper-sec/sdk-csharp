# Whisper.Api.Sdk.Model.SimilarCasesRequest
Request for ML-based similar case matching

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Indicators** | **List&lt;string&gt;** | List of indicators for the current case | 
**BehaviorDescription** | **string** | Description of observed behavior | [optional] 
**ObservedTTPs** | **List&lt;string&gt;** | Observed MITRE ATT&amp;CK TTPs | [optional] 
**MinSimilarity** | **double** | Confidence threshold for matches (0-1) | [optional] 
**Limit** | **int** | Maximum number of similar cases to return | [optional] 

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

