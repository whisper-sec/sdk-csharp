# Whisper.Api.Sdk.Api.IndicatorsApi

All URIs are relative to *http://api.whisper.security*

| Method | HTTP request | Description |
|--------|--------------|-------------|
| [**GetIndicator**](IndicatorsApi.md#getindicator) | **GET** /v1/indicators/{type}/{value} | Enrich a Single Indicator (IP or Domain) |
| [**GetIndicatorGraph**](IndicatorsApi.md#getindicatorgraph) | **GET** /v1/indicators/{type}/{value}/graph | Get Infrastructure Relationship Graph |
| [**GetIndicatorHistory**](IndicatorsApi.md#getindicatorhistory) | **GET** /v1/indicators/{type}/{value}/history | Get Historical Data for Indicator |
| [**GetSubdomains**](IndicatorsApi.md#getsubdomains) | **GET** /v1/indicators/domain/{domain}/subdomains | Get Domain Subdomains |

<a id="getindicator"></a>
# **GetIndicator**
> IndicatorResponse GetIndicator (string type, string value, string include = null)

Enrich a Single Indicator (IP or Domain)

<p>Retrieves comprehensive intelligence for a single IP address or domain. This is the primary, high-performance endpoint for synchronous enrichment.</p> <p>It aggregates data from multiple sources, including geolocation, WHOIS, DNS, reputation scoring, and relationship mapping. Use the `include` parameter to request additional, deeper data sets that may have higher latency.</p> <h4>Performance:</h4> <ul>     <li><b>Base Response:</b> Typically under 500ms.</li>     <li><b>With `include=routing`:</b> First request may take up to 5 seconds; subsequent requests are cached for 5 minutes and respond in &lt;200ms.</li>     <li><b>With `include=ip_intelligence`:</b> Adds 200-500ms of latency for each IP address resolved from the domain.</li> </ul> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **type** | **string** | The type of indicator to enrich. |  |
| **value** | **string** | The value of the indicator (e.g., an IPv4/IPv6 address or a domain name). |  |
| **include** | **string** | A comma-separated list of additional data modules to include in the response. Requesting more modules may increase latency. | [optional]  |

### Return type

[**IndicatorResponse**](IndicatorResponse.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **404** | The requested indicator was not found in our datasets. |  -  |
| **400** | Invalid indicator format or unsupported type. |  -  |
| **200** | Successfully retrieved intelligence data. |  -  |
| **401** | Authentication failed. Missing or invalid API key. |  -  |
| **429** | Rate limit exceeded. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="getindicatorgraph"></a>
# **GetIndicatorGraph**
> void GetIndicatorGraph (string type, string value, int limit = null)

Get Infrastructure Relationship Graph

<p>Returns graph visualization data showing relationships between the indicator and related infrastructure. Perfect for interactive network diagrams and threat actor infrastructure mapping.</p> <h4>Relationship Types Included:</h4> <ul>     <li><b>For Domains:</b>         <ul>             <li>Resolves to IPs</li>             <li>Shares nameservers with</li>             <li>Same SSL certificate as</li>             <li>Same registrant as</li>             <li>Links to/from other domains</li>         </ul>     </li>     <li><b>For IPs:</b>         <ul>             <li>Hosts domains</li>             <li>Same ASN as</li>             <li>Same network block as</li>             <li>Connected via routing</li>         </ul>     </li> </ul> <h4>Output Format:</h4> <p>Compatible with react-force-graph, vis.js, cytoscape.js:</p> <pre><code>{   \"nodes\": [     {\"id\": \"example.com\", \"type\": \"domain\", \"label\": \"example.com\"},     {\"id\": \"8.8.8.8\", \"type\": \"ip\", \"label\": \"8.8.8.8\"}   ],   \"links\": [     {\"source\": \"example.com\", \"target\": \"8.8.8.8\", \"type\": \"resolves_to\"}   ] }</code></pre> <h4>Performance:</h4> <ul>     <li>Response Time: 500ms-2s depending on graph complexity</li>     <li>Default: 100 nodes maximum (adjustable)</li> </ul> <h4>Use Cases:</h4> <ul>     <li>Interactive threat actor infrastructure visualization</li>     <li>Discovering related phishing campaigns</li>     <li>Mapping shadow IT and sprawl</li>     <li>Network topology visualization</li> </ul> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **type** | **string** | Type of indicator |  |
| **value** | **string** | The indicator value (IP address or domain) |  |
| **limit** | **int** | Maximum number of nodes to return in the graph | [optional] [default to 100] |

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
| **400** | Invalid indicator type or limit parameter. |  -  |
| **200** | Successfully retrieved graph data. |  -  |
| **401** | Authentication failed. Missing or invalid API key. |  -  |
| **404** | Indicator not found or no relationships discovered. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="getindicatorhistory"></a>
# **GetIndicatorHistory**
> HistoryResponse GetIndicatorHistory (string type, string value, string historyType = null)

Get Historical Data for Indicator

<p>Retrieves time-series historical data for an IP address or domain. Track how infrastructure changes over time for threat intelligence and forensic analysis.</p> <h4>History Types:</h4> <ul>     <li><b>whois:</b> Registration history - registrant changes, expiration updates, transfers</li>     <li><b>routing:</b> BGP routing history - prefix announcements, ASN changes, route hijacks</li>     <li><b>dns:</b> DNS resolution history - IP address changes, nameserver updates</li>     <li><b>ssl:</b> Certificate history - cert replacements, CA changes, expiration events</li>     <li><b>reputation:</b> Risk score history - blacklist appearances, reputation changes</li> </ul> <h4>Data Format:</h4> <p>Timeline with dated snapshots showing what changed and when:</p> <pre><code>{   \"history\": [     {       \"timestamp\": \"2025-01-15T10:00:00Z\",       \"field\": \"registrant_company\",       \"old_value\": \"Evil Corp\",       \"new_value\": \"Legitimate LLC\"     }   ] }</code></pre> <h4>Use Cases:</h4> <ul>     <li>Tracking domain ownership changes</li>     <li>Investigating IP reputation degradation</li>     <li>Forensic timeline reconstruction</li>     <li>Detecting infrastructure pivots by threat actors</li> </ul> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **type** | **string** | Type of indicator |  |
| **value** | **string** | The indicator value (IP address or domain) |  |
| **historyType** | **string** | Type of historical data to retrieve | [optional]  |

### Return type

[**HistoryResponse**](HistoryResponse.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **404** | No historical data found for this indicator. |  -  |
| **200** | Successfully retrieved historical data. |  -  |
| **400** | Invalid indicator type or history type. |  -  |
| **401** | Authentication failed. Missing or invalid API key. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="getsubdomains"></a>
# **GetSubdomains**
> SubdomainResponse GetSubdomains (string domain, int limit = null)

Get Domain Subdomains

Retrieves a list of discovered subdomains for a given root domain, based on passive DNS and other enumeration techniques.


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **domain** | **string** | The root domain to query for subdomains. |  |
| **limit** | **int** | The maximum number of subdomains to return. | [optional] [default to 100] |

### Return type

[**SubdomainResponse**](SubdomainResponse.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **404** | Domain not found or no subdomains discovered. |  -  |
| **400** | Invalid domain format. |  -  |
| **401** | Authentication failed. Missing or invalid API key. |  -  |
| **200** | Successfully retrieved subdomains. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

