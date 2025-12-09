<div align="center">
  <img src="Whisper_Logo.png" alt="Whisper Logo" width="400"/>

  # Whisper API SDK - C# / .NET

[![Build](https://github.com/whisper-sec/sdk-csharp/actions/workflows/ci.yml/badge.svg)](https://github.com/whisper-sec/sdk-csharp/actions/workflows/ci.yml)
[![Publish](https://github.com/whisper-sec/sdk-csharp/actions/workflows/publish.yml/badge.svg)](https://github.com/whisper-sec/sdk-csharp/actions/workflows/publish.yml)
[![NuGet version](https://badge.fury.io/nu/Whisper.Api.Sdk.svg)](https://badge.fury.io/nu/Whisper.Api.Sdk)
[![NuGet downloads](https://img.shields.io/nuget/dt/Whisper.Api.Sdk.svg)](https://www.nuget.org/packages/Whisper.Api.Sdk)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)

> **Official C# / .NET SDK for Whisper API** - Comprehensive threat intelligence and security operations for domains, IPs, and web infrastructure.

**[Website](https://www.whisper.security)** | **[Documentation](https://docs.whisper.security)** | **[API Reference](https://developer.whisper.security)** | **[API Playground](https://dash.whisper.security/playground)** | **[Contact Us](https://www.whisper.security/contactus)**

</div>

---

## Quick Start

### 1. Installation

```bash
dotnet add package Whisper.Api.Sdk
```

Or via Package Manager Console:
```powershell
Install-Package Whisper.Api.Sdk
```

### 2. Get Your API Key

Sign up at [dash.whisper.security](https://dash.whisper.security) to get your API key.

### 3. Make Your First Request

```csharp
using Whisper.Api.Sdk.Api;
using Whisper.Api.Sdk.Client;

var config = new Configuration();
config.BasePath = "https://api.whisper.security";
config.AccessToken = "YOUR_API_KEY";

var api = new EnrichmentApi(config);
var response = await api.GetIndicatorAsync("ip", "8.8.8.8");
Console.WriteLine($"Organization: {response.Summary.Organization}");
```

---

## Key Features

- **Unified API** - Single interface for IP, Domain, WHOIS, DNS, Routing, Geolocation
- **Async/Await** - Modern async programming model throughout
- **Fully Typed** - Complete type definitions with IntelliSense support
- **Fast** - <500ms typical response time with strategic caching
- **.NET 6+** - Compatible with .NET 6, 7, and 8

---

## API Overview

### Enrichment API
Comprehensive enrichment for IPs and domains.

```csharp
var api = new EnrichmentApi(config);

// IP enrichment with optional modules
var ip = await api.GetIndicatorAsync("ip", "8.8.8.8", "routing,rpki");

// Domain analysis
var domain = await api.GetIndicatorAsync("domain", "example.com", "whois,dns_details");

// Subdomain discovery
var subdomains = await api.GetSubdomainsAsync("example.com");

// Predictive risk score (AI-powered)
var risk = await api.GetPredictiveRiskAsync("ip", "8.8.8.8");

// Bulk enrichment (async job)
var job = await api.BulkEnrichmentAsync(new BulkRequest {
    Indicators = new List<string> { "8.8.8.8", "example.com" }
});
```

### Location API
IP geolocation lookups.

```csharp
var api = new LocationApi(config);

var location = await api.GetIpLocationAsync("8.8.8.8");
Console.WriteLine($"Country: {location.Country}, City: {location.City}");

// Bulk geolocation
var bulk = await api.GetBulkIpLocationAsync(bulkRequest);

// Network/CIDR lookup
var network = await api.GetNetworkLocationAsync("8.8.8.0/24");
```

### AI Intelligence API
AI-powered threat investigation and analysis.

```csharp
var api = new AiIntelligenceApi(config);

// Industry security benchmark (synchronous)
var benchmark = await api.GetIndustryBenchmarkAsync("financial_services", "enterprise");

// AI-powered investigation (async job)
var investigation = await api.AiInvestigateAsync(investigateRequest);

// Threat actor attribution
var attribution = await api.AiAttributeAsync(attributeRequest);

// Global indicator correlation
var correlation = await api.AiCorrelateAsync(correlateRequest);
```

### Screenshots API
Website screenshot capture and scheduling.

```csharp
var api = new ScreenshotsApi(config);

// Capture screenshot (returns job ID)
var job = await api.CreateScreenshotAsync(screenshotRequest);

// Schedule recurring screenshots
var schedule = await api.ScheduleScreenshotAsync(scheduleRequest);
```

### Jobs API
Manage async operations.

```csharp
var api = new JobsApi(config);

// Get job status and results
var job = await api.GetJobAsync(jobId);

// List your jobs
var jobs = await api.ListJobsAsync();
```

---

## Authentication

All endpoints require Bearer token authentication:

```csharp
var config = new Configuration {
    BasePath = "https://api.whisper.security",
    AccessToken = Environment.GetEnvironmentVariable("WHISPER_API_KEY")
};
```

---

## Error Handling

```csharp
try {
    var response = await api.GetIndicatorAsync("ip", "8.8.8.8");
} catch (ApiException e) {
    Console.WriteLine($"Status: {e.ErrorCode}, Message: {e.Message}");
}
```

---

## Rate Limits

| Category | Limit |
|----------|-------|
| Indicators (`/v1/indicators/*`) | 100 req/sec |
| Location (`/v1/location/*`) | 100 req/sec |
| Jobs (`/v1/ops/jobs/*`) | 100 req/sec |
| Bulk Operations | 10 req/sec |
| Screenshots | 10 req/sec |
| Scans | 10 req/sec |
| AI Operations | 5 req/min |

---

## Documentation

- **Full Documentation**: [docs.whisper.security](https://docs.whisper.security)
- **API Reference**: [developer.whisper.security](https://developer.whisper.security)
- **API Playground**: [dash.whisper.security/playground](https://dash.whisper.security/playground)

---

## Requirements

- .NET 6.0+ / .NET 7.0+ / .NET 8.0+

---

## Other SDKs

- **Python**: [github.com/whisper-sec/sdk-python](https://github.com/whisper-sec/sdk-python)
- **TypeScript/JavaScript**: [github.com/whisper-sec/sdk-typescript](https://github.com/whisper-sec/sdk-typescript)
- **Java**: [github.com/whisper-sec/sdk-java](https://github.com/whisper-sec/sdk-java)
- **Rust**: [github.com/whisper-sec/sdk-rust](https://github.com/whisper-sec/sdk-rust)

---

## Support

- **Email**: [support@whisper.security](mailto:support@whisper.security)
- **Issues**: [github.com/whisper-sec/sdk-csharp/issues](https://github.com/whisper-sec/sdk-csharp/issues)

---

## License

MIT License - See [LICENSE](LICENSE) file for details.
