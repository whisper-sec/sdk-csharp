# Whisper API SDK - C# / .NET

[![CI](https://github.com/whisper-sec/sdk-csharp/actions/workflows/ci.yml/badge.svg)](https://github.com/whisper-sec/sdk-csharp/actions/workflows/ci.yml)
[![Publish](https://github.com/whisper-sec/sdk-csharp/actions/workflows/publish.yml/badge.svg)](https://github.com/whisper-sec/sdk-csharp/actions/workflows/publish.yml)
[![NuGet version](https://badge.fury.io/nu/Whisper.Api.Sdk.svg)](https://badge.fury.io/nu/Whisper.Api.Sdk)
[![NuGet downloads](https://img.shields.io/nuget/dt/Whisper.Api.Sdk.svg)](https://www.nuget.org/packages/Whisper.Api.Sdk)
[![.NET Version](https://img.shields.io/badge/.NET-6.0%2B-blue)](https://dotnet.microsoft.com/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)

> **Official C# / .NET SDK for Whisper API** - Comprehensive intelligence and monitoring capabilities for domains, IPs, and web infrastructure.

## Whisper API v1 - C# SDK

**The Foundational Intelligence Layer for the Internet**

Gain deep visibility into any internet asset with Whisper's comprehensive intelligence platform. Access powerful APIs for threat intelligence, domain monitoring, network security analysis, WHOIS data, DNS records, geolocation, BGP routing, and more - all through a single, unified interface.

The Whisper API provides comprehensive, real-time intelligence on any internet asset. By connecting billions of data points across live internet routing, historical registration records, and deep resolution data, our API moves beyond simple enrichment to deliver predictive, context-rich insights.

This C# SDK provides a fully-typed, async client for the Whisper API v1, designed for .NET applications and services.

---

## 🚀 Quick Start

### 1. Installation

```bash
dotnet add package Whisper.Api.Sdk
```

**Or via Package Manager Console:**
```powershell
Install-Package Whisper.Api.Sdk
```

### 2. Get Your API Key

Sign up at [dash.whisper.security](https://dash.whisper.security) to get your API key.

### 3. Make Your First Request

```csharp
using Whisper.Api.Sdk.Api;
using Whisper.Api.Sdk.Client;
using Whisper.Api.Sdk.Model;

class Program
{
    static async Task Main(string[] args)
    {
        // Configure Bearer token authentication
        var config = new Configuration();
        config.BasePath = "http://api.whisper.security";
        config.AccessToken = "YOUR_API_KEY";  // Replace with your actual API key

        var apiInstance = new IndicatorsApi(config);

        try
        {
            // Enrich an IP address
            var response = await apiInstance.GetIndicatorAsync("ip", "8.8.8.8");
            Console.WriteLine($"Organization: {response.Summary.Organization}");
            Console.WriteLine($"Location: {response.Summary.Location}");
            Console.WriteLine($"Risk Score: {response.Reputation.RiskScore}");
        }
        catch (ApiException e)
        {
            Console.WriteLine($"API Error: {e.Message}");
            Console.WriteLine($"Status Code: {e.ErrorCode}");
        }
    }
}
```

---

## 🎯 Key Features

- **Unified & Simple**: Small set of powerful, resource-oriented endpoints
- **Performant by Design**: Asynchronous-first with strategic caching (<500ms typical response)
- **Workflow-Oriented**: Built for real-world security operations, not just data dumps
- **Comprehensive**: IP, Domain, DNS, WHOIS, Routing, Geolocation, Screenshots, Monitoring
- **Fully Typed**: Complete type definitions with IntelliSense support
- **Async/Await**: Modern async programming model
- **.NET Standard 2.0+**: Compatible with .NET Framework, .NET Core, and .NET 5+

---

## 📋 Common Use Cases

### IP Address Enrichment
```csharp
var ipData = await apiInstance.GetIndicatorAsync("ip", "8.8.8.8", "routing,rpki");
Console.WriteLine($"ASN: {ipData.Network.Asn}");
```

### Domain Analysis
```csharp
var domainData = await apiInstance.GetIndicatorAsync("domain", "example.com", "whois,dns_details");
Console.WriteLine($"Registrar: {domainData.Whois.Registrar}");
Console.WriteLine($"Created: {domainData.Whois.CreatedDate}");
```

### Bulk Lookups (Asynchronous)
```csharp
var opsApi = new OperationsApi(config);

var bulkRequest = new BulkRequest
{
    Indicators = new List<string> { "8.8.8.8", "example.com" },
    Include = new List<string> { "basic", "reputation" }
};

var jobResponse = await apiInstance.BulkEnrichmentAsync(bulkRequest);
Console.WriteLine($"Job ID: {jobResponse.JobId}");

// Poll for results
var result = await opsApi.GetJobAsync(jobResponse.JobId);
Console.WriteLine($"Status: {result.Status}");
```

### Geolocation Lookup
```csharp
var locationApi = new LocationApi(config);
var location = await locationApi.GetIpLocationAsync("8.8.8.8");
Console.WriteLine($"Country: {location.Country}");
Console.WriteLine($"City: {location.City}");
Console.WriteLine($"Latitude: {location.Latitude}, Longitude: {location.Longitude}");
```

### Error Handling
```csharp
try
{
    var response = await apiInstance.GetIndicatorAsync("ip", "invalid-ip");
}
catch (ApiException e)
{
    Console.WriteLine($"Status Code: {e.ErrorCode}");
    Console.WriteLine($"Error: {e.Message}");
    Console.WriteLine($"Response Body: {e.ErrorContent}");
}
```

---

## 🔐 Authentication

All API endpoints require Bearer token authentication. Set your API key when creating the Configuration:

```csharp
var config = new Configuration();
config.BasePath = "http://api.whisper.security";
config.AccessToken = "YOUR_API_KEY";
```

### Using Environment Variables

```csharp
var config = new Configuration
{
    BasePath = "http://api.whisper.security",
    AccessToken = Environment.GetEnvironmentVariable("WHISPER_API_KEY")
};
```

### Using Configuration Files (appsettings.json)

```json
{
  "WhisperApi": {
    "BasePath": "http://api.whisper.security",
    "AccessToken": "YOUR_API_KEY"
  }
}
```

```csharp
var config = new Configuration
{
    BasePath = configuration["WhisperApi:BasePath"],
    AccessToken = configuration["WhisperApi:AccessToken"]
};
```

---

## 🔧 Advanced Configuration

### Custom HTTP Client
```csharp
var httpClient = new HttpClient();
httpClient.Timeout = TimeSpan.FromSeconds(30);

var config = new Configuration
{
    BasePath = "http://api.whisper.security",
    AccessToken = "YOUR_API_KEY"
};

var apiInstance = new IndicatorsApi(httpClient, config);
```

### Retry Policy (using Polly)
```csharp
var retryPolicy = Policy
    .Handle<ApiException>()
    .WaitAndRetryAsync(3, retryAttempt =>
        TimeSpan.FromSeconds(Math.Pow(2, retryAttempt)));

await retryPolicy.ExecuteAsync(async () =>
{
    return await apiInstance.GetIndicatorAsync("ip", "8.8.8.8");
});
```

---

## 📚 SDK Documentation

### Package Structure

```
Whisper.Api.Sdk/
├── Api/
│   ├── IndicatorsApi.cs        # Indicator enrichment endpoints
│   ├── LocationApi.cs          # Geolocation endpoints
│   └── OperationsApi.cs        # Async job management
├── Model/                      # Data models and classes
├── Client/
│   ├── Configuration.cs        # SDK configuration
│   ├── ApiClient.cs           # Core API client
│   └── ApiException.cs        # Exception handling
└── README.md
```

### API Classes

The SDK provides three main API classes with full async/await support:

#### IndicatorsApi
Comprehensive indicator enrichment for IPs and domains.

**Methods:**
- `GetIndicatorAsync(type, value, include = null)` - Enrich a single indicator
- `GetIndicatorHistoryAsync(type, value, limit = null)` - Get historical data
- `GetIndicatorGraphAsync(type, value)` - Get relationship graph
- `GetSubdomainsAsync(domain, limit = null)` - Get domain subdomains
- `GenerateSimilarDomainsGetAsync(domain, type = null, limit = null)` - Generate similar domains (GET)
- `GenerateSimilarDomainsPostAsync(domain, similarDomainsRequest)` - Generate similar domains (POST)
- `BulkEnrichmentAsync(bulkRequest)` - Bulk enrichment (async job)
- `SearchIndicatorsAsync(searchRequest)` - Search indicators (async job)

**Example:**
```csharp
using Whisper.Api.Sdk.Api;

var api = new IndicatorsApi(config);
var response = await api.GetIndicatorAsync("ip", "8.8.8.8", "routing,rpki");
Console.WriteLine($"ASN: {response.Network.Asn}");
```

[View Full IndicatorsApi Documentation](docs/apis/IndicatorsApi.md)

#### LocationApi
Geolocation lookups and searches.

**Methods:**
- `GetIpLocationAsync(ip)` - Get IP geolocation
- `SearchLocationAsync(field, value, limit = null)` - Search by location attributes

**Example:**
```csharp
using Whisper.Api.Sdk.Api;

var api = new LocationApi(config);
var location = await api.GetIpLocationAsync("8.8.8.8");
Console.WriteLine($"Country: {location.Country}, City: {location.City}");
```

[View Full LocationApi Documentation](docs/apis/LocationApi.md)

#### OperationsApi
Manage asynchronous jobs and operations.

**Methods:**
- `GetJobAsync(jobId)` - Get job status and results
- `ListJobsAsync(status = null, limit = null)` - List user jobs
- `CreateScreenshotAsync(screenshotRequest)` - Capture screenshot (async job)
- `CreateScanAsync(infraScanRequest)` - Infrastructure scan (async job)

**Example:**
```csharp
using Whisper.Api.Sdk.Api;

var api = new OperationsApi(config);
var job = await api.GetJobAsync("job-uuid-here");
Console.WriteLine($"Status: {job.Status}, Progress: {job.Progress.Percentage}%");
```

[View Full OperationsApi Documentation](docs/apis/OperationsApi.md)

---

## 📦 Data Models & Types

The SDK includes comprehensive C# classes for all API responses and requests with:
- Full property definitions with XML documentation
- JSON serialization/deserialization attributes
- Nullable reference type annotations
- Property validation

### Core Response Models

#### IndicatorResponse
Comprehensive intelligence for an IP or domain.

**Properties:**
- `Query` (QueryInfo) - Query metadata
- `Summary` (SummaryInfo) - Quick summary
- `Geolocation` (Dictionary<string, object>) - Geographic data
- `Network` (Dictionary<string, object>) - Network information
- `Isp` (Dictionary<string, object>) - ISP details
- `Registration` (Dictionary<string, object>) - WHOIS registration
- `Dns` (DnsInfo) - DNS records
- `Relationships` (RelationshipInfo) - Related infrastructure
- `Reputation` (ReputationInfo) - Risk and reputation scores
- `Security` (Dictionary<string, object>) - Security context
- `Metadata` (MetadataInfo) - Response metadata

[View Full Model Documentation](docs/models/IndicatorResponse.md)

#### LocationResponse
Geolocation data for an IP address.

**Properties:**
- `Ip` (string) - IP address
- `Country` (string) - Country name
- `CountryCode` (string) - ISO country code
- `City` (string) - City name
- `Latitude` (decimal) - Latitude
- `Longitude` (decimal) - Longitude
- `Timezone` (string) - Timezone
- `Isp` (string) - ISP name
- `Asn` (int) - Autonomous System Number

[View Full Model Documentation](docs/models/LocationResponse.md)

#### JobResponse
Asynchronous job status and results.

**Properties:**
- `JobId` (string) - Unique job identifier
- `Status` (string) - Job status (pending, in_progress, completed, failed)
- `Progress` (JobProgress) - Progress information
- `Result` (object) - Job results (when completed)
- `Error` (JobError) - Error details (when failed)
- `CreatedAt` (DateTime) - Creation timestamp
- `UpdatedAt` (DateTime) - Last update timestamp

[View Full Model Documentation](docs/models/JobResponse.md)

### Request Models

#### BulkRequest
Request for bulk indicator enrichment.

**Properties:**
- `Indicators` (List<string>) - List of IPs/domains (max 100)
- `Include` (List<string>) - Data modules to include
- `Options` (BulkOptions) - Processing options

[View Full Model Documentation](docs/models/BulkRequest.md)

#### SearchRequest
Request for indicator search.

**Properties:**
- `Query` (string) - Search query
- `Field` (string) - Field to search (registrantName, registrarName, etc.)
- `Limit` (int) - Maximum results (default: 100)

[View Full Model Documentation](docs/models/SearchRequest.md)

#### ScreenshotRequest
Request for website screenshot.

**Properties:**
- `Url` (string) - Target URL
- `Options` (ScreenshotOptions) - Capture options (fullPage, format, etc.)

[View Full Model Documentation](docs/models/ScreenshotRequest.md)

#### InfraScanRequest
Request for infrastructure scanning.

**Properties:**
- `Domain` (string) - Target domain
- `Type` (string) - Scan type (subdomains, ports, dns)
- `Config` (Dictionary<string, object>) - Type-specific configuration

[View Full Model Documentation](docs/models/InfraScanRequest.md)

### Complete Model Reference

For a complete list of all data models and their properties, see:

**Core Models:**
- [IndicatorResponse](docs/models/IndicatorResponse.md) - Main enrichment response
- [LocationResponse](docs/models/LocationResponse.md) - Geolocation data
- [JobResponse](docs/models/JobResponse.md) - Async job status
- [HistoryResponse](docs/models/HistoryResponse.md) - Historical data

**Request Models:**
- [BulkRequest](docs/models/BulkRequest.md) - Bulk enrichment
- [SearchRequest](docs/models/SearchRequest.md) - Search parameters
- [ScreenshotRequest](docs/models/ScreenshotRequest.md) - Screenshot options
- [InfraScanRequest](docs/models/InfraScanRequest.md) - Scan configuration
- [SimilarDomainsRequest](docs/models/SimilarDomainsRequest.md) - Similar domain generation

**Nested Models:**
- [QueryInfo](docs/models/QueryInfo.md) - Query metadata
- [SummaryInfo](docs/models/SummaryInfo.md) - Quick summary
- [DnsInfo](docs/models/DnsInfo.md) - DNS records
- [RelationshipInfo](docs/models/RelationshipInfo.md) - Infrastructure relationships
- [ReputationInfo](docs/models/ReputationInfo.md) - Reputation scores
- [MetadataInfo](docs/models/MetadataInfo.md) - Response metadata
- [JobProgress](docs/models/JobProgress.md) - Job progress details
- [JobError](docs/models/JobError.md) - Job error information

**Configuration Models:**
- [BulkOptions](docs/models/BulkOptions.md) - Bulk processing options
- [ScreenshotOptions](docs/models/ScreenshotOptions.md) - Screenshot settings
- [DnsEnumConfig](docs/models/DnsEnumConfig.md) - DNS enumeration config
- [PortScanConfig](docs/models/PortScanConfig.md) - Port scanning config
- [SubdomainEnumConfig](docs/models/SubdomainEnumConfig.md) - Subdomain enumeration config

**Security Models:**
- [BlacklistScores](docs/models/BlacklistScores.md) - Blacklist check results
- [DomainReputationScores](docs/models/DomainReputationScores.md) - Domain reputation
- [DomainReputationDetails](docs/models/DomainReputationDetails.md) - Detailed reputation data

**View All Models:** See the [docs/models/](docs/models/) directory for complete model documentation.

---

## 🔧 Advanced Usage

### Error Handling

```csharp
using Whisper.Api.Sdk.Client;

try
{
    var response = await apiInstance.GetIndicatorAsync("ip", "8.8.8.8");
}
catch (ApiException e)
{
    Console.WriteLine($"Status Code: {e.ErrorCode}");
    Console.WriteLine($"Message: {e.Message}");
    Console.WriteLine($"Response: {e.ErrorContent}");
}
```

### Custom Configuration

```csharp
using Whisper.Api.Sdk.Client;

var config = new Configuration
{
    BasePath = "http://api.whisper.security",
    AccessToken = Environment.GetEnvironmentVariable("WHISPER_API_KEY"),
    Timeout = 60000,
    UserAgent = "MyApp/1.0"
};

// Enable debugging
config.Debug = true;
```

### Working with Async Jobs

```csharp
using System.Threading.Tasks;
using Whisper.Api.Sdk.Api;
using Whisper.Api.Sdk.Model;

public async Task ProcessBulkEnrichmentAsync()
{
    var indicatorsApi = new IndicatorsApi(config);
    var opsApi = new OperationsApi(config);

    // Submit bulk job
    var bulkRequest = new BulkRequest
    {
        Indicators = new List<string> { "8.8.8.8", "1.1.1.1", "example.com" },
        Include = new List<string> { "basic", "reputation" }
    };

    var jobResponse = await indicatorsApi.BulkEnrichmentAsync(bulkRequest);

    // Poll for completion
    while (true)
    {
        var job = await opsApi.GetJobAsync(jobResponse.JobId);
        Console.WriteLine($"Status: {job.Status}, Progress: {job.Progress?.Percentage}%");

        if (job.Status == "completed" || job.Status == "failed")
        {
            break;
        }

        await Task.Delay(2000);
    }

    // Get results
    var finalJob = await opsApi.GetJobAsync(jobResponse.JobId);
    if (finalJob.Status == "completed")
    {
        Console.WriteLine($"Results: {finalJob.Result}");
    }
}
```

### Using with Dependency Injection (ASP.NET Core)

```csharp
// Startup.cs or Program.cs
using Whisper.Api.Sdk.Api;
using Whisper.Api.Sdk.Client;

services.AddSingleton<Configuration>(sp =>
{
    return new Configuration
    {
        BasePath = "http://api.whisper.security",
        AccessToken = Configuration["WhisperApi:AccessToken"]
    };
});

services.AddTransient<IIndicatorsApi, IndicatorsApi>();
services.AddTransient<ILocationApi, LocationApi>();
services.AddTransient<IOperationsApi, OperationsApi>();

// In your controller or service
public class ThreatService
{
    private readonly IIndicatorsApi _indicatorsApi;

    public ThreatService(IIndicatorsApi indicatorsApi)
    {
        _indicatorsApi = indicatorsApi;
    }

    public async Task<IndicatorResponse> EnrichIpAsync(string ip)
    {
        return await _indicatorsApi.GetIndicatorAsync("ip", ip);
    }
}
```

### Strongly-Typed Response Handling

```csharp
using Whisper.Api.Sdk.Model;

public async Task AnalyzeIndicatorAsync(string ip)
{
    var response = await apiInstance.GetIndicatorAsync("ip", ip);

    // Strongly typed access with IntelliSense
    if (response.Reputation?.RiskScore != null)
    {
        int risk = response.Reputation.RiskScore.Value;
        if (risk > 50)
        {
            Console.WriteLine($"High risk IP: {ip}");
        }
    }

    // Access nested properties safely
    var country = response.Geolocation?["country"];
    var asn = response.Network?["asn"];
}
```

### Cancellation Token Support

```csharp
using System.Threading;

var cts = new CancellationTokenSource();
cts.CancelAfter(TimeSpan.FromSeconds(30));

try
{
    var response = await apiInstance.GetIndicatorAsync(
        "ip",
        "8.8.8.8",
        cancellationToken: cts.Token
    );
}
catch (OperationCanceledException)
{
    Console.WriteLine("Request was cancelled");
}
```

---

## 📚 External Documentation

For detailed API documentation, visit:
- **Full Documentation**: [docs.whisper.security](https://docs.whisper.security)
- **API Reference**: [docs.whisper.security/api](https://docs.whisper.security/api)
- **Quick Start Guide**: [docs.whisper.security/quickstart](https://docs.whisper.security/quickstart)

---

## 📊 Rate Limits

| Category | Limit |
|----------|-------|
| Standard Enrichment | 100 req/min |
| Bulk Operations | 10 req/min |
| Search/Discovery | 5 req/min |
| Screenshots | 10 req/min |

Rate limits return HTTP 429. Retry after the time specified in the `Retry-After` header.

---

## 🆘 Support

- **Email**: api-support@whisper.security
- **Documentation**: https://docs.whisper.security
- **Issues**: https://github.com/whisper-sec/sdk-csharp/issues

---

## 📄 License

NoLicense - [http://localhost](http://localhost)

---

## 🏗️ Requirements

- .NET Standard 2.0 or higher
- .NET Framework 4.6.1 or higher
- .NET Core 2.0 or higher
- .NET 5.0 or higher

---

*Generated with ❤️ by Whisper Security*
