# Whisper.Api.Sdk.Api.IndicatorsApi

All URIs are relative to *https://api.whisper.security*

| Method | HTTP request | Description |
|--------|--------------|-------------|
| [**BulkEnrichment**](IndicatorsApi.md#bulkenrichment) | **POST** /v1/indicators/bulk | Bulk Indicator Enrichment (Asynchronous) |
| [**GenerateSimilarDomainsGet**](IndicatorsApi.md#generatesimilardomainsget) | **GET** /v1/indicators/domain/{domain}/similar | Generate Similar Domains - GET (Asynchronous) |
| [**GenerateSimilarDomainsPost**](IndicatorsApi.md#generatesimilardomainspost) | **POST** /v1/indicators/domain/{domain}/similar | Generate Similar Domains - POST (Asynchronous) |
| [**GetIndicator**](IndicatorsApi.md#getindicator) | **GET** /v1/indicators/{type}/{value} | Enrich a Single Indicator (IP or Domain) |
| [**GetIndicatorGraph**](IndicatorsApi.md#getindicatorgraph) | **GET** /v1/indicators/{type}/{value}/graph | Get Infrastructure Relationship Graph |
| [**GetIndicatorHistory**](IndicatorsApi.md#getindicatorhistory) | **GET** /v1/indicators/{type}/{value}/history | Get Historical Data for Indicator |
| [**GetSubdomains**](IndicatorsApi.md#getsubdomains) | **GET** /v1/indicators/domain/{domain}/subdomains | Get Domain Subdomains |
| [**SearchIndicators**](IndicatorsApi.md#searchindicators) | **POST** /v1/indicators/search | Search Indicators (Asynchronous) |

<a id="bulkenrichment"></a>
# **BulkEnrichment**
> JobResponse BulkEnrichment (BulkRequest bulkRequest)

Bulk Indicator Enrichment (Asynchronous)

<p>Process multiple indicators (IPs and/or domains) in a single request. This endpoint is optimized for batch processing and can handle up to 100 indicators per request.</p> <p><b>Performance:</b> Processing time depends on batch size and requested data modules. Expect 5-30 seconds for typical batches.</p> <p><b>Rate Limits:</b> Limited to 10 requests per minute due to the resource-intensive nature of bulk operations.</p> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **bulkRequest** | [**BulkRequest**](BulkRequest.md) | List of indicators and processing options. |  |

### Return type

[**JobResponse**](JobResponse.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **429** | Rate limit exceeded for bulk operations. |  -  |
| **202** | Bulk job successfully accepted for processing. |  -  |
| **400** | Invalid request. Empty indicator list or exceeds 100 indicator limit. |  -  |
| **401** | Authentication failed. Missing or invalid API key. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="generatesimilardomainsget"></a>
# **GenerateSimilarDomainsGet**
> JobResponse GenerateSimilarDomainsGet (string domain)

Generate Similar Domains - GET (Asynchronous)

<p>Initiates an asynchronous job to generate potential lookalike domains using default options. This GET variant is provided for convenience.</p> <p>For custom options (algorithms, limits, etc.), use the POST version of this endpoint.</p> <p>The API immediately returns a `jobId`. Poll the `/v1/ops/jobs/{jobId}` endpoint to get the results when complete.</p> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **domain** | **string** | The domain to generate variations for. |  |

### Return type

[**JobResponse**](JobResponse.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **400** | Invalid domain format in path. |  -  |
| **202** | Job successfully accepted for processing. |  -  |
| **401** | Authentication failed. Missing or invalid API key. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="generatesimilardomainspost"></a>
# **GenerateSimilarDomainsPost**
> JobResponse GenerateSimilarDomainsPost (string domain, SimilarDomainRequest similarDomainRequest = null)

Generate Similar Domains - POST (Asynchronous)

<p>Initiates an asynchronous job to generate potential lookalike domains for typosquatting, homoglyph, and brand protection analysis. This is a powerful tool for proactive threat hunting.</p> <p>Because this can be a long-running process, the API immediately returns a `jobId`. Poll the `/v1/ops/jobs/{jobId}` endpoint to get the results when the job is complete.</p> <p>Use this POST version to specify custom options like algorithms, limits, or filters.</p> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **domain** | **string** | The domain to generate variations for. |  |
| **similarDomainRequest** | [**SimilarDomainRequest**](SimilarDomainRequest.md) | Configuration for the similarity generation. | [optional]  |

### Return type

[**JobResponse**](JobResponse.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **400** | Invalid domain format in path. |  -  |
| **202** | Job successfully accepted for processing. |  -  |
| **401** | Authentication failed. Missing or invalid API key. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

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
| **429** | Rate limit exceeded. |  -  |
| **400** | Invalid indicator format or unsupported type. |  -  |
| **404** | The requested indicator was not found in our datasets. |  -  |
| **200** | Successfully retrieved intelligence data. |  -  |
| **401** | Authentication failed. Missing or invalid API key. |  -  |

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
| **404** | Indicator not found or no relationships discovered. |  -  |
| **401** | Authentication failed. Missing or invalid API key. |  -  |

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
| **200** | Successfully retrieved historical data. |  -  |
| **400** | Invalid indicator type or history type. |  -  |
| **404** | No historical data found for this indicator. |  -  |
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
| **200** | Successfully retrieved subdomains. |  -  |
| **400** | Invalid domain format. |  -  |
| **401** | Authentication failed. Missing or invalid API key. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="searchindicators"></a>
# **SearchIndicators**
> JobResponse SearchIndicators (SearchRequest searchRequest)

Search Indicators (Asynchronous)

<p>Initiates an asynchronous job to search for indicators matching specific criteria. This endpoint is extremely powerful for infrastructure discovery and threat hunting.</p> <p><b>Performance Note:</b> Searches on WHOIS fields (like `registrantCompany`) are data-intensive and can take over 50 seconds to complete. This endpoint is therefore asynchronous by design. Poll the `/v1/ops/jobs/{jobId}` endpoint to retrieve results.</p> <h4>Example Search Queries:</h4> <ul>     <li>`registrantCompany:EvilCorp` - Find all domains registered by EvilCorp</li>     <li>`asn:15169` - Find all IPs in Google's ASN</li>     <li>`city:\"San Francisco\"` - Find all IPs geolocated to San Francisco</li> </ul> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **searchRequest** | [**SearchRequest**](SearchRequest.md) | The search query and configuration. |  |

### Return type

[**JobResponse**](JobResponse.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **202** | Search job successfully accepted. |  -  |
| **429** | Rate limit exceeded for search operations. |  -  |
| **401** | Authentication failed. Missing or invalid API key. |  -  |
| **400** | Invalid search query or parameters. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

