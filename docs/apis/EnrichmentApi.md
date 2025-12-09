# Whisper.Api.Sdk.Api.EnrichmentApi

All URIs are relative to *https://api.whisper.security*

| Method | HTTP request | Description |
|--------|--------------|-------------|
| [**BulkEnrichment**](EnrichmentApi.md#bulkenrichment) | **POST** /v1/ops/enrichment/bulk | Bulk Indicator Enrichment (Asynchronous) |
| [**GetIndicator**](EnrichmentApi.md#getindicator) | **GET** /v1/indicators/{type}/{value} | Enrich a Single Indicator (IP or Domain) |
| [**GetIndicatorGraph**](EnrichmentApi.md#getindicatorgraph) | **GET** /v1/indicators/{type}/{value}/graph | Get Infrastructure Relationship Graph |
| [**GetIndicatorHistory**](EnrichmentApi.md#getindicatorhistory) | **GET** /v1/indicators/{type}/{value}/history | Get Historical Data for Indicator |
| [**GetPredictiveRisk**](EnrichmentApi.md#getpredictiverisk) | **GET** /v1/indicators/{type}/{value}/predictive-risk | Get AI Predictive Risk Score |
| [**GetSubdomains**](EnrichmentApi.md#getsubdomains) | **GET** /v1/indicators/domain/{domain}/subdomains | Get Domain Subdomains |
| [**SearchIndicators**](EnrichmentApi.md#searchindicators) | **POST** /v1/ops/enrichment/search | Search WHOIS and Geolocation Records (Asynchronous) |
| [**SimilarDomains**](EnrichmentApi.md#similardomains) | **POST** /v1/ops/enrichment/similar-domains | Find Similar Domains (Asynchronous) |

<a id="bulkenrichment"></a>
# **BulkEnrichment**
> BulkEnrichmentResult BulkEnrichment (BulkRequest bulkRequest)

Bulk Indicator Enrichment (Asynchronous)

<p>Process multiple indicators (IPs and/or domains) in a single request. This endpoint is optimized for batch processing and can handle up to 100 indicators per request.</p>  <h4>Performance</h4> <p>Processing time depends on batch size and indicator types. IP enrichment is faster than domain enrichment.</p> <ul>     <li><b>IPs only:</b> 2-10 seconds for typical batches</li>     <li><b>Domains only:</b> 10-30 seconds (WHOIS lookups are slower)</li>     <li><b>Mixed:</b> 5-30 seconds depending on ratio</li> </ul>  <h4>Rate Limits</h4> <p>Limited to 10 requests per minute due to the resource-intensive nature of bulk operations.</p>  <h4>Response Structure</h4> <p>When the job completes, the <code>result</code> field contains:</p> <ul>     <li><code>status</code>: \"completed\" or \"failed\"</li>     <li><code>results</code>: Array of enriched indicator objects (see below)</li>     <li><code>errors</code>: Array of failed enrichments with error details</li>     <li><code>totalProcessed</code>: Number of indicators processed</li>     <li><code>totalFailed</code>: Number of failed enrichments</li>     <li><code>totalIndicators</code>: Total indicators in request</li>     <li><code>successRate</code>: Percentage of successful enrichments (0-100)</li> </ul>  <h4>Result Item Structure</h4> <p>Each item in the <code>results</code> array includes:</p> <ul>     <li><code>indicator</code>: The original indicator value</li>     <li><code>type</code>: \"ip\" or \"domain\"</li>     <li><code>query</code>: Request metadata (type, value, timestamp, response_time_ms)</li>     <li><code>summary</code>: Key information summary</li> </ul>  <p><b>For IP indicators:</b></p> <ul>     <li><code>geolocation</code>: Country, city, coordinates, ISP, ASN</li>     <li><code>network</code>: BGP routing data, prefix visibility, origins</li>     <li><code>isp</code>: ISP name, organization, ASN</li>     <li><code>reputation</code>: Risk score, blacklist scores</li>     <li><code>relationships</code>: Related domains, shared infrastructure</li> </ul>  <p><b>For domain indicators:</b></p> <ul>     <li><code>registration</code>: WHOIS data (registrar, dates, nameservers, status)</li>     <li><code>dns</code>: DNS records (A, AAAA, MX, NS, TXT, CNAME)</li>     <li><code>reputation</code>: Domain reputation, infrastructure scores</li>     <li><code>relationships</code>: Related domains, incoming/outgoing links</li> </ul>  <h4>Error Item Structure</h4> <p>Each item in the <code>errors</code> array includes:</p> <ul>     <li><code>indicator</code>: The indicator that failed</li>     <li><code>type</code>: \"ip\" or \"domain\"</li>     <li><code>error</code>: true</li>     <li><code>message</code>: Error description</li> </ul> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **bulkRequest** | [**BulkRequest**](BulkRequest.md) | List of indicators and processing options. |  |

### Return type

[**BulkEnrichmentResult**](BulkEnrichmentResult.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **202** | Bulk job successfully accepted for processing. Poll GET /v1/ops/jobs/{jobId} for results. |  -  |
| **200** | Job result schema (returned via GET /v1/ops/jobs/{jobId} when job completes). See endpoint description for detailed result structure. |  -  |
| **400** | Invalid request. Empty indicator list or exceeds 100 indicator limit. |  -  |
| **401** | Authentication failed. Missing or invalid API key. |  -  |
| **429** | Rate limit exceeded for bulk operations. |  -  |

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
| **include** | **string** | A comma-separated list of additional data modules to include in the response. Note: WHOIS and DNS data are included by default for domains. Requesting more modules may increase latency. | [optional]  |

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
| **200** | Successfully retrieved intelligence data. |  -  |
| **400** | Invalid indicator format or unsupported type. |  -  |
| **401** | Authentication failed. Missing or invalid API key. |  -  |
| **404** | The requested indicator was not found in our datasets. |  -  |
| **429** | Rate limit exceeded. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="getindicatorgraph"></a>
# **GetIndicatorGraph**
> GraphResponse GetIndicatorGraph (string type, string value, int limit = null)

Get Infrastructure Relationship Graph

<p>Returns graph visualization data showing relationships between the indicator and related infrastructure. Perfect for interactive network diagrams and threat actor infrastructure mapping.</p> <h4>Relationship Types Included:</h4> <ul>     <li><b>For Domains:</b>         <ul>             <li>Resolves to IPs</li>             <li>Shares nameservers with</li>             <li>Same SSL certificate as</li>             <li>Same registrant as</li>             <li>Links to/from other domains</li>         </ul>     </li>     <li><b>For IPs:</b>         <ul>             <li>Hosts domains</li>             <li>Same ASN as</li>             <li>Same network block as</li>             <li>Connected via routing</li>         </ul>     </li> </ul> <h4>Output Format:</h4> <p>Compatible with react-force-graph, vis.js, cytoscape.js:</p> <pre><code>{   \"nodes\": [     {\"id\": \"example.com\", \"type\": \"domain\", \"label\": \"example.com\"},     {\"id\": \"8.8.8.8\", \"type\": \"ip\", \"label\": \"8.8.8.8\"}   ],   \"links\": [     {\"source\": \"example.com\", \"target\": \"8.8.8.8\", \"type\": \"resolves_to\"}   ] }</code></pre> <h4>Performance:</h4> <ul>     <li>Response Time: 500ms-2s depending on graph complexity</li>     <li>Default: 100 nodes maximum (adjustable)</li> </ul> <h4>Use Cases:</h4> <ul>     <li>Interactive threat actor infrastructure visualization</li>     <li>Discovering related phishing campaigns</li>     <li>Mapping shadow IT and sprawl</li>     <li>Network topology visualization</li> </ul> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **type** | **string** | Type of indicator |  |
| **value** | **string** | The indicator value (IP address or domain) |  |
| **limit** | **int** | Maximum number of nodes to return in the graph | [optional] [default to 100] |

### Return type

[**GraphResponse**](GraphResponse.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Successfully retrieved graph data. Compatible with react-force-graph, vis.js, and cytoscape.js. |  -  |
| **400** | Invalid indicator type or limit parameter. Type must be &#39;ip&#39; or &#39;domain&#39;, limit must be 1-500. |  -  |
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
| **200** | Successfully retrieved historical data. |  -  |
| **400** | Invalid indicator type or history type. |  -  |
| **401** | Authentication failed. Missing or invalid API key. |  -  |
| **404** | No historical data found for this indicator. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="getpredictiverisk"></a>
# **GetPredictiveRisk**
> PredictiveRiskResponse GetPredictiveRisk (string type, string value)

Get AI Predictive Risk Score

<p>Returns ML-based predictive risk assessment for an IP address or domain. Provides current risk scoring, 7-day and 30-day predictions, risk trajectory analysis, and contributing factors.</p> <h4>Response Includes:</h4> <ul>     <li><b>Current Assessment:</b> Risk score (0-100), risk level, and confidence</li>     <li><b>Predictions:</b> 7-day and 30-day risk forecasts with confidence intervals</li>     <li><b>Trajectory:</b> Trend direction (improving/stable/worsening), velocity, stability</li>     <li><b>Risk Factors:</b> Contributing factors with weights and descriptions</li>     <li><b>Early Warnings:</b> Signals indicating potential future risk changes</li>     <li><b>Similar Cases:</b> Historical indicators with similar profiles and their outcomes</li> </ul> <h4>Risk Levels:</h4> <ul>     <li><b>low:</b> Score 0-30 - Minimal observed risk</li>     <li><b>medium:</b> Score 31-60 - Moderate risk, warrants monitoring</li>     <li><b>high:</b> Score 61-80 - Elevated risk, investigation recommended</li>     <li><b>critical:</b> Score 81-100 - Severe risk, immediate action advised</li> </ul> <h4>Performance:</h4> <p>Pre-computed ML predictions. Response time typically under 500ms with 15-minute cache.</p> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **type** | **string** | Type of indicator |  |
| **value** | **string** | The indicator value (IP address or domain) |  |

### Return type

[**PredictiveRiskResponse**](PredictiveRiskResponse.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Successfully retrieved predictive risk assessment. |  -  |
| **400** | Invalid indicator type or value. |  -  |
| **401** | Authentication failed. Missing or invalid API key. |  -  |
| **404** | Indicator not found in AI model data. |  -  |

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
| **200** | Successfully retrieved subdomains. |  -  |
| **400** | Invalid domain format. |  -  |
| **401** | Authentication failed. Missing or invalid API key. |  -  |
| **404** | Domain not found or no subdomains discovered. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="searchindicators"></a>
# **SearchIndicators**
> SearchResponse SearchIndicators (SearchRequest searchRequest)

Search WHOIS and Geolocation Records (Asynchronous)

            <p>Initiates an asynchronous job to search domain registration (WHOIS) or IP geolocation records. This endpoint is extremely powerful for infrastructure discovery, threat hunting, and brand protection.</p>             <p><b>Performance Note:</b> WHOIS searches are data-intensive and can take over 50 seconds to complete. Geolocation searches are faster (5-10 seconds). This endpoint is asynchronous by design. Poll the <code>/v1/ops/jobs/{jobId}</code> endpoint to retrieve results.</p>              <h4>Search Types:</h4>             <p>The endpoint automatically routes to the appropriate backend based on the fields provided:</p>             <ul>                 <li><b>WHOIS Search:</b> Use registrant fields (registrantCompany, registrantEmail, etc.) or domain-related fields (tld, nameServer, etc.)</li>                 <li><b>Geolocation Search:</b> Use IP geolocation fields (city, country, asn, isp, etc.) to find IPs matching criteria</li>             </ul>              <h4>WHOIS Search Fields:</h4>             <table>                 <tr><th>Field</th><th>Type</th><th>Description</th></tr>                 <tr><td><code>tld</code></td><td>exact</td><td>Top-level domain (e.g., \"com\", \"org\", \"net\")</td></tr>                 <tr><td><code>registrarName</code></td><td>exact</td><td>Domain registrar name</td></tr>                 <tr><td><code>registrarIanaId</code></td><td>exact</td><td>IANA registrar ID</td></tr>                 <tr><td><code>registrantName</code></td><td>text</td><td>Domain registrant name (partial match)</td></tr>                 <tr><td><code>registrantCompany</code></td><td>text</td><td>Registrant organization/company (partial match)</td></tr>                 <tr><td><code>registrantEmail</code></td><td>text</td><td>Registrant email address (supports *@domain.com wildcards)</td></tr>                 <tr><td><code>registrantPhone</code></td><td>text</td><td>Registrant phone number</td></tr>                 <tr><td><code>registrantCountry</code></td><td>text</td><td>2-letter country code (e.g., \"US\", \"DE\")</td></tr>                 <tr><td><code>registrantCity</code></td><td>text</td><td>Registrant city</td></tr>                 <tr><td><code>nameServer</code></td><td>text</td><td>Name server hostname</td></tr>                 <tr><td><code>domainStatus</code></td><td>text</td><td>Domain status flag (e.g., \"clientTransferProhibited\")</td></tr>                 <tr><td><code>createdDate</code></td><td>exact</td><td>Domain creation date (YYYY-MM-DD format)</td></tr>                 <tr><td><code>updatedDate</code></td><td>exact</td><td>Domain last update date (YYYY-MM-DD format)</td></tr>                 <tr><td><code>expiryDate</code></td><td>exact</td><td>Domain expiry date (YYYY-MM-DD format)</td></tr>             </table>              <h4>Geolocation Search Fields (query string syntax):</h4>             <table>                 <tr><th>Field</th><th>Description</th><th>Example</th></tr>                 <tr><td><code>city</code></td><td>City name</td><td><code>city:London</code></td></tr>                 <tr><td><code>country</code></td><td>Country name</td><td><code>country:Germany</code></td></tr>                 <tr><td><code>asn</code></td><td>Autonomous System Number</td><td><code>asn:15169</code> (Google)</td></tr>                 <tr><td><code>isp</code></td><td>Internet Service Provider name</td><td><code>isp:Cloudflare</code></td></tr>                 <tr><td><code>organization</code></td><td>Organization name</td><td><code>organization:Amazon</code></td></tr>                 <tr><td><code>region</code></td><td>Region/State</td><td><code>region:California</code></td></tr>                 <tr><td><code>postal_code</code></td><td>Postal/ZIP code</td><td><code>postal_code:94043</code></td></tr>                 <tr><td><code>continent</code></td><td>Continent</td><td><code>continent:Europe</code></td></tr>             </table>              <h4>Example Requests:</h4>             <p><b>WHOIS search (field-based):</b></p>             <pre>{   \"registrantCompany\": \"Google\",   \"registrantCountry\": \"US\",   \"limit\": 100,   \"page\": 0 }</pre>             <p><b>Geolocation search (find IPs by ASN):</b></p>             <pre>{   \"query\": \"asn:15169\",   \"limit\": 100 }</pre>             <p><b>Geolocation search (find IPs by city):</b></p>             <pre>{   \"query\": \"city:Mountain View\",   \"limit\": 100 }</pre>             <p><b>Date-based domain search:</b></p>             <pre>{   \"createdDate\": \"2024-01-15\",   \"tld\": \"com\",   \"limit\": 100 }</pre>              <h4>Pagination:</h4>             <ul>                 <li><code>limit</code>: Maximum 100 results per page (default: 100)</li>                 <li><code>page</code>: 0-indexed page number (default: 0)</li>                 <li><code>offset</code>: Alternative to page - number of results to skip</li>             </ul>              <h4>Use Cases:</h4>             <ul>                 <li><b>Threat hunting:</b> Find domains/IPs registered by known malicious actors</li>                 <li><b>Infrastructure mapping:</b> Find all IPs in a specific ASN or organization</li>                 <li><b>Brand protection:</b> Monitor for domains similar to your brand</li>                 <li><b>Geolocation analysis:</b> Find IPs in specific geographic regions</li>                 <li><b>Investigation:</b> Track domains created on specific dates or IPs from specific ISPs</li>             </ul>              <h4>Security:</h4>             <p>All search parameters are validated for:</p>             <ul>                 <li>SQL injection prevention</li>                 <li>Command injection prevention</li>                 <li>Input length limits</li>                 <li>Format validation (dates, emails, country codes, etc.)</li>             </ul> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **searchRequest** | [**SearchRequest**](SearchRequest.md) | The search query and configuration. |  |

### Return type

[**SearchResponse**](SearchResponse.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **202** | Search job successfully accepted. Poll GET /v1/ops/jobs/{jobId} to retrieve results. When completed, the job&#39;s &#x60;result&#x60; field contains a SearchResponse object. |  -  |
| **200** | Job result schema (returned via GET /v1/ops/jobs/{jobId} when status&#x3D;COMPLETED). This is NOT returned by this endpoint directly, but documents the final result structure. |  -  |
| **400** | Invalid search query or parameters. |  -  |
| **401** | Authentication failed. Missing or invalid API key. |  -  |
| **429** | Rate limit exceeded for search operations. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="similardomains"></a>
# **SimilarDomains**
> SimilarDomainsResponse SimilarDomains (SimilarDomainsOpsRequest similarDomainsOpsRequest)

Find Similar Domains (Asynchronous)

<p>Finds domains similar to the provided domain using various similarity detection techniques. This endpoint is useful for brand protection, typosquatting detection, and threat hunting.</p>  <h4>Supported Techniques:</h4> <p>Specify techniques in the <code>techniques</code> array. If not specified, defaults to <code>typosquatting</code>.</p> <ul>     <li><b>typosquatting</b> - Keyboard proximity errors and common typos (e.g., gooogle.com, gogle.com)</li>     <li><b>homoglyph</b> - Visually similar Unicode characters (e.g., gооgle.com using Cyrillic 'о')</li>     <li><b>tld_variation</b> - Different TLD variations (e.g., google.net, google.org)</li>     <li><b>sounding</b> - Phonetically similar domains</li>     <li><b>prefix</b> - Domains starting with the target</li>     <li><b>suffix</b> - Domains ending with the target</li>     <li><b>contains</b> - Domains containing the target as a substring</li>     <li><b>levenshtein</b> - Edit distance similarity</li> </ul>  <h4>Example Request:</h4> <pre><code>{   \"domain\": \"google.com\",   \"techniques\": [\"typosquatting\", \"homoglyph\", \"tld_variation\"],   \"limit\": 100 }</code></pre>  <h4>Response Format:</h4> <p>Poll <code>/v1/ops/jobs/{jobId}</code> to get results. The result contains:</p> <pre><code>{   \"domain\": \"google.com\",   \"status\": \"completed\",   \"similarDomains\": [     {\"domain\": \"gooogle.com\", \"technique\": \"TYPO\"},     {\"domain\": \"gооgle.com\", \"technique\": \"UTFVARS\"}   ],   \"totalCount\": 200,   \"analysis\": {     \"techniquesUsed\": \"TYPO,UTFVARS\",     \"baseDomain\": \"google.com\",     \"searchLimit\": 100   } }</code></pre>  <h4>Performance:</h4> <p>Typically completes in 5-15 seconds. Multiple techniques run in parallel.</p>  <h4>Note:</h4> <p>The <code>check_registration</code>, <code>include_dns</code>, and <code>include_risk_score</code> options are not currently supported by the backend service and will be ignored.</p> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **similarDomainsOpsRequest** | [**SimilarDomainsOpsRequest**](SimilarDomainsOpsRequest.md) | Similar domains request with domain and options. |  |

### Return type

[**SimilarDomainsResponse**](SimilarDomainsResponse.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **202** | Similar domains job created successfully. Poll GET /v1/ops/jobs/{jobId} to retrieve results. When completed, the job&#39;s &#x60;result&#x60; field contains a SimilarDomainsResponse object. |  -  |
| **200** | Job result schema (returned via GET /v1/ops/jobs/{jobId} when status&#x3D;COMPLETED). This is NOT returned by this endpoint directly, but documents the final result structure. |  -  |
| **400** | Invalid domain or options. |  -  |
| **401** | Authentication failed. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

