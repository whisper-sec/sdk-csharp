# Whisper.Api.Sdk.Model.IndicatorResponse
Comprehensive intelligence response for an IP address or domain indicator

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Query** | [**QueryInfo**](QueryInfo.md) | Query metadata including the indicator type, value, and response timing | [optional] 
**Summary** | [**SummaryInfo**](SummaryInfo.md) | Executive summary with key facts about the indicator for quick decision-making | [optional] 
**Geolocation** | **Object** |  | [optional] 
**Network** | **Object** |  | [optional] 
**Routing** | **Object** |  | [optional] 
**Isp** | **Object** |  | [optional] 
**Registration** | **Object** |  | [optional] 
**Dns** | [**DnsInfo**](DnsInfo.md) | DNS records and resolution data | [optional] 
**Relationships** | [**RelationshipInfo**](RelationshipInfo.md) | Relationship data showing connections to other infrastructure | [optional] 
**Reputation** | [**ReputationInfo**](ReputationInfo.md) | Reputation and risk scoring information | [optional] 
**Security** | **Object** |  | [optional] 
**Rpki** | **Object** |  | [optional] 
**IpIntelligence** | **Dictionary&lt;string, Object&gt;** | When domain is queried with include&#x3D;ip_intelligence, contains full intelligence for each resolved IP | [optional] 
**Metadata** | [**MetadataInfo**](MetadataInfo.md) | Response metadata including data sources, errors, and processing information | [optional] 

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

