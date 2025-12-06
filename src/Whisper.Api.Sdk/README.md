<div align="center">
  <img src="Whisper_Logo.png" alt="Whisper Logo" width="400"/>

  # Whisper API SDK - C#

[![CI](https://github.com/whisper-sec/sdk-csharp/actions/workflows/ci.yml/badge.svg)](https://github.com/whisper-sec/sdk-csharp/actions/workflows/ci.yml)
[![NuGet](https://img.shields.io/nuget/v/Whisper.Api.Sdk.svg)](https://www.nuget.org/packages/Whisper.Api.Sdk)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)

> **Official C# SDK for Whisper API** - Comprehensive threat intelligence and security operations for domains, IPs, and web infrastructure.

**[Website](https://www.whisper.security)** | **[Documentation](https://docs.whisper.security)** | **[API Reference](https://developer.whisper.security)** | **[API Playground](https://dash.whisper.security/playground)** | **[Contact Us](https://www.whisper.security/contactus)**

</div>

---

## Quick Start

### Installation

```bash
dotnet add package Whisper.Api.Sdk
```

**Or via Package Manager:**
```powershell
Install-Package Whisper.Api.Sdk
```

### Get Your API Key

Sign up at [dash.whisper.security](https://dash.whisper.security) to get your API key.

### First Request

```csharp
using Whisper.Api.Sdk.Api;
using Whisper.Api.Sdk.Client;

var config = new Configuration();
config.BasePath = "http://api.whisper.security";
config.AccessToken = "YOUR_API_KEY";

var api = new IndicatorsApi(config);

// Enrich an IP address
var response = await api.GetIndicatorAsync("ip", "8.8.8.8");
Console.WriteLine(response);
```

---

## Key Features

- **Async/Await** - Modern async programming model
- **Fully Typed** - Complete type definitions with IntelliSense support
- **Comprehensive** - IP, Domain, DNS, WHOIS, Routing, Geolocation, Screenshots, AI/ML
- **Fast** - Sub-500ms typical response times with strategic caching
- **.NET 6+** - Compatible with .NET 6, 7, and 8

---

## API Overview

### Indicators API
Enrich IPs and domains with comprehensive threat intelligence.

```csharp
var api = new IndicatorsApi(config);

// Basic enrichment
var ipData = await api.GetIndicatorAsync("ip", "8.8.8.8");

// With additional data modules
var domainData = await api.GetIndicatorAsync("domain", "example.com", "whois,dns_details");

// Get relationship graph
var graph = await api.GetIndicatorGraphAsync("ip", "8.8.8.8");

// Historical data
var history = await api.GetIndicatorHistoryAsync("domain", "example.com", 10);

// Predictive risk score (AI-powered)
var risk = await api.GetPredictiveRiskAsync("ip", "8.8.8.8");

// Subdomain discovery
var subdomains = await api.GetSubdomainsAsync("example.com", 100);
```

### Location API
Geolocation lookups and network analysis.

```csharp
var api = new LocationApi(config);

// Single IP geolocation
var location = await api.GetIpLocationAsync("8.8.8.8");

// Bulk geolocation (up to 1000 IPs)
var bulkResult = await api.GetBulkIpLocationAsync(bulkRequest);

// Network/CIDR lookup
var network = await api.GetNetworkLocationAsync("8.8.8.0/24");

// Search by attributes
var results = await api.SearchLocationAsync("city", "San Francisco", 100);
```

### Operations API
Async operations for scanning, monitoring, and AI-powered analysis.

```csharp
var api = new OperationsApi(config);

// Screenshot capture (returns job ID)
var job = await api.CreateScreenshotAsync(screenshotRequest);

// Infrastructure scan
var scanJob = await api.CreateInfrastructureScanAsync(scanRequest);

// Check job status
var status = await api.GetJobAsync(job.JobId);

// AI-powered investigation
var investigation = await api.AiInvestigateAsync(investigateRequest);

// Similar threat cases
var cases = await api.AiSimilarCasesAsync(similarCasesRequest);
```

---

## Authentication

All endpoints require Bearer token authentication:

```csharp
var config = new Configuration
{
    BasePath = "http://api.whisper.security",
    AccessToken = Environment.GetEnvironmentVariable("WHISPER_API_KEY")
};
```

---

## Rate Limits

| Category | Limit |
|----------|-------|
| Standard Enrichment | 100 req/min |
| Bulk Operations | 10 req/min |
| Search/Discovery | 5 req/min |
| Screenshots | 10 req/min |

Rate limits return HTTP 429 with a `Retry-After` header.

---

## Documentation

- **API Documentation**: [docs.whisper.security](https://docs.whisper.security)
- **API Reference**: [developer.whisper.security](https://developer.whisper.security)
- **XML Docs**: See the `docs/` directory

---

## Support

- **Email**: [support@whisper.security](mailto:support@whisper.security)
- **Issues**: [github.com/whisper-sec/sdk-csharp/issues](https://github.com/whisper-sec/sdk-csharp/issues)

---

## License

MIT License - See [LICENSE](LICENSE) file for details.

---

*Built with C# by Whisper Security*
