# Noctis.FrontGraph.Sdk.Api.IntelligenceServicesApi

All URIs are relative to *https://spider.noctisnet.com*

| Method | HTTP request | Description |
|--------|--------------|-------------|
| [**GetDomainIntelligence**](IntelligenceServicesApi.md#getdomainintelligence) | **GET** /intelligence/v1/domain/{domain} | Get comprehensive domain intelligence with streaming support |
| [**GetIpIntelligence**](IntelligenceServicesApi.md#getipintelligence) | **GET** /intelligence/v1/ip/{address} | Get comprehensive IP address intelligence with streaming support |

<a id="getdomainintelligence"></a>
# **GetDomainIntelligence**
> DomainIntelligenceResponse GetDomainIntelligence (string domain)

Get comprehensive domain intelligence with streaming support

Analyzes a domain name and returns comprehensive intelligence data from multiple sources.  **🚀 Response Modes:** - **Batch Mode** (Default): Complete JSON response in 2-5 seconds - **Streaming Mode**: Server-Sent Events with 200ms time-to-first-byte   - Accept: `application/json` for batch mode   - Accept: `text/event-stream` for streaming mode  **Key Features:** - WHOIS registration data with ownership history - Complete DNS record enumeration (A, AAAA, MX, NS, TXT, CNAME, SOA) - Subdomain discovery and enumeration - Link analysis showing connected domains - IP intelligence for all resolved addresses - Trademark and brand protection status - Infrastructure relationships and shared hosting  **Streaming Example:** ```bash curl -N -H 'Accept: text/event-stream' \\      -H 'Authorization: Bearer {token}' \\      https://api.example.com/intelligence/v1/domain/example.com ```  **Streaming Events:** - `whois`: Domain registration info - `dns`: DNS records - `subdomains`: Discovered subdomains - `ip_intelligence`: Intelligence for each resolved IP - `complete`: Final aggregated data  **Input Processing:** - Automatically strips protocols (http://, https://) - Removes www prefix if present - Validates domain format before processing  **Note:** Swagger UI only displays batch mode. Use curl or EventSource for streaming.

### Example
```csharp
using System.Collections.Generic;
using System.Diagnostics;
using Noctis.FrontGraph.Sdk.Api;
using Noctis.FrontGraph.Sdk.Client;
using Noctis.FrontGraph.Sdk.Model;

namespace Example
{
    public class GetDomainIntelligenceExample
    {
        public static void Main()
        {
            Configuration config = new Configuration();
            config.BasePath = "https://spider.noctisnet.com";
            // Configure Bearer token for authorization: bearerAuth
            config.AccessToken = "YOUR_BEARER_TOKEN";

            var apiInstance = new IntelligenceServicesApi(config);
            var domain = "domain_example";  // string | Domain name to analyze. Can be a root domain or subdomain. Protocol and www prefix are automatically removed.

            try
            {
                // Get comprehensive domain intelligence with streaming support
                DomainIntelligenceResponse result = apiInstance.GetDomainIntelligence(domain);
                Debug.WriteLine(result);
            }
            catch (ApiException  e)
            {
                Debug.Print("Exception when calling IntelligenceServicesApi.GetDomainIntelligence: " + e.Message);
                Debug.Print("Status Code: " + e.ErrorCode);
                Debug.Print(e.StackTrace);
            }
        }
    }
}
```

#### Using the GetDomainIntelligenceWithHttpInfo variant
This returns an ApiResponse object which contains the response data, status code and headers.

```csharp
try
{
    // Get comprehensive domain intelligence with streaming support
    ApiResponse<DomainIntelligenceResponse> response = apiInstance.GetDomainIntelligenceWithHttpInfo(domain);
    Debug.Write("Status Code: " + response.StatusCode);
    Debug.Write("Response Headers: " + response.Headers);
    Debug.Write("Response Body: " + response.Data);
}
catch (ApiException e)
{
    Debug.Print("Exception when calling IntelligenceServicesApi.GetDomainIntelligenceWithHttpInfo: " + e.Message);
    Debug.Print("Status Code: " + e.ErrorCode);
    Debug.Print(e.StackTrace);
}
```

### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **domain** | **string** | Domain name to analyze. Can be a root domain or subdomain. Protocol and www prefix are automatically removed. |  |

### Return type

[**DomainIntelligenceResponse**](DomainIntelligenceResponse.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Domain intelligence data successfully retrieved |  * X-RateLimit-Limit - Number of requests allowed per hour <br>  |
| **400** | Invalid domain name format |  -  |
| **401** | Authentication required |  -  |
| **404** | Domain not found or unregistered |  -  |
| **429** | Rate limit exceeded |  -  |
| **500** | Internal server error during intelligence aggregation |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

<a id="getipintelligence"></a>
# **GetIpIntelligence**
> IpIntelligenceResponse GetIpIntelligence (string address)

Get comprehensive IP address intelligence with streaming support

Analyzes an IP address and returns comprehensive intelligence data aggregated from multiple sources.  **🚀 Response Modes:** - **Batch Mode** (Default): Complete JSON response in 2-3 seconds - **Streaming Mode**: Server-Sent Events with 150ms time-to-first-byte   - Accept: `application/json` for batch mode   - Accept: `text/event-stream` for streaming mode  **Key Features:** - Geolocation with city-level precision and confidence scores - Network topology including ASN, BGP prefixes, and routing visibility - ISP and organization identification - DNS relationships showing associated domains - Risk scoring based on threat intelligence feeds - RPKI validation and routing security assessment - Historical routing data and stability metrics  **Streaming Example:** ```bash curl -N -H 'Accept: text/event-stream' \\      -H 'Authorization: Bearer {token}' \\      https://api.example.com/intelligence/v1/ip/8.8.8.8 ```  **Note:** Swagger UI only displays batch mode. Use curl or EventSource for streaming.

### Example
```csharp
using System.Collections.Generic;
using System.Diagnostics;
using Noctis.FrontGraph.Sdk.Api;
using Noctis.FrontGraph.Sdk.Client;
using Noctis.FrontGraph.Sdk.Model;

namespace Example
{
    public class GetIpIntelligenceExample
    {
        public static void Main()
        {
            Configuration config = new Configuration();
            config.BasePath = "https://spider.noctisnet.com";
            // Configure Bearer token for authorization: bearerAuth
            config.AccessToken = "YOUR_BEARER_TOKEN";

            var apiInstance = new IntelligenceServicesApi(config);
            var address = "address_example";  // string | IPv4 or IPv6 address to analyze. Supports standard notation (e.g., 192.168.1.1 or 2001:db8::1)

            try
            {
                // Get comprehensive IP address intelligence with streaming support
                IpIntelligenceResponse result = apiInstance.GetIpIntelligence(address);
                Debug.WriteLine(result);
            }
            catch (ApiException  e)
            {
                Debug.Print("Exception when calling IntelligenceServicesApi.GetIpIntelligence: " + e.Message);
                Debug.Print("Status Code: " + e.ErrorCode);
                Debug.Print(e.StackTrace);
            }
        }
    }
}
```

#### Using the GetIpIntelligenceWithHttpInfo variant
This returns an ApiResponse object which contains the response data, status code and headers.

```csharp
try
{
    // Get comprehensive IP address intelligence with streaming support
    ApiResponse<IpIntelligenceResponse> response = apiInstance.GetIpIntelligenceWithHttpInfo(address);
    Debug.Write("Status Code: " + response.StatusCode);
    Debug.Write("Response Headers: " + response.Headers);
    Debug.Write("Response Body: " + response.Data);
}
catch (ApiException e)
{
    Debug.Print("Exception when calling IntelligenceServicesApi.GetIpIntelligenceWithHttpInfo: " + e.Message);
    Debug.Print("Status Code: " + e.ErrorCode);
    Debug.Print(e.StackTrace);
}
```

### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **address** | **string** | IPv4 or IPv6 address to analyze. Supports standard notation (e.g., 192.168.1.1 or 2001:db8::1) |  |

### Return type

[**IpIntelligenceResponse**](IpIntelligenceResponse.md)

### Authorization

[bearerAuth](../README.md#bearerAuth)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | IP intelligence data successfully retrieved |  * X-RateLimit-Limit - Number of requests allowed per hour <br>  * X-RateLimit-Remaining - Number of requests remaining <br>  |
| **400** | Invalid IP address format |  -  |
| **401** | Authentication required |  -  |
| **404** | IP address not found or private/reserved |  -  |
| **429** | Rate limit exceeded |  * Retry-After - Number of seconds to wait before retrying <br>  |
| **500** | Internal server error during intelligence aggregation |  -  |

[[Back to top]](#) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to Model list]](../../README.md#documentation-for-models) [[Back to README]](../../README.md)

