# Whisper.Api.Sdk.Model.MonitorAssertions
Assertions to validate check results

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Headers** | **Dictionary&lt;string, string&gt;** | Expected response headers | [optional] 
**StatusCode** | **int** | Expected HTTP status code | [optional] 
**MaxResponseTime** | **long** | Maximum response time in milliseconds | [optional] 
**ContainsText** | **string** | Text that must be present in response body | [optional] 
**NotContainsText** | **string** | Text that must NOT be present in response body | [optional] 
**SslDaysUntilExpiry** | **int** | Minimum SSL certificate days until expiry (for ssl checks) | [optional] 
**DnsRecordValue** | **string** | Expected DNS record value (for dns checks) | [optional] 
**DnsRecordType** | **string** | DNS record type (for dns checks) | [optional] 

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

