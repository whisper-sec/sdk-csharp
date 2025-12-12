# Whisper.Api.Sdk.Model.ChangeEvent
A single detected change event

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Timestamp** | **DateTime** | When the change was detected | [optional] 
**Field** | **string** | Field that changed (dot notation, e.g., &#39;dns.a_record&#39;) | [optional] 
**OldValue** | **Object** |  | [optional] 
**NewValue** | **Object** |  | [optional] 
**Category** | **string** | Category of the change (dns, whois, ssl, etc.) | [optional] 
**Severity** | **string** | Severity of the change: low, medium, high | [optional] 

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

