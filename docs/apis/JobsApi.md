# Whisper.Api.Sdk.Api.JobsApi

All URIs are relative to *https://api.whisper.security*

| Method | HTTP request | Description |
|--------|--------------|-------------|
| [**GetJob**](JobsApi.md#getjob) | **GET** /v1/ops/jobs/{jobId} | Get Asynchronous Job Status and Results |
| [**ListJobs**](JobsApi.md#listjobs) | **GET** /v1/ops/jobs/list | List Recent Jobs |

<a id="getjob"></a>
# **GetJob**
> Job GetJob (string jobId)

Get Asynchronous Job Status and Results

<p>Retrieves the current status and results of an asynchronous job. Poll this endpoint to check job progress.</p> <h4>Polling Recommendations:</h4> <ul>     <li>For fast jobs (e.g., similar domains), poll every 1-2 seconds.</li>     <li>For slow jobs (e.g., WHOIS search, screenshots), poll every 5-10 seconds.</li>     <li>Implement an exponential backoff strategy for very long-running jobs.</li>     <li>Stop polling when the status is `COMPLETED`, `FAILED`, or `CANCELLED`.</li> </ul> <h4>Job Statuses:</h4> <ul>     <li><b>PENDING:</b> Job is queued and waiting to start.</li>     <li><b>PROCESSING:</b> Job is actively being processed.</li>     <li><b>COMPLETED:</b> Job finished successfully, results are available.</li>     <li><b>FAILED:</b> Job failed with an error.</li>     <li><b>CANCELLED:</b> Job was cancelled by user or system.</li> </ul> <h4>Result Schemas by Job Type:</h4> <ul>     <li><b>ai-investigate:</b> InvestigateResult - verdict, timeline, analysis, recommendations</li>     <li><b>ai-pivot:</b> PivotResult - related indicators, investigation paths, relationship graph</li>     <li><b>ai-attribute:</b> AttributeResult - actor identification, campaign clustering, TTP mapping</li>     <li><b>ai-correlate:</b> CorrelateResult - prevalence, industry breakdown, co-occurrence</li>     <li><b>ai-similar-cases:</b> SimilarCasesResult - similar cases with similarity scores</li>     <li><b>screenshot:</b> ScreenshotResult - screenshot URL, ID, capture time, metadata</li> </ul> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **jobId** | **string** | The unique ID of the job, returned from a &#x60;POST&#x60; operation. |  |

### Return type

[**Job**](Job.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Job status and results retrieved successfully. |  -  |
| **401** | Authentication failed. Missing or invalid API key. |  -  |
| **404** | Job ID not found. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="listjobs"></a>
# **ListJobs**
> JobListResponse ListJobs (string status = null, int limit = null, int offset = null)

List Recent Jobs

<p>Retrieves a list of recent jobs for the authenticated user, optionally filtered by status.</p> <h4>Query Parameters:</h4> <ul>     <li><b>status:</b> Filter by job status (PENDING, PROCESSING, COMPLETED, FAILED, CANCELLED)</li>     <li><b>limit:</b> Maximum number of jobs to return (default: 50, max: 100)</li>     <li><b>offset:</b> Number of jobs to skip for pagination (default: 0)</li> </ul> <h4>Response Format:</h4> <p>Returns a JSON object with a \"jobs\" array containing job summaries.</p> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **status** | **string** | Filter by job status | [optional]  |
| **limit** | **int** | Maximum number of jobs to return | [optional] [default to 50] |
| **offset** | **int** | Number of jobs to skip | [optional] [default to 0] |

### Return type

[**JobListResponse**](JobListResponse.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Successfully retrieved job list. |  -  |
| **401** | Authentication failed. Missing or invalid API key. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

