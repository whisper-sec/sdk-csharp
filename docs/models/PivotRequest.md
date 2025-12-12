# Whisper.Api.Sdk.Model.PivotRequest
Request for intelligent infrastructure pivoting and relationship discovery

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Indicator** | **string** | Starting indicator (IP address, domain, or hash) for pivot analysis | 
**IndicatorType** | **string** | Type of the starting indicator. Must be one of: ip, domain, hash | 
**Depth** | **int** | Pivot depth - how many hops to traverse from the starting indicator. Higher depth &#x3D; more results but longer processing time. | [optional] [default to 1]
**Strategies** | **List&lt;string&gt;** | Pivot strategies to use. Possible values: dns (DNS relationships), whois (WHOIS data), ssl (SSL certificates), infrastructure (hosting), passive_dns (historical DNS) | [optional] 
**MaxNodes** | **int** | Maximum number of related nodes/indicators to discover. Limits result size for performance. | [optional] [default to 100]

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

