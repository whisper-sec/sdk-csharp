# Whisper.Api.Sdk.Model.InfraScanRequest
Configuration for performing infrastructure discovery and security scanning

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Target** | **string** | The target to scan (IP, CIDR, domain, or ASN) | 
**TargetType** | **string** | Type of target being scanned | 
**ScanTypes** | **HashSet&lt;string&gt;** | Types of scans to perform | [optional] 
**ScanDepth** | **string** | Scan depth level | [optional] [default to ScanDepthEnum.Medium]
**Timeout** | **int** | Maximum scan duration in seconds | [optional] [default to 300]
**Options** | [**ScanOptions**](ScanOptions.md) |  | [optional] 

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

