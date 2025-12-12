# Whisper.Api.Sdk.Model.BulkRequest
Request payload for bulk enrichment of multiple IP addresses and domains

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Indicators** | **List&lt;string&gt;** | List of indicators (IP addresses or domains) to enrich. Mix of IPs and domains is supported. The indicator type is auto-detected. | 
**Include** | **List&lt;BulkRequest.IncludeEnum&gt;** | Additional data modules to include for each indicator. By default, base enrichment includes geolocation, ASN, reputation, and relationships. For domains, WHOIS (registration) and DNS data are included by default.  &lt;b&gt;Available options:&lt;/b&gt; &lt;ul&gt;   &lt;li&gt;&lt;code&gt;routing&lt;/code&gt; - BGP routing data, prefix visibility, route origins (IPs only)&lt;/li&gt;   &lt;li&gt;&lt;code&gt;rpki&lt;/code&gt; - RPKI validation status (IPs only)&lt;/li&gt;   &lt;li&gt;&lt;code&gt;historical&lt;/code&gt; - Historical data for the indicator&lt;/li&gt;   &lt;li&gt;&lt;code&gt;whois&lt;/code&gt; - WHOIS registration data (domains only, included by default)&lt;/li&gt;   &lt;li&gt;&lt;code&gt;dns&lt;/code&gt; - DNS records (domains only, included by default)&lt;/li&gt;   &lt;li&gt;&lt;code&gt;ip_intelligence&lt;/code&gt; - Full IP enrichment for resolved domain IPs (domains only, significantly increases processing time)&lt;/li&gt; &lt;/ul&gt;  Note: Adding more include options increases processing time per indicator.  | [optional] 
**Options** | [**BulkOptions**](BulkOptions.md) | Advanced processing options for bulk operations. Customize batch size, timeouts, and error handling. | [optional] 

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

