# Whisper.Api.Sdk.Api.MonitoringApi

All URIs are relative to *https://api.whisper.security*

| Method | HTTP request | Description |
|--------|--------------|-------------|
| [**CreateMonitorCheck**](MonitoringApi.md#createmonitorcheck) | **POST** /v1/ops/monitoring | Create Monitoring Check |
| [**CreateMonitoringAlert**](MonitoringApi.md#createmonitoringalert) | **POST** /v1/ops/monitoring/{target}/alert | Configure Monitoring Alert |
| [**DeleteMonitorCheck**](MonitoringApi.md#deletemonitorcheck) | **DELETE** /v1/ops/monitoring/{checkId} | Delete Monitoring Check |
| [**GetMonitorCheck**](MonitoringApi.md#getmonitorcheck) | **GET** /v1/ops/monitoring/{checkId} | Get Monitoring Check |
| [**GetMonitorDashboard**](MonitoringApi.md#getmonitordashboard) | **GET** /v1/ops/monitoring/dashboard | Get Monitoring Dashboard |
| [**GetMonitorResults**](MonitoringApi.md#getmonitorresults) | **GET** /v1/ops/monitoring/{checkId}/results | Get Check Results |
| [**GetMonitoringStatus**](MonitoringApi.md#getmonitoringstatus) | **GET** /v1/ops/monitoring/status/{target} | Get Monitoring Status |
| [**ListMonitorChecks**](MonitoringApi.md#listmonitorchecks) | **GET** /v1/ops/monitoring | List Monitoring Checks |
| [**TriggerMonitorCheck**](MonitoringApi.md#triggermonitorcheck) | **POST** /v1/ops/monitoring/{checkId}/trigger | Trigger Manual Check |
| [**UpdateMonitorCheck**](MonitoringApi.md#updatemonitorcheck) | **PUT** /v1/ops/monitoring/{checkId} | Update Monitoring Check |

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
| **201** | Monitoring check created successfully. |  -  |
| **400** | Invalid request - missing name or URL. |  -  |
| **401** | Authentication failed. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="createmonitoringalert"></a>
# **CreateMonitoringAlert**
> JobResponse CreateMonitoringAlert (string target, MonitoringAlertRequest monitoringAlertRequest)

Configure Monitoring Alert

<p>Configure alert notifications for a monitored target. Set up notifications for downtime, SSL expiry, DNS changes, and more.</p> <h4>Alert Types:</h4> <ul>     <li><b>downtime:</b> Alert when target becomes unreachable</li>     <li><b>dns_change:</b> Alert when DNS records change</li>     <li><b>whois_change:</b> Alert when WHOIS data changes</li>     <li><b>ssl_expiring:</b> Alert when SSL certificate is expiring (within threshold days)</li>     <li><b>content_change:</b> Alert when page content changes significantly</li>     <li><b>technology_change:</b> Alert when detected technologies change</li> </ul> <h4>Notification Channels:</h4> <ul>     <li><b>email:</b> Send alerts via email</li>     <li><b>slack:</b> Post to Slack webhook</li>     <li><b>webhook:</b> POST to custom webhook URL</li>     <li><b>pagerduty:</b> Create PagerDuty incident</li> </ul> 


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
| **202** | Alert configuration job accepted. |  -  |
| **400** | Invalid alert configuration. |  -  |
| **401** | Authentication failed. Missing or invalid API key. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="deletemonitorcheck"></a>
# **DeleteMonitorCheck**
> Object DeleteMonitorCheck (string checkId)

Delete Monitoring Check

Delete a monitoring check and stop all monitoring for the target.


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **checkId** | **string** | Check ID |  |

### Return type

**Object**

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: */*, application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **204** | Check deleted successfully. |  -  |
| **404** | Check not found or access denied. |  -  |
| **401** | Authentication failed. |  -  |

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
| **404** | Check not found or access denied. |  -  |
| **401** | Authentication failed. |  -  |

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
| **200** | Dashboard summary. |  -  |
| **401** | Authentication failed. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="getmonitorresults"></a>
# **GetMonitorResults**
> MonitorResultListResponse GetMonitorResults (string checkId, int limit = null)

Get Check Results

<p>Get the execution history for a monitoring check.</p> <h4>Response includes for each result:</h4> <ul>     <li>Timestamp of execution</li>     <li>Success/failure status</li>     <li>Response time</li>     <li>HTTP status code (for API checks)</li>     <li>Error message (if failed)</li> </ul> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **checkId** | **string** | Check ID |  |
| **limit** | **int** | Maximum number of results to return | [optional] [default to 10] |

### Return type

[**MonitorResultListResponse**](MonitorResultListResponse.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Check execution history. |  -  |
| **404** | Check not found or access denied. |  -  |
| **401** | Authentication failed. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="getmonitoringstatus"></a>
# **GetMonitoringStatus**
> MonitoringStatusResponse GetMonitoringStatus (string target)

Get Monitoring Status

<p>Get the current monitoring status and metrics for a domain or IP address.</p> <h4>Metrics Returned:</h4> <ul>     <li>Uptime percentage (last 30 days)</li>     <li>Average response time</li>     <li>SSL certificate expiration countdown</li>     <li>DNS change events</li>     <li>WHOIS change events</li> </ul> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **target** | **string** | The domain or IP address to check monitoring status for. |  |

### Return type

[**MonitoringStatusResponse**](MonitoringStatusResponse.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Successfully retrieved monitoring status. |  -  |
| **401** | Authentication failed. Missing or invalid API key. |  -  |
| **404** | Target is not being monitored. |  -  |

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

<a id="triggermonitorcheck"></a>
# **TriggerMonitorCheck**
> GenericSuccessResponse TriggerMonitorCheck (string checkId)

Trigger Manual Check

Trigger an immediate execution of a monitoring check.


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **checkId** | **string** | Check ID |  |

### Return type

[**GenericSuccessResponse**](GenericSuccessResponse.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **202** | Check triggered successfully. |  -  |
| **404** | Check not found or access denied. |  -  |
| **401** | Authentication failed. |  -  |

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
| **200** | Check updated successfully. |  -  |
| **404** | Check not found or access denied. |  -  |
| **401** | Authentication failed. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

