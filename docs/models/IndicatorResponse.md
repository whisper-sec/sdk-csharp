# Whisper.Api.Sdk.Model.IndicatorResponse
Comprehensive intelligence response for an IP address or domain indicator

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Query** | [**QueryInfo**](QueryInfo.md) |  | [optional] 
**Summary** | [**SummaryInfo**](SummaryInfo.md) |  | [optional] 
**Geolocation** | **Object** |  | [optional] 
**Network** | **Object** |  | [optional] 
**Routing** | **Object** |  | [optional] 
**Isp** | **Object** |  | [optional] 
**Registration** | **Object** |  | [optional] 
**Dns** | [**DnsInfo**](DnsInfo.md) |  | [optional] 
**Relationships** | [**RelationshipInfo**](RelationshipInfo.md) |  | [optional] 
**Reputation** | [**ReputationInfo**](ReputationInfo.md) |  | [optional] 
**Security** | **Object** |  | [optional] 
**Rpki** | **Object** |  | [optional] 
**IpIntelligence** | **Dictionary&lt;string, Object&gt;** | When domain is queried with include&#x3D;ip_intelligence, contains full intelligence for each resolved IP | [optional] 
**Metadata** | [**MetadataInfo**](MetadataInfo.md) |  | [optional] 

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

