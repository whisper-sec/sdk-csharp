# Whisper.Api.Sdk.Model.SimilarCasesRequest
Request for ML-based similar case matching. Finds historical incidents similar to the current case based on indicators, behaviors, and TTPs.

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Indicators** | **List&lt;string&gt;** | List of indicators (IPs, domains, hashes, URLs) associated with the current case. This is the primary matching criteria. | 
**BehaviorDescription** | **string** | Free-text description of observed malicious behavior or incident details. Improves matching accuracy by considering behavioral patterns. | [optional] 
**ObservedTTPs** | **List&lt;string&gt;** | Observed MITRE ATT&amp;CK technique IDs. Helps find cases with similar attack techniques. See https://attack.mitre.org for reference. | [optional] 
**MinSimilarity** | **double** | Minimum similarity score threshold (0.0 to 1.0). Higher values return fewer but more precise matches. Default: 0.5 | [optional] [default to 0.5D]
**Limit** | **int** | Maximum number of similar cases to return. Higher limits may increase processing time. | [optional] [default to 10]

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

