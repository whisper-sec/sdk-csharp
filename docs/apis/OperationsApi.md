# Whisper.Api.Sdk.Api.OperationsApi

All URIs are relative to *http://api.whisper.security*

| Method | HTTP request | Description |
|--------|--------------|-------------|
| [**BulkEnrichment**](OperationsApi.md#bulkenrichment) | **POST** /v1/ops/enrichment/bulk | Bulk Indicator Enrichment (Asynchronous) |
| [**CreateInfrastructureMap**](OperationsApi.md#createinfrastructuremap) | **POST** /v1/ops/scans/map | Map Infrastructure Relationships (Asynchronous) |
| [**CreateInfrastructureScan**](OperationsApi.md#createinfrastructurescan) | **POST** /v1/ops/scans/infrastructure | Infrastructure Security Scan (Asynchronous) |
| [**CreateMonitorCheck**](OperationsApi.md#createmonitorcheck) | **POST** /v1/ops/monitoring | Create Monitoring Check |
| [**CreateMonitoringAlert**](OperationsApi.md#createmonitoringalert) | **POST** /v1/ops/monitoring/{target}/alert | Configure Monitoring Alerts (Asynchronous) |
| [**CreateScreenshot**](OperationsApi.md#createscreenshot) | **POST** /v1/ops/screenshots/capture | Capture a Website Screenshot (Asynchronous) |
| [**DeleteMonitorCheck**](OperationsApi.md#deletemonitorcheck) | **DELETE** /v1/ops/monitoring/{checkId} | Delete Monitoring Check |
| [**GetChanges**](OperationsApi.md#getchanges) | **GET** /v1/ops/tracking/{type}/{value} | Get Detected Changes |
| [**GetJob**](OperationsApi.md#getjob) | **GET** /v1/ops/jobs/{jobId} | Get Asynchronous Job Status and Results |
| [**GetMonitorCheck**](OperationsApi.md#getmonitorcheck) | **GET** /v1/ops/monitoring/{checkId} | Get Monitoring Check |
| [**GetMonitorDashboard**](OperationsApi.md#getmonitordashboard) | **GET** /v1/ops/monitoring/dashboard | Get Monitoring Dashboard |
| [**GetMonitorResults**](OperationsApi.md#getmonitorresults) | **GET** /v1/ops/monitoring/{checkId}/results | Get Check Results |
| [**GetMonitoringStatus**](OperationsApi.md#getmonitoringstatus) | **GET** /v1/ops/monitoring/status/{target} | Get Monitoring Status and Metrics |
| [**GetScreenshotHistory**](OperationsApi.md#getscreenshothistory) | **GET** /v1/ops/screenshots/history | Get Screenshot History |
| [**ListJobs**](OperationsApi.md#listjobs) | **GET** /v1/ops/jobs/list | List Recent Jobs |
| [**ListMonitorChecks**](OperationsApi.md#listmonitorchecks) | **GET** /v1/ops/monitoring | List Monitoring Checks |
| [**ListTrackedIndicators**](OperationsApi.md#listtrackedindicators) | **GET** /v1/ops/tracking | List Tracked Indicators |
| [**ScheduleScreenshot**](OperationsApi.md#schedulescreenshot) | **POST** /v1/ops/screenshots/schedule | Schedule Recurring Screenshots (Asynchronous) |
| [**SearchIndicators**](OperationsApi.md#searchindicators) | **POST** /v1/ops/enrichment/search | Search Indicators (Asynchronous) |
| [**SimilarDomains**](OperationsApi.md#similardomains) | **POST** /v1/ops/enrichment/similar-domains | Find Similar Domains (Asynchronous) |
| [**StartChangeTracking**](OperationsApi.md#startchangetracking) | **POST** /v1/ops/tracking/{type}/{value} | Start Change Tracking |
| [**StopChangeTracking**](OperationsApi.md#stopchangetracking) | **DELETE** /v1/ops/tracking/{type}/{value} | Stop Change Tracking |
| [**TriggerCheck**](OperationsApi.md#triggercheck) | **POST** /v1/ops/tracking/{type}/{value}/check | Trigger Immediate Check |
| [**TriggerMonitorCheck**](OperationsApi.md#triggermonitorcheck) | **POST** /v1/ops/monitoring/{checkId}/trigger | Trigger Manual Check |
| [**UpdateMonitorCheck**](OperationsApi.md#updatemonitorcheck) | **PUT** /v1/ops/monitoring/{checkId} | Update Monitoring Check |

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
| **400** | Invalid request. Empty indicator list or exceeds 100 indicator limit. |  -  |
| **429** | Rate limit exceeded for bulk operations. |  -  |
| **401** | Authentication failed. Missing or invalid API key. |  -  |
| **202** | Bulk job successfully accepted for processing. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="createinfrastructuremap"></a>
# **CreateInfrastructureMap**
> JobResponse CreateInfrastructureMap (InfrastructureMapRequest infrastructureMapRequest)

Map Infrastructure Relationships (Asynchronous)

<p>Creates a comprehensive map of infrastructure relationships starting from a domain or IP. Discovers connected assets through shared hosting, DNS, certificates, and network relationships.</p> <h4>Mapping Depth Levels:</h4> <ul>     <li><b>Depth 1:</b> Direct relationships only (~30 seconds, 10-50 assets)</li>     <li><b>Depth 2:</b> 2 hops out (~2-5 minutes, 50-500 assets)</li>     <li><b>Depth 3:</b> 3 hops out (~10-30 minutes, 500-5000 assets)</li> </ul> <h4>Relationship Types Discovered:</h4> <ul>     <li>Domains on same IP</li>     <li>Domains sharing nameservers</li>     <li>Domains with same SSL certificate</li>     <li>IPs in same ASN</li>     <li>Domains with same registrant</li> </ul> <h4>Output Format:</h4> <p>Results returned as graph data compatible with visualization libraries (nodes and edges).</p> <h4>Use Cases:</h4> <ul>     <li>Threat actor infrastructure mapping</li>     <li>Discovering related phishing domains</li>     <li>Finding shadow IT and forgotten assets</li> </ul> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **infrastructureMapRequest** | [**InfrastructureMapRequest**](InfrastructureMapRequest.md) | Mapping configuration. Example: &#x60;&#x60;&#x60;json {   \&quot;startPoint\&quot;: \&quot;example.com\&quot;,   \&quot;depth\&quot;: 2 } &#x60;&#x60;&#x60;  |  |

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
| **202** | Mapping job successfully accepted. Poll &#x60;/v1/ops/jobs/{jobId}&#x60; for results. |  -  |
| **401** | Authentication failed. Missing or invalid API key. |  -  |
| **400** | Invalid starting point or depth (must be 1-3). |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="createinfrastructurescan"></a>
# **CreateInfrastructureScan**
> JobResponse CreateInfrastructureScan (ScanRequest scanRequest)

Infrastructure Security Scan (Asynchronous)

<p>Initiates a comprehensive security scan of a domain's infrastructure. Performs reconnaissance, port scanning, service detection, and vulnerability assessment.</p> <h4>Scan Types:</h4> <ul>     <li><b>comprehensive:</b> Full scan including all modules (recommended for complete assessment)</li>     <li><b>subdomains:</b> Subdomain enumeration only</li>     <li><b>ports:</b> Port scanning and service detection</li>     <li><b>technologies:</b> Technology stack detection</li>     <li><b>vulnerabilities:</b> Known vulnerability checks</li>     <li><b>ssl:</b> SSL/TLS configuration and certificate analysis</li>     <li><b>dns:</b> DNS configuration and zone transfer tests</li>     <li><b>whois:</b> Registration and ownership information</li> </ul> <h4>Performance:</h4> <ul>     <li><b>Quick scans:</b> 30-60 seconds (subdomains, dns, whois)</li>     <li><b>Comprehensive scan:</b> 5-15 minutes depending on infrastructure size</li> </ul> <h4>Use Cases:</h4> <ul>     <li>Pre-engagement reconnaissance for penetration testing</li>     <li>Attack surface assessment</li>     <li>Infrastructure inventory and mapping</li>     <li>Vulnerability management</li> </ul> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **scanRequest** | [**ScanRequest**](ScanRequest.md) | Scan configuration including target domain and scan type. |  |

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
| **202** | Scan job successfully accepted. Poll &#x60;/v1/ops/jobs/{jobId}&#x60; for results. |  -  |
| **401** | Authentication failed. Missing or invalid API key. |  -  |
| **400** | Invalid domain or scan type. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="createmonitorcheck"></a>
# **CreateMonitorCheck**
> MonitorCheckResponse CreateMonitorCheck (MonitorCheckRequest monitorCheckRequest)

Create Monitoring Check

<p>Create a new monitoring check to track uptime and performance of a URL or endpoint.</p> <h4>Check Types:</h4> <ul>     <li><b>api:</b> HTTP/HTTPS endpoint monitoring - checks status code, response time, content</li>     <li><b>ssl:</b> SSL certificate monitoring - validates certificate and tracks expiry</li>     <li><b>dns:</b> DNS record monitoring - validates DNS resolution and record values</li> </ul> <h4>Frequency Options:</h4> <p>Check frequency in minutes: 1, 5, 10, 15, 30, 60, 1440 (daily)</p> <h4>Locations:</h4> <p>Checks can run from multiple global locations: us-east-1, us-west-1, eu-west-1, ap-southeast-1</p> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **monitorCheckRequest** | [**MonitorCheckRequest**](MonitorCheckRequest.md) | Monitoring check configuration |  |

### Return type

[**MonitorCheckResponse**](MonitorCheckResponse.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **401** | Authentication failed. |  -  |
| **201** | Monitoring check created successfully. |  -  |
| **400** | Invalid request - missing name or URL. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="createmonitoringalert"></a>
# **CreateMonitoringAlert**
> JobResponse CreateMonitoringAlert (string target, MonitoringAlertRequest monitoringAlertRequest)

Configure Monitoring Alerts (Asynchronous)

<p>Create alert rules for a monitored asset. Get notified via webhook, email, or Slack when specific conditions are met.</p> <h4>Alert Types:</h4> <ul>     <li><b>downtime:</b> Site becomes unreachable</li>     <li><b>dns_change:</b> DNS records modified</li>     <li><b>whois_change:</b> Registration details updated</li>     <li><b>ssl_expiring:</b> Certificate expires soon (7, 14, 30 days)</li>     <li><b>content_change:</b> Page content modified</li>     <li><b>technology_change:</b> Tech stack changes detected</li> </ul> <h4>Notification Channels:</h4> <ul>     <li>Webhook (POST to your endpoint)</li>     <li>Email</li>     <li>Slack</li>     <li>PagerDuty</li> </ul> <h4>Example Configuration:</h4> <pre><code>{   \"type\": \"ssl_expiring\",   \"threshold_days\": 14,   \"channels\": [\"email\", \"slack\"],   \"email\": \"alerts@example.com\",   \"slack_webhook\": \"https://hooks.slack.com/...\" }</code></pre> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **target** | **string** | The domain or IP address to configure alerts for. |  |
| **monitoringAlertRequest** | [**MonitoringAlertRequest**](MonitoringAlertRequest.md) | Alert configuration including type, thresholds, and notification channels. |  |

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
| **401** | Authentication failed. Missing or invalid API key. |  -  |
| **202** | Alert configuration job accepted. Poll &#x60;/v1/ops/jobs/{jobId}&#x60; for status. |  -  |
| **400** | Invalid alert configuration. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="createscreenshot"></a>
# **CreateScreenshot**
> JobResponse CreateScreenshot (ScreenshotRequest screenshotRequest)

Capture a Website Screenshot (Asynchronous)

<p>Initiates an asynchronous job to capture a screenshot of a website. Supports various viewport sizes, full-page captures, and JavaScript rendering.</p> <p><b>Performance Note:</b> A typical screenshot capture takes 10-30 seconds. Poll the `/v1/ops/jobs/{jobId}` endpoint to retrieve the URL of the final image.</p> <p><b>Output:</b> The job result will contain a URL to download the screenshot image in the specified format (PNG, JPEG, or WebP).</p> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **screenshotRequest** | [**ScreenshotRequest**](ScreenshotRequest.md) | The URL and options for the screenshot capture. |  |

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
| **202** | Screenshot job successfully accepted. |  -  |
| **400** | Invalid URL or options provided. |  -  |
| **401** | Authentication failed. Missing or invalid API key. |  -  |
| **429** | Rate limit exceeded. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="deletemonitorcheck"></a>
# **DeleteMonitorCheck**
> void DeleteMonitorCheck (string checkId)

Delete Monitoring Check

Delete a monitoring check and stop all monitoring for the target.


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **checkId** | **string** | Check ID |  |

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
| **401** | Authentication failed. |  -  |
| **404** | Check not found or access denied. |  -  |
| **204** | Check deleted successfully. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="getchanges"></a>
# **GetChanges**
> ChangeTrackingResponse GetChanges (string type, string value, string since = null)

Get Detected Changes

<p>Retrieve detected changes for a tracked indicator. Returns the current tracking configuration, baseline snapshot, and list of all detected changes.</p> <h4>Response Includes:</h4> <ul>     <li><b>tracking:</b> Current tracking configuration (enabled, frequency, fields, next check)</li>     <li><b>baseline:</b> The stored baseline snapshot data</li>     <li><b>changes:</b> Array of detected changes with timestamps, old/new values</li>     <li><b>totalChanges:</b> Total number of changes detected</li> </ul> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **type** | **string** | Indicator type: ip or domain |  |
| **value** | **string** | Indicator value |  |
| **since** | **string** | ISO 8601 timestamp to get changes from | [optional]  |

### Return type

[**ChangeTrackingResponse**](ChangeTrackingResponse.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **401** | Authentication failed. |  -  |
| **200** | Successfully retrieved changes. |  -  |
| **404** | Indicator is not being tracked. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="getjob"></a>
# **GetJob**
> Job GetJob (string jobId)

Get Asynchronous Job Status and Results

<p>Retrieves the current status and results of an asynchronous job. Poll this endpoint to check job progress.</p> <h4>Polling Recommendations:</h4> <ul>     <li>For fast jobs (e.g., similar domains), poll every 1-2 seconds.</li>     <li>For slow jobs (e.g., WHOIS search, screenshots), poll every 5-10 seconds.</li>     <li>Implement an exponential backoff strategy for very long-running jobs.</li>     <li>Stop polling when the status is `COMPLETED`, `FAILED`, or `CANCELLED`.</li> </ul> <h4>Job Statuses:</h4> <ul>     <li><b>PENDING:</b> Job is queued and waiting to start.</li>     <li><b>PROCESSING:</b> Job is actively being processed.</li>     <li><b>COMPLETED:</b> Job finished successfully, results are available.</li>     <li><b>FAILED:</b> Job failed with an error.</li>     <li><b>CANCELLED:</b> Job was cancelled by user or system.</li> </ul> 


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
| **404** | Job ID not found. |  -  |
| **200** | Job status and results retrieved successfully. |  -  |
| **401** | Authentication failed. Missing or invalid API key. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="getmonitorcheck"></a>
# **GetMonitorCheck**
> MonitorCheckResponse GetMonitorCheck (string checkId)

Get Monitoring Check

Get details of a specific monitoring check including uptime metrics.


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **checkId** | **string** | Check ID |  |

### Return type

[**MonitorCheckResponse**](MonitorCheckResponse.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Check details. |  -  |
| **401** | Authentication failed. |  -  |
| **404** | Check not found or access denied. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="getmonitordashboard"></a>
# **GetMonitorDashboard**
> MonitorDashboardResponse GetMonitorDashboard ()

Get Monitoring Dashboard

<p>Get aggregated dashboard statistics for all monitoring checks.</p> <h4>Includes:</h4> <ul>     <li>Total, passing, failing, and degraded check counts</li>     <li>Average uptime percentages (24h, 7d, 30d)</li>     <li>Average response time</li>     <li>Checks grouped by type and status</li> </ul> 


### Parameters
This endpoint does not need any parameter.
### Return type

[**MonitorDashboardResponse**](MonitorDashboardResponse.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **401** | Authentication failed. |  -  |
| **200** | Dashboard summary. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="getmonitorresults"></a>
# **GetMonitorResults**
> void GetMonitorResults (string checkId, int limit = null)

Get Check Results

<p>Get the execution history for a monitoring check.</p> <h4>Response includes for each result:</h4> <ul>     <li>Timestamp of execution</li>     <li>Success/failure status</li>     <li>Response time</li>     <li>HTTP status code (for API checks)</li>     <li>Error message (if failed)</li> </ul> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **checkId** | **string** | Check ID |  |
| **limit** | **int** | Maximum number of results to return | [optional] [default to 10] |

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
| **401** | Authentication failed. |  -  |
| **404** | Check not found or access denied. |  -  |
| **200** | Check execution history. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="getmonitoringstatus"></a>
# **GetMonitoringStatus**
> void GetMonitoringStatus (string target)

Get Monitoring Status and Metrics

<p>Retrieves current monitoring configuration and historical metrics for a domain or IP address.</p> <h4>Status Information:</h4> <ul>     <li><b>Monitoring State:</b> Active, paused, or not monitored</li>     <li><b>Check Frequency:</b> How often checks are performed</li>     <li><b>Active Alerts:</b> Currently triggered alert conditions</li>     <li><b>Last Check:</b> Timestamp of most recent check</li> </ul> <h4>Metrics Included:</h4> <ul>     <li>Uptime percentage (last 30 days)</li>     <li>Average response time</li>     <li>SSL certificate expiration countdown</li>     <li>DNS change events</li>     <li>WHOIS change events</li> </ul> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **target** | **string** | The domain or IP address to check monitoring status for. |  |

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
| **404** | Target is not being monitored. |  -  |
| **200** | Successfully retrieved monitoring status. |  -  |
| **401** | Authentication failed. Missing or invalid API key. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="getscreenshothistory"></a>
# **GetScreenshotHistory**
> void GetScreenshotHistory (string target, int limit = null)

Get Screenshot History

<p>Retrieve all previously captured screenshots for a specific URL, ordered by capture time (newest first). Includes download URLs and metadata for each capture.</p> <h4>Response Includes:</h4> <ul>     <li><b>Download URL:</b> Direct link to screenshot image</li>     <li><b>Capture Time:</b> Timestamp when screenshot was taken</li>     <li><b>Dimensions:</b> Image width and height</li>     <li><b>Format:</b> Image format (PNG, JPEG, WebP)</li>     <li><b>File Size:</b> Size in bytes</li> </ul> <h4>Use Cases:</h4> <ul>     <li>Review website evolution over time</li>     <li>Compare screenshots for change detection</li>     <li>Download historical screenshots for reporting</li> </ul> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **target** | **string** | The target domain or URL to retrieve screenshot history for. |  |
| **limit** | **int** | Maximum number of screenshots to return. | [optional] [default to 10] |

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
| **200** | Successfully retrieved screenshot history. |  -  |
| **400** | Invalid URL parameter. |  -  |
| **401** | Authentication failed. Missing or invalid API key. |  -  |
| **404** | No screenshots found for the specified URL. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="listjobs"></a>
# **ListJobs**
> void ListJobs (string status = null, int limit = null, int offset = null)

List Recent Jobs

<p>Retrieves a list of recent jobs for the authenticated user, optionally filtered by status.</p> <h4>Query Parameters:</h4> <ul>     <li><b>status:</b> Filter by job status (PENDING, PROCESSING, COMPLETED, FAILED, CANCELLED)</li>     <li><b>limit:</b> Maximum number of jobs to return (default: 50, max: 100)</li>     <li><b>offset:</b> Number of jobs to skip for pagination (default: 0)</li> </ul> <h4>Response Format:</h4> <p>Returns a JSON object with a \"jobs\" array containing job summaries.</p> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **status** | **string** | Filter by job status | [optional]  |
| **limit** | **int** | Maximum number of jobs to return | [optional] [default to 50] |
| **offset** | **int** | Number of jobs to skip | [optional] [default to 0] |

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
| **200** | Successfully retrieved job list. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="listmonitorchecks"></a>
# **ListMonitorChecks**
> MonitorListResponse ListMonitorChecks (string type = null, string status = null)

List Monitoring Checks

<p>Get a list of all monitoring checks created by the authenticated user.</p> <h4>Filtering:</h4> <ul>     <li><b>type:</b> Filter by check type (api, ssl, dns)</li>     <li><b>status:</b> Filter by status (passing, failing, degraded, pending)</li> </ul> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **type** | **string** | Filter by check type | [optional]  |
| **status** | **string** | Filter by status | [optional]  |

### Return type

[**MonitorListResponse**](MonitorListResponse.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | List of monitoring checks. |  -  |
| **401** | Authentication failed. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="listtrackedindicators"></a>
# **ListTrackedIndicators**
> void ListTrackedIndicators ()

List Tracked Indicators

<p>Get a list of all indicators currently being tracked for changes by the authenticated user.</p> 


### Parameters
This endpoint does not need any parameter.
### Return type

void (empty response body)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json, */*


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | List of tracked indicators. |  -  |
| **401** | Authentication failed. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="schedulescreenshot"></a>
# **ScheduleScreenshot**
> JobResponse ScheduleScreenshot (ScreenshotRequest screenshotRequest)

Schedule Recurring Screenshots (Asynchronous)

<p>Create a recurring job to capture website screenshots at regular intervals. Essential for monitoring website changes, detecting defacements, and tracking competitor updates.</p> <h4>Schedule Options:</h4> <ul>     <li><b>Cron Expression:</b> Full cron syntax support (e.g., `0 0 * * * *` = hourly)</li>     <li><b>Frequency Presets:</b> hourly, daily, weekly, monthly</li>     <li><b>Timezone:</b> Specify timezone for accurate scheduling</li>     <li><b>Retention:</b> Auto-cleanup old screenshots (default: keep last 30)</li> </ul> <h4>Performance:</h4> <ul>     <li><b>Setup Time:</b> ~2 seconds to create schedule</li>     <li><b>Screenshot Time:</b> 10-30 seconds per capture</li> </ul> <h4>Use Cases:</h4> <ul>     <li>Automated defacement detection</li>     <li>Compliance monitoring and archival</li>     <li>Competitor website tracking</li>     <li>Visual regression testing</li> </ul> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **screenshotRequest** | [**ScreenshotRequest**](ScreenshotRequest.md) | Schedule configuration including URL, schedule timing, and screenshot options. |  |

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
| **401** | Authentication failed. Missing or invalid API key. |  -  |
| **202** | Schedule successfully created. Poll &#x60;/v1/ops/jobs/{jobId}&#x60; for status. |  -  |
| **400** | Invalid schedule configuration or missing required fields. |  -  |

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
| **401** | Authentication failed. Missing or invalid API key. |  -  |
| **429** | Rate limit exceeded for search operations. |  -  |
| **400** | Invalid search query or parameters. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="similardomains"></a>
# **SimilarDomains**
> JobResponse SimilarDomains (SimilarDomainsOpsRequest similarDomainsOpsRequest)

Find Similar Domains (Asynchronous)

<p>Generates potential lookalike, typosquatting, and homoglyph domains for brand protection and threat hunting.</p> <h4>Detection Methods:</h4> <ul>     <li>Typosquatting (keyboard proximity)</li>     <li>Homoglyph attacks (visually similar characters)</li>     <li>Combosquatting (brand + keyword)</li>     <li>TLD variations</li> </ul> <h4>Performance:</h4> <p>Typically completes in 5-15 seconds depending on options.</p> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **similarDomainsOpsRequest** | [**SimilarDomainsOpsRequest**](SimilarDomainsOpsRequest.md) | Similar domains request with domain and options. |  |

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
| **400** | Invalid domain or options. |  -  |
| **401** | Authentication failed. |  -  |
| **202** | Similar domains job created successfully. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="startchangetracking"></a>
# **StartChangeTracking**
> JobResponse StartChangeTracking (string type, string value, ChangeTrackingRequest changeTrackingRequest)

Start Change Tracking

<p>Start tracking changes for an IP or domain. When tracking is started, a baseline snapshot is captured. Subsequent checks will compare against this baseline and record any detected changes.</p> <h4>Trackable Fields for Domains:</h4> <ul>     <li><b>dns:</b> A, AAAA, MX, NS, TXT, CNAME records</li>     <li><b>whois:</b> Registrant, registrar, dates, nameservers</li>     <li><b>ssl:</b> Certificate issuer, expiry, SAN</li>     <li><b>subdomains:</b> Discovered subdomains</li>     <li><b>ips:</b> Resolved IP addresses</li> </ul> <h4>Trackable Fields for IPs:</h4> <ul>     <li><b>geolocation:</b> Country, city, coordinates</li>     <li><b>asn:</b> ASN number, organization</li>     <li><b>routing:</b> BGP routing status</li>     <li><b>rpki:</b> RPKI validation status</li>     <li><b>reverse_dns:</b> PTR records</li> </ul> <h4>Frequencies:</h4> <ul>     <li><b>hourly:</b> Check every hour</li>     <li><b>daily:</b> Check once per day (default)</li>     <li><b>weekly:</b> Check once per week</li> </ul> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **type** | **string** | Indicator type: ip or domain |  |
| **value** | **string** | Indicator value (IP address or domain name) |  |
| **changeTrackingRequest** | [**ChangeTrackingRequest**](ChangeTrackingRequest.md) | Tracking configuration |  |

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
| **202** | Tracking started. Job ID returned for baseline capture. |  -  |
| **401** | Authentication failed. |  -  |
| **400** | Invalid indicator type or fields. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="stopchangetracking"></a>
# **StopChangeTracking**
> void StopChangeTracking (string type, string value, bool deleteHistory = null)

Stop Change Tracking

<p>Stop tracking changes for an indicator. Optionally delete all change history.</p> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **type** | **string** | Indicator type: ip or domain |  |
| **value** | **string** | Indicator value |  |
| **deleteHistory** | **bool** | Delete change history as well | [optional] [default to false] |

### Return type

void (empty response body)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: Not defined


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **401** | Authentication failed. |  -  |
| **204** | Tracking stopped successfully. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="triggercheck"></a>
# **TriggerCheck**
> JobResponse TriggerCheck (string type, string value)

Trigger Immediate Check

<p>Trigger an immediate check for changes on a tracked indicator. Creates a job to compare current data against the stored baseline.</p> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **type** | **string** | Indicator type |  |
| **value** | **string** | Indicator value |  |

### Return type

[**JobResponse**](JobResponse.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: */*, application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **401** | Authentication failed. |  -  |
| **202** | Check triggered. Job ID returned. |  -  |
| **404** | Indicator is not being tracked. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="triggermonitorcheck"></a>
# **TriggerMonitorCheck**
> void TriggerMonitorCheck (string checkId)

Trigger Manual Check

Trigger an immediate execution of a monitoring check.


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **checkId** | **string** | Check ID |  |

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
| **401** | Authentication failed. |  -  |
| **404** | Check not found or access denied. |  -  |
| **202** | Check triggered successfully. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="updatemonitorcheck"></a>
# **UpdateMonitorCheck**
> MonitorCheckResponse UpdateMonitorCheck (string checkId, MonitorCheckRequest monitorCheckRequest)

Update Monitoring Check

Update an existing monitoring check configuration.


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **checkId** | **string** | Check ID |  |
| **monitorCheckRequest** | [**MonitorCheckRequest**](MonitorCheckRequest.md) | Updated check configuration |  |

### Return type

[**MonitorCheckResponse**](MonitorCheckResponse.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **401** | Authentication failed. |  -  |
| **200** | Check updated successfully. |  -  |
| **404** | Check not found or access denied. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

