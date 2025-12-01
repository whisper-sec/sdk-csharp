# Whisper.Api.Sdk.Api.LocationApi

All URIs are relative to *http://api.whisper.security*

| Method | HTTP request | Description |
|--------|--------------|-------------|
| [**GetBulkIpLocation**](LocationApi.md#getbulkiplocation) | **POST** /v1/location/ips/bulk | Bulk IP Geolocation Lookup |
| [**GetIpLocation**](LocationApi.md#getiplocation) | **GET** /v1/location/ip/{ip} | Get IP Geolocation and ASN Data |
| [**GetLocationStats**](LocationApi.md#getlocationstats) | **GET** /v1/location/stats | Get Geolocation Database Statistics |
| [**GetNetworkLocation**](LocationApi.md#getnetworklocation) | **GET** /v1/location/network/{*network} | Get Network/CIDR Geolocation Data |
| [**SearchLocation**](LocationApi.md#searchlocation) | **GET** /v1/location/search | Search Geolocation Database by Field |

<a id="getbulkiplocation"></a>
# **GetBulkIpLocation**
> void GetBulkIpLocation (List<string> requestBody)

Bulk IP Geolocation Lookup

<p>Retrieve geolocation data for up to 1000 IP addresses in a single request. Optimized for batch processing with parallel lookups.</p> <h4>Request Format:</h4> <p>Send a JSON array of IP addresses (IPv4 or IPv6):</p> <pre><code>[\"8.8.8.8\", \"1.1.1.1\", \"208.67.222.222\"]</code></pre> <h4>Performance:</h4> <ul>     <li><b>Response Time:</b> 500-2000ms for typical batches (10-100 IPs)</li>     <li><b>Processing:</b> Parallel lookups with automatic batching</li>     <li><b>Limit:</b> Maximum 1000 IPs per request</li>     <li><b>Rate Limit:</b> 10 requests per minute</li> </ul> <h4>Response Format:</h4> <p>Returns an array of geolocation objects matching the order of input IPs. Failed lookups are indicated with error objects.</p> <h4>Use Cases:</h4> <ul>     <li>Batch enrichment of access logs</li>     <li>Bulk fraud scoring</li>     <li>Geographic distribution analysis</li>     <li>Network infrastructure mapping</li> </ul> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **requestBody** | [**List&lt;string&gt;**](string.md) | JSON array of IP addresses to lookup. Maximum 1000 IPs per request. |  |

### Return type

void (empty response body)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **429** | Rate limit exceeded for bulk operations. |  -  |
| **200** | Successfully retrieved bulk geolocation data. |  -  |
| **400** | Invalid request format. Expected JSON array of IP addresses, or array exceeds 1000 IP limit. |  -  |
| **401** | Authentication failed. Missing or invalid API key. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="getiplocation"></a>
# **GetIpLocation**
> void GetIpLocation (string ip)

Get IP Geolocation and ASN Data

<p>Returns comprehensive geolocation and network information for any IPv4 or IPv6 address. This is one of the fastest endpoints in the API, optimized for real-time fraud detection and access control.</p> <h4>Data Included:</h4> <ul>     <li><b>Geographic:</b> Country, city, region, postal code, coordinates, timezone</li>     <li><b>Network:</b> ASN, ISP/organization name, network range</li>     <li><b>Classification:</b> Connection type (residential, datacenter, VPN, proxy, hosting)</li>     <li><b>Reputation:</b> Risk indicators and abuse scores</li> </ul> <h4>Performance:</h4> <ul>     <li><b>Response Time:</b> Typically &lt;150ms</li>     <li><b>Cache:</b> Results cached for 6 hours by default</li> </ul> <h4>Use Cases:</h4> <ul>     <li>Real-time fraud detection in payment flows</li>     <li>Geographic access control and compliance</li>     <li>Bot and VPN detection</li>     <li>Threat intelligence enrichment</li> </ul> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **ip** | **string** | The IPv4 or IPv6 address to lookup. |  |

### Return type

void (empty response body)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **404** | IP address not found in geolocation database. |  -  |
| **200** | Successfully retrieved geolocation data. |  -  |
| **401** | Authentication failed. Missing or invalid API key. |  -  |
| **429** | Rate limit exceeded. |  -  |
| **400** | Invalid IP address format. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="getlocationstats"></a>
# **GetLocationStats**
> void GetLocationStats ()

Get Geolocation Database Statistics

<p>Returns metadata and statistics about the geolocation database, including coverage, update frequency, and data quality metrics.</p> <h4>Statistics Included:</h4> <ul>     <li><b>Coverage:</b> Total IP addresses, networks, and ASNs covered</li>     <li><b>Geographic:</b> Number of countries, cities, and regions</li>     <li><b>Freshness:</b> Last update timestamp and update frequency</li>     <li><b>Data Sources:</b> Providers and data collection methods</li>     <li><b>Accuracy:</b> Quality metrics and confidence scores</li> </ul> <h4>Use Cases:</h4> <ul>     <li>Verifying database coverage for your use case</li>     <li>Monitoring data freshness</li>     <li>Understanding data quality and accuracy</li> </ul> 


### Parameters
This endpoint does not need any parameter.
### Return type

void (empty response body)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **401** | Authentication failed. Missing or invalid API key. |  -  |
| **200** | Successfully retrieved database statistics. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="getnetworklocation"></a>
# **GetNetworkLocation**
> void GetNetworkLocation (string network)

Get Network/CIDR Geolocation Data

<p>Returns geolocation and network information for an entire network range specified in CIDR notation. Useful for analyzing network blocks, ranges, and subnets.</p> <h4>Supported Formats:</h4> <ul>     <li><b>IPv4 CIDR:</b> 192.168.1.0/24</li>     <li><b>IPv6 CIDR:</b> 2001:db8::/32</li> </ul> <h4>Data Included:</h4> <ul>     <li><b>Network Details:</b> CIDR range, first/last IP, total addresses</li>     <li><b>Geographic:</b> Country, city, region for the network block</li>     <li><b>Network:</b> ASN, organization, ISP information</li>     <li><b>Classification:</b> Network type and usage category</li> </ul> <h4>Use Cases:</h4> <ul>     <li>Analyzing suspicious network ranges</li>     <li>Bulk geolocation for network blocks</li>     <li>Infrastructure mapping and reconnaissance</li> </ul> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **network** | **string** | The network range in CIDR notation (e.g., 192.168.1.0/24 or 2001:db8::/32). |  |

### Return type

void (empty response body)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **400** | Invalid CIDR format or network specification. |  -  |
| **404** | Network not found in geolocation database. |  -  |
| **401** | Authentication failed. Missing or invalid API key. |  -  |
| **200** | Successfully retrieved network geolocation data. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="searchlocation"></a>
# **SearchLocation**
> void SearchLocation (string field, string value, int limit = null)

Search Geolocation Database by Field

<p>Search the geolocation database by specific fields to find all IP addresses matching your criteria. Powerful for threat hunting, infrastructure discovery, and pattern analysis.</p> <h4>Searchable Fields:</h4> <ul>     <li><b>Geographic:</b> city, country, country_code, region, postal_code, continent, continent_code</li>     <li><b>Network:</b> asn, as_number, organization, isp, isp_name</li>     <li><b>Coordinates:</b> latitude, longitude</li> </ul> <h4>Query Examples:</h4> <ul>     <li><b>Find all IPs in a city:</b> field=city&value=London</li>     <li><b>Find all IPs for an ASN:</b> field=asn&value=15169</li>     <li><b>Find all IPs for an ISP:</b> field=isp_name&value=Google</li>     <li><b>Find all IPs in country:</b> field=country_code&value=US</li> </ul> <h4>Performance:</h4> <ul>     <li><b>Response Time:</b> 200-500ms depending on result size</li>     <li><b>Rate Limit:</b> 5 searches per minute</li> </ul> <h4>Use Cases:</h4> <ul>     <li>Infrastructure mapping for threat actors</li>     <li>Finding all IPs in a specific region for compliance</li>     <li>Discovering VPN/proxy exit nodes</li>     <li>Threat hunting by ISP or ASN</li> </ul> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **field** | **string** | The field to search. Valid fields: city, country, country_code, isp_name, isp, asn, as_number, organization, continent, continent_code, region, postal_code, latitude, longitude |  |
| **value** | **string** | The value to search for in the specified field. |  |
| **limit** | **int** | Maximum number of results to return. | [optional] [default to 100] |

### Return type

void (empty response body)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Successfully retrieved search results. |  -  |
| **400** | Invalid search field or parameters. |  -  |
| **401** | Authentication failed. Missing or invalid API key. |  -  |
| **429** | Rate limit exceeded for search operations. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

