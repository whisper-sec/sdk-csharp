# Noctis.FrontGraph.Sdk.Api.DomainManagementApi

All URIs are relative to *https://spider.noctisnet.com*

| Method | HTTP request | Description |
|--------|--------------|-------------|
| [**FindSubdomains**](DomainManagementApi.md#findsubdomains) | **GET** /domainer/api/domains/subdomains/{baseDomain} | Find subdomains |

<a id="findsubdomains"></a>
# **FindSubdomains**
> DomainerStringListResponse FindSubdomains (string baseDomain, int limit = null, string level = null)

Find subdomains

Finds domains that are subdomains of the given base domain (e.g., finding 'www.example.com' for base 'example.com'). Allows filtering by absolute domain level (dot count). NOTE: This differs from relative depth filtering.

### Example
```csharp
using System.Collections.Generic;
using System.Diagnostics;
using Noctis.FrontGraph.Sdk.Api;
using Noctis.FrontGraph.Sdk.Client;
using Noctis.FrontGraph.Sdk.Model;

namespace Example
{
    public class FindSubdomainsExample
    {
        public static void Main()
        {
            Configuration config = new Configuration();
            config.BasePath = "https://spider.noctisnet.com";
            // Configure Bearer token for authorization: bearerAuth
            config.AccessToken = "YOUR_BEARER_TOKEN";

            var apiInstance = new DomainManagementApi(config);
            var baseDomain = example.com;  // string | Base domain name (e.g., example.com)
            var limit = 100;  // int | Maximum number of results (optional)  (default to 100)
            var level = ALL;  // string | Level of subdomains to find relative to the base domain (ALL, IMMEDIATE=one level deeper, MAX_DEPTH=deepest found relative to base). (optional) 

            try
            {
                // Find subdomains
                DomainerStringListResponse result = apiInstance.FindSubdomains(baseDomain, limit, level);
                Debug.WriteLine(result);
            }
            catch (ApiException  e)
            {
                Debug.Print("Exception when calling DomainManagementApi.FindSubdomains: " + e.Message);
                Debug.Print("Status Code: " + e.ErrorCode);
                Debug.Print(e.StackTrace);
            }
        }
    }
}
```

#### Using the FindSubdomainsWithHttpInfo variant
This returns an ApiResponse object which contains the response data, status code and headers.

```csharp
try
{
    // Find subdomains
    ApiResponse<DomainerStringListResponse> response = apiInstance.FindSubdomainsWithHttpInfo(baseDomain, limit, level);
    Debug.Write("Status Code: " + response.StatusCode);
    Debug.Write("Response Headers: " + response.Headers);
    Debug.Write("Response Body: " + response.Data);
}
catch (ApiException e)
{
    Debug.Print("Exception when calling DomainManagementApi.FindSubdomainsWithHttpInfo: " + e.Message);
    Debug.Print("Status Code: " + e.ErrorCode);
    Debug.Print(e.StackTrace);
}
```

### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **baseDomain** | **string** | Base domain name (e.g., example.com) |  |
| **limit** | **int** | Maximum number of results | [optional] [default to 100] |
| **level** | **string** | Level of subdomains to find relative to the base domain (ALL, IMMEDIATE&#x3D;one level deeper, MAX_DEPTH&#x3D;deepest found relative to base). | [optional]  |

### Return type

[**DomainerStringListResponse**](DomainerStringListResponse.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Subdomains found |  -  |
| **400** | Invalid base domain name |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

