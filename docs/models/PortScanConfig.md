# Whisper.Api.Sdk.Model.PortScanConfig
Configuration for port scanning

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Ports** | **string** | Ports to scan (comma-separated or range) | [optional] [default to "top-1000"]
**Technique** | **string** | Scan technique | [optional] [default to TechniqueEnum.Syn]
**Threads** | **int** | Number of parallel threads | [optional] [default to 10]
**PortTimeout** | **int** | Timeout per port in milliseconds | [optional] [default to 1000]

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

