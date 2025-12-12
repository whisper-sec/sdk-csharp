<div align="center">
  <img src="Whisper_Logo.png" alt="Whisper Logo" width="400"/>

  # Whisper API SDK - C#

[![CI](https://github.com/whisper-sec/sdk-csharp/actions/workflows/ci.yml/badge.svg)](https://github.com/whisper-sec/sdk-csharp/actions/workflows/ci.yml)
[![NuGet](https://img.shields.io/nuget/v/Whisper.Api.Sdk.svg)](https://www.nuget.org/packages/Whisper.Api.Sdk)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)

> **Official C# SDK for Whisper API** - Comprehensive threat intelligence and security operations for domains, IPs, and web infrastructure.

**[Website](https://whisper.security)** | **[Dashboard](https://dash.whisper.security)** | **[Documentation](https://docs.whisper.security)** | **[API Reference](https://developer.whisper.security)** | **[API Playground](https://dash.whisper.security/playground)** | **[Contact Us](https://whisper.security/contactus)**

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
config.BasePath = "https://api.whisper.security";
config.AccessToken = "YOUR_API_KEY";

var api = new EnrichmentApi(config);

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

### Enrichment API
Enrich IPs and domains with comprehensive threat intelligence.

```csharp
var api = new EnrichmentApi(config);

// Basic enrichment
var ipData = await api.GetIndicatorAsync("ip", "8.8.8.8");

// With additional data modules
var domainData = await api.GetIndicatorAsync("domain", "example.com", "whois,dns_details,routing,rpki");

// Get relationship graph
var graph = await api.GetIndicatorGraphAsync("ip", "8.8.8.8");

// Historical data
var history = await api.GetIndicatorHistoryAsync("domain", "example.com", 10);

// Predictive risk score (AI-powered)
var risk = await api.GetPredictiveRiskAsync("ip", "8.8.8.8");

// Subdomain discovery
var subdomains = await api.GetSubdomainsAsync("example.com", 100);

// Bulk enrichment (async job)
var job = await api.BulkEnrichmentAsync(bulkRequest);

// Search by WHOIS fields
var searchJob = await api.SearchIndicatorsAsync(searchRequest);

// Similar/typosquat domain generation
var similarJob = await api.SimilarDomainsAsync(similarRequest);
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

// Location statistics
var stats = await api.GetLocationStatsAsync();
```

### Screenshots API
Capture and schedule website screenshots.

```csharp
var api = new ScreenshotsApi(config);

// Screenshot capture (returns job ID)
var job = await api.CreateScreenshotAsync(screenshotRequest);

// Schedule recurring screenshots
var schedule = await api.ScheduleScreenshotAsync(scheduleRequest);

// Get screenshot history
var history = await api.GetScreenshotHistoryAsync("https://example.com");

// List scheduled screenshots
var schedules = await api.ListScreenshotSchedulesAsync();
```

### AI Intelligence API
AI-powered threat investigation and analysis.

```csharp
var api = new AiIntelligenceApi(config);

// Industry security benchmark (synchronous)
var benchmark = await api.GetIndustryBenchmarkAsync("financial_services", "enterprise");

// AI-powered investigation (async job)
var investigation = await api.AiInvestigateAsync(investigateRequest);

// Find similar threat cases
var cases = await api.FindSimilarCasesAsync(similarCasesRequest);

// Infrastructure pivoting
var pivot = await api.AiPivotAsync(pivotRequest);

// Threat actor attribution
var attribution = await api.AiAttributeAsync(attributeRequest);

// Global indicator correlation
var correlation = await api.AiCorrelateAsync(correlateRequest);
```

### Infrastructure Scanning API
Discover and analyze infrastructure.

```csharp
var api = new InfrastructureScanningApi(config);

// Infrastructure scan (SSL, technologies, subdomains, ports)
var scanJob = await api.CreateInfrastructureScanAsync(scanRequest);

// Infrastructure relationship mapping
var mapJob = await api.CreateInfrastructureMapAsync(mapRequest);
```

### Monitoring API
Uptime and availability monitoring.

```csharp
var api = new MonitoringApi(config);

// Create monitoring check
var check = await api.CreateMonitorCheckAsync(monitorRequest);

// List monitoring checks
var checks = await api.ListMonitorChecksAsync();

// Get dashboard summary
var dashboard = await api.GetMonitorDashboardAsync();

// Configure alerts
await api.CreateMonitoringAlertAsync(checkId, alertRequest);
```

### Change Tracking API
Monitor indicators for changes.

```csharp
var api = new ChangeTrackingApi(config);

// Start tracking an indicator
await api.StartChangeTrackingAsync("domain", "example.com", trackingRequest);

// Get detected changes
var changes = await api.GetChangesAsync("domain", "example.com");

// List tracked indicators
var tracked = await api.ListTrackedIndicatorsAsync();

// Trigger immediate check
await api.TriggerCheckAsync("domain", "example.com");
```

### Graph Database API
Direct access to the threat intelligence graph.

```csharp
var api = new GraphDatabaseApi(config);

// Execute Cypher query
var result = await api.ExecuteCypherQueryAsync(cypherRequest);

// Execute GraphQL query
var graphqlResult = await api.ExecuteGraphQLAsync(graphqlRequest);

// Get graph schema
var schema = await api.GetSchemaAsync();

// Check graph health
var health = await api.GetHealthAsync();
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
var config = new Configuration
{
    BasePath = "https://api.whisper.security",
    AccessToken = Environment.GetEnvironmentVariable("WHISPER_API_KEY")
};
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
| Monitoring | 10 req/sec |
| Change Tracking | 10 req/sec |
| AI Operations | 5 req/min |

Rate limits return HTTP 429 with a `Retry-After` header.

---

## Documentation

- **API Documentation**: [docs.whisper.security](https://docs.whisper.security)
- **API Reference**: [developer.whisper.security](https://developer.whisper.security)
- **XML Docs**: See the `docs/` directory

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

---

*Built with C# by [Whisper Security](https://whisper.security)*
