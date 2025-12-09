# Whisper.Api.Sdk.Api.AIIntelligenceApi

All URIs are relative to *https://api.whisper.security*

| Method | HTTP request | Description |
|--------|--------------|-------------|
| [**AiAttribute**](AIIntelligenceApi.md#aiattribute) | **POST** /v1/ops/ai/attribute | Threat Actor Attribution (Asynchronous) |
| [**AiCorrelate**](AIIntelligenceApi.md#aicorrelate) | **POST** /v1/ops/ai/correlate | Global Indicator Correlation (Asynchronous) |
| [**AiInvestigate**](AIIntelligenceApi.md#aiinvestigate) | **POST** /v1/ops/ai/investigate | AI Threat Investigation (Asynchronous) |
| [**AiPivot**](AIIntelligenceApi.md#aipivot) | **POST** /v1/ops/ai/pivot | AI Infrastructure Pivot (Asynchronous) |
| [**FindSimilarCases**](AIIntelligenceApi.md#findsimilarcases) | **POST** /v1/ops/ai/similar-cases | Find Similar Cases (Asynchronous) |
| [**GetIndustryBenchmark**](AIIntelligenceApi.md#getindustrybenchmark) | **GET** /v1/ops/ai/benchmark/{industry} | Get Industry Security Benchmark (Synchronous) |

<a id="aiattribute"></a>
# **AiAttribute**
> AttributeResult AiAttribute (AttributeRequest attributeRequest)

Threat Actor Attribution (Asynchronous)

<p>Analyzes indicators and context to identify potential threat actors and campaigns. Uses ML clustering and TTP matching against known threat actor profiles.</p> <h4>Attribution Analysis:</h4> <ul>     <li><b>Actor Identification:</b> Potential threat actor matches with confidence</li>     <li><b>Campaign Clustering:</b> Groups indicators into potential campaigns</li>     <li><b>TTP Mapping:</b> MITRE ATT&CK technique mapping</li>     <li><b>Historical Context:</b> Known actor activity patterns</li> </ul> <h4>Limitations:</h4> <p>Maximum 500 indicators per request. Attribution is probabilistic and should be validated.</p> <h4>Performance:</h4> <p>Campaign clustering and analysis. Expected: 60-300 seconds.</p> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **attributeRequest** | [**AttributeRequest**](AttributeRequest.md) | Attribution request |  |

### Return type

[**AttributeResult**](AttributeResult.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **202** | Attribution analysis job accepted. Poll GET /v1/ops/jobs/{jobId} for results. |  -  |
| **200** | Job result schema (returned via GET /v1/ops/jobs/{jobId} when job completes) |  -  |
| **400** | Invalid request or exceeds 500 indicator limit. |  -  |
| **401** | Authentication failed. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="aicorrelate"></a>
# **AiCorrelate**
> CorrelateResult AiCorrelate (CorrelateRequest correlateRequest)

Global Indicator Correlation (Asynchronous)

<p>Correlates your indicators against anonymized global threat data from all customers. Identifies shared campaigns, widespread threats, and prevalence across industries.</p> <h4>Correlation Analysis:</h4> <ul>     <li><b>Prevalence:</b> How common are these indicators across our customer base</li>     <li><b>Industry Breakdown:</b> Which industries are seeing these indicators</li>     <li><b>Campaign Detection:</b> Are these part of a broader campaign</li>     <li><b>First/Last Seen:</b> Global timeline of indicator activity</li>     <li><b>Co-occurrence:</b> Indicators frequently seen together</li> </ul> <h4>Limitations:</h4> <p>Maximum 100 indicators per request.</p> <h4>Performance:</h4> <p>Cross-customer correlation. Expected: 10-60 seconds.</p> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **correlateRequest** | [**CorrelateRequest**](CorrelateRequest.md) | Correlation request |  |

### Return type

[**CorrelateResult**](CorrelateResult.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **202** | Correlation job accepted. Poll GET /v1/ops/jobs/{jobId} for results. |  -  |
| **200** | Job result schema (returned via GET /v1/ops/jobs/{jobId} when job completes) |  -  |
| **400** | Invalid request or exceeds 100 indicator limit. |  -  |
| **401** | Authentication failed. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="aiinvestigate"></a>
# **AiInvestigate**
> InvestigateResult AiInvestigate (InvestigateRequest investigateRequest)

AI Threat Investigation (Asynchronous)

<p>Initiates a comprehensive AI-powered threat investigation for an indicator. Uses large language models to analyze threat intelligence, generate insights, and provide actionable recommendations.</p> <h4>Investigation Output:</h4> <ul>     <li><b>Verdict:</b> Threat assessment with confidence score</li>     <li><b>Timeline:</b> Activity timeline reconstruction</li>     <li><b>Analysis:</b> Detailed findings from multiple data sources</li>     <li><b>Related Indicators:</b> Discovered related infrastructure</li>     <li><b>Recommendations:</b> Suggested response actions</li> </ul> <h4>Performance:</h4> <p>LLM-based analysis. Expected completion: 30-180 seconds depending on complexity.</p> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **investigateRequest** | [**InvestigateRequest**](InvestigateRequest.md) | Investigation request. Required fields: - **indicator**: The IP, domain, or hash to investigate - **indicatorType**: Must be \&quot;ip\&quot;, \&quot;domain\&quot;, or \&quot;hash\&quot;  Optional fields: - **depth**: Investigation depth (\&quot;quick\&quot;, \&quot;standard\&quot;, \&quot;comprehensive\&quot;). Default: \&quot;standard\&quot; - **context**: Object with optional fields: hypothesis (string), relatedIndicators (array), timeRange (string)  |  |

### Return type

[**InvestigateResult**](InvestigateResult.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **202** | Investigation job accepted. Poll GET /v1/ops/jobs/{jobId} for results. |  -  |
| **200** | Job result schema (returned via GET /v1/ops/jobs/{jobId} when job completes) |  -  |
| **400** | Invalid request. |  -  |
| **401** | Authentication failed. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="aipivot"></a>
# **AiPivot**
> PivotResult AiPivot (PivotRequest pivotRequest)

AI Infrastructure Pivot (Asynchronous)

<p>Performs intelligent infrastructure pivoting starting from an indicator. Uses ML to identify the most relevant relationships and suggest investigation paths.</p> <h4>Pivot Strategies:</h4> <ul>     <li><b>infrastructure:</b> Shared hosting, nameservers, certificates</li>     <li><b>registration:</b> Same registrant, registration patterns</li>     <li><b>behavioral:</b> Similar traffic patterns, communication</li>     <li><b>temporal:</b> Co-occurrence within time windows</li> </ul> <h4>Response Includes:</h4> <ul>     <li>Discovered related indicators with relevance scores</li>     <li>Suggested investigation paths ranked by priority</li>     <li>Relationship graph data</li> </ul> <h4>Performance:</h4> <p>Graph traversal with ML ranking. Expected: 10-120 seconds based on depth.</p> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **pivotRequest** | [**PivotRequest**](PivotRequest.md) | Pivot request |  |

### Return type

[**PivotResult**](PivotResult.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **202** | Pivot analysis job accepted. Poll GET /v1/ops/jobs/{jobId} for results. |  -  |
| **200** | Job result schema (returned via GET /v1/ops/jobs/{jobId} when job completes) |  -  |
| **400** | Invalid request. |  -  |
| **401** | Authentication failed. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="findsimilarcases"></a>
# **FindSimilarCases**
> SimilarCasesResult FindSimilarCases (SimilarCasesRequest similarCasesRequest)

Find Similar Cases (Asynchronous)

<p>Uses ML to find historical threat cases similar to the current investigation. Helps analysts understand attack patterns and expected outcomes.</p> <h4>Matching Criteria:</h4> <ul>     <li>Indicator overlap and relationships</li>     <li>Behavioral patterns and TTPs</li>     <li>Infrastructure characteristics</li>     <li>Attack progression similarities</li> </ul> <h4>Response Includes:</h4> <ul>     <li>Similar cases with similarity scores</li>     <li>Case outcomes and verdicts</li>     <li>Common patterns across matches</li> </ul> <h4>Performance:</h4> <p>ML similarity matching. Expected completion: 5-30 seconds.</p> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **similarCasesRequest** | [**SimilarCasesRequest**](SimilarCasesRequest.md) | Similar cases request |  |

### Return type

[**SimilarCasesResult**](SimilarCasesResult.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **202** | Similar cases search job accepted. Poll GET /v1/ops/jobs/{jobId} for results. |  -  |
| **200** | Job result schema (returned via GET /v1/ops/jobs/{jobId} when job completes) |  -  |
| **400** | Invalid request. |  -  |
| **401** | Authentication failed. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="getindustrybenchmark"></a>
# **GetIndustryBenchmark**
> BenchmarkResponse GetIndustryBenchmark (string industry, string size = null, string region = null)

Get Industry Security Benchmark (Synchronous)

<p>Returns anonymized, aggregated security metrics for your industry vertical. Compare your security posture against peers.</p> <h4>Available Industries:</h4> <ul>     <li>financial_services, healthcare, technology, retail, manufacturing</li>     <li>energy, telecommunications, government, education, media</li> </ul> <h4>Metrics Included:</h4> <ul>     <li><b>Risk Scores:</b> Average risk score, percentiles (25th, 50th, 75th, 90th)</li>     <li><b>Response Metrics:</b> Mean time to detect (MTTD), mean time to respond (MTTR)</li>     <li><b>Detection Metrics:</b> Detection rate, false positive rate</li>     <li><b>Threat Profile:</b> Top threats, common attack vectors, targeted assets</li>     <li><b>Trends:</b> 30-day risk trend direction and change percentage</li> </ul> <h4>Performance:</h4> <p>Pre-aggregated data. Response time typically under 500ms with 1-hour cache.</p> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **industry** | **string** | Industry vertical code |  |
| **size** | **string** | Organization size filter. Compares against organizations of similar size. | [optional]  |
| **region** | **string** | Geographic region filter. Compares against organizations in the same region. | [optional]  |

### Return type

[**BenchmarkResponse**](BenchmarkResponse.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Successfully retrieved industry benchmark. |  -  |
| **400** | Invalid industry code. |  -  |
| **401** | Authentication failed. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

