# Whisper.Api.Sdk.Api.ChangeTrackingApi

All URIs are relative to *https://api.whisper.security*

| Method | HTTP request | Description |
|--------|--------------|-------------|
| [**GetChanges**](ChangeTrackingApi.md#getchanges) | **GET** /v1/ops/tracking/{type}/{value} | Get Detected Changes |
| [**ListTrackedIndicators**](ChangeTrackingApi.md#listtrackedindicators) | **GET** /v1/ops/tracking | List Tracked Indicators |
| [**StartChangeTracking**](ChangeTrackingApi.md#startchangetracking) | **POST** /v1/ops/tracking/{type}/{value} | Start Change Tracking |
| [**StopChangeTracking**](ChangeTrackingApi.md#stopchangetracking) | **DELETE** /v1/ops/tracking/{type}/{value} | Stop Change Tracking |
| [**TriggerCheck**](ChangeTrackingApi.md#triggercheck) | **POST** /v1/ops/tracking/{type}/{value}/check | Trigger Immediate Check |

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
| **200** | Successfully retrieved changes. |  -  |
| **404** | Indicator is not being tracked. |  -  |
| **401** | Authentication failed. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="listtrackedindicators"></a>
# **ListTrackedIndicators**
> TrackedIndicatorsResponse ListTrackedIndicators ()

List Tracked Indicators

<p>Get a list of all indicators currently being tracked for changes by the authenticated user.</p> 


### Parameters
This endpoint does not need any parameter.
### Return type

[**TrackedIndicatorsResponse**](TrackedIndicatorsResponse.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | List of tracked indicators. |  -  |
| **401** | Authentication failed. |  -  |

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
| **400** | Invalid indicator type or fields. |  -  |
| **401** | Authentication failed. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="stopchangetracking"></a>
# **StopChangeTracking**
> GenericSuccessResponse StopChangeTracking (string type, string value, bool deleteHistory = null)

Stop Change Tracking

<p>Stop tracking changes for an indicator. Optionally delete all change history.</p> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **type** | **string** | Indicator type: ip or domain |  |
| **value** | **string** | Indicator value |  |
| **deleteHistory** | **bool** | Delete change history as well | [optional] [default to false] |

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
| **200** | Tracking stopped successfully. |  -  |
| **401** | Authentication failed. |  -  |
| **500** | Internal server error. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="triggercheck"></a>
# **TriggerCheck**
> GenericSuccessResponse TriggerCheck (string type, string value)

Trigger Immediate Check

<p>Trigger an immediate check for changes on a tracked indicator. Creates a job to compare current data against the stored baseline.</p> 


### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **type** | **string** | Indicator type |  |
| **value** | **string** | Indicator value |  |

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
| **400** | Invalid indicator type. |  -  |
| **404** | Indicator is not being tracked. |  -  |
| **401** | Authentication failed. |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

