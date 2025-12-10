# Whisper.Api.Sdk.Model.InfrastructureMapRequest
Configuration for mapping infrastructure relationships and discovering connected assets

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**StartPoint** | **string** | Starting point for infrastructure mapping (domain or IP address) | 
**Depth** | **int** | Depth of relationship mapping (number of hops from starting point). Depth 1: Direct relationships (~30s, 10-50 assets), Depth 2: 2 hops (~2-5 min, 50-500 assets), Depth 3: 3 hops (~10-30 min, 500-5000 assets) | [optional] [default to 1]

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

