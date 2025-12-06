<div align="center">
  <img src="Whisper_Logo.png" alt="Whisper Logo" width="400"/>

  # Whisper API SDK - C# / .NET

[![Build](https://github.com/whisper-sec/sdk-csharp/actions/workflows/ci.yml/badge.svg)](https://github.com/whisper-sec/sdk-csharp/actions/workflows/ci.yml)
[![Publish](https://github.com/whisper-sec/sdk-csharp/actions/workflows/publish.yml/badge.svg)](https://github.com/whisper-sec/sdk-csharp/actions/workflows/publish.yml)
[![NuGet version](https://badge.fury.io/nu/Whisper.Api.Sdk.svg)](https://badge.fury.io/nu/Whisper.Api.Sdk)
[![NuGet downloads](https://img.shields.io/nuget/dt/Whisper.Api.Sdk.svg)](https://www.nuget.org/packages/Whisper.Api.Sdk)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)

> **Official C# / .NET SDK for Whisper API** - Comprehensive intelligence and monitoring for domains, IPs, and web infrastructure.

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
config.BasePath = "http://api.whisper.security";
config.AccessToken = "YOUR_API_KEY";

var api = new IndicatorsApi(config);
var response = await api.GetIndicatorAsync("ip", "8.8.8.8");
Console.WriteLine($"Organization: {response.Summary.Organization}");
```

---

## Key Features

- **Unified API** - Single interface for IP, Domain, WHOIS, DNS, Routing, Geolocation
- **Async/Await** - Modern async programming model throughout
- **Fully Typed** - Complete type definitions with IntelliSense support
- **Fast** - <500ms typical response time with strategic caching
- **.NET Standard 2.0+** - Compatible with .NET Framework, .NET Core, and .NET 5+

---

## API Overview

### Indicators API
Comprehensive enrichment for IPs and domains.

```csharp
// IP enrichment with optional modules
var ip = await api.GetIndicatorAsync("ip", "8.8.8.8", "routing,rpki");

// Domain analysis
var domain = await api.GetIndicatorAsync("domain", "example.com", "whois,dns_details");

// Subdomain discovery
var subdomains = await api.GetSubdomainsAsync("example.com");
```

### Location API
IP geolocation lookups.

```csharp
var locationApi = new LocationApi(config);
var location = await locationApi.GetIpLocationAsync("8.8.8.8");
Console.WriteLine($"Country: {location.Country}, City: {location.City}");
```

### Operations API
Async operations for long-running tasks.

```csharp
var opsApi = new OperationsApi(config);

// Bulk enrichment (returns job ID)
var job = await api.BulkEnrichmentAsync(new BulkRequest {
    Indicators = new List<string> { "8.8.8.8", "example.com" }
});

// Check job status
var status = await opsApi.GetJobAsync(job.JobId);
```

---

## Authentication

All endpoints require Bearer token authentication:

```csharp
var config = new Configuration {
    BasePath = "http://api.whisper.security",
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
| Standard Enrichment | 100 req/min |
| Bulk Operations | 10 req/min |
| Search/Discovery | 5 req/min |

---

## Documentation

- **Full Documentation**: [docs.whisper.security](https://docs.whisper.security)
- **API Reference**: [developer.whisper.security](https://developer.whisper.security)
- **API Playground**: [dash.whisper.security/playground](https://dash.whisper.security/playground)

---

## Requirements

- .NET Standard 2.0+ / .NET Framework 4.6.1+ / .NET Core 2.0+ / .NET 5.0+

---

## Support

- **Email**: [support@whisper.security](mailto:support@whisper.security)
- **Issues**: https://github.com/whisper-sec/sdk-csharp/issues

---

## License

MIT License - See [LICENSE](LICENSE) file for details.
