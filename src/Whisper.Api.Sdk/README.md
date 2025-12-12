# Created with Openapi Generator

<a id="cli"></a>
## Creating the library
Create a config.yaml file similar to what is below, then run the following powershell command to generate the library `java -jar "<path>/openapi-generator/modules/openapi-generator-cli/target/openapi-generator-cli.jar" generate -c config.yaml`

```yaml
generatorName: csharp
inputSpec: /home/runner/work/frontgraph/frontgraph/unified-spec.yaml
outputDir: out

# https://openapi-generator.tech/docs/generators/csharp
additionalProperties:
  packageGuid: '{476DBECD-65FE-4AB1-BC41-C01370D2F654}'

# https://openapi-generator.tech/docs/integrations/#github-integration
# gitHost:
# gitUserId:
# gitRepoId:

# https://openapi-generator.tech/docs/globals
# globalProperties:

# https://openapi-generator.tech/docs/customization/#inline-schema-naming
# inlineSchemaOptions:

# https://openapi-generator.tech/docs/customization/#name-mapping
# modelNameMappings:
# nameMappings:

# https://openapi-generator.tech/docs/customization/#openapi-normalizer
# openapiNormalizer:

# templateDir: https://openapi-generator.tech/docs/templating/#modifying-templates

# releaseNote:
```

<a id="usage"></a>
## Using the library in your project

```cs
using Microsoft.Extensions.Hosting;
using Microsoft.Extensions.DependencyInjection;
using Whisper.Api.Sdk.Api;
using Whisper.Api.Sdk.Client;
using Whisper.Api.Sdk.Model;
using Org.OpenAPITools.Extensions;

namespace YourProject
{
    public class Program
    {
        public static async Task Main(string[] args)
        {
            var host = CreateHostBuilder(args).Build();
            var api = host.Services.GetRequiredService<IAIIntelligenceApi>();
            IAiAttributeApiResponse apiResponse = await api.AiAttributeAsync("todo");
            AttributeResult model = apiResponse.Ok();
        }

        public static IHostBuilder CreateHostBuilder(string[] args) => Host.CreateDefaultBuilder(args)
          .ConfigureApi((context, services, options) =>
          {
              // The type of token here depends on the api security specifications
              // Available token types are ApiKeyToken, BasicToken, BearerToken, HttpSigningToken, and OAuthToken.
              BearerToken token = new("<your token>");
              options.AddTokens(token);

              // optionally choose the method the tokens will be provided with, default is RateLimitProvider
              options.UseProvider<RateLimitProvider<BearerToken>, BearerToken>();

              options.ConfigureJsonOptions((jsonOptions) =>
              {
                  // your custom converters if any
              });

              options.AddApiHttpClients(client =>
              {
                  // client configuration
              }, builder =>
              {
                  builder
                      .AddRetryPolicy(2)
                      .AddTimeoutPolicy(TimeSpan.FromSeconds(5))
                      .AddCircuitBreakerPolicy(10, TimeSpan.FromSeconds(30));
                      // add whatever middleware you prefer
                  }
              );
          });
    }
}
```
<a id="questions"></a>
## Questions

- What about HttpRequest failures and retries?
  Configure Polly in the IHttpClientBuilder
- How are tokens used?
  Tokens are provided by a TokenProvider class. The default is RateLimitProvider which will perform client side rate limiting.
  Other providers can be used with the UseProvider method.
- Does an HttpRequest throw an error when the server response is not Ok?
  It depends how you made the request. If the return type is ApiResponse<T> no error will be thrown, though the Content property will be null.
  StatusCode and ReasonPhrase will contain information about the error.
  If the return type is T, then it will throw. If the return type is TOrDefault, it will return null.
- How do I validate requests and process responses?
  Use the provided On and After partial methods in the api classes.

## Api Information
- appName: Whisper Security API
- appVersion: 1.0.0
- appDescription: # Whisper Security Threat Intelligence API  The Whisper Security API provides comprehensive threat intelligence, geolocation data, and security operations capabilities for enterprise security teams and developers.  ## Key Capabilities  - **Indicator Enrichment**: Get comprehensive intelligence on IP addresses and domains including   geolocation, WHOIS, DNS, reputation scoring, and relationship mapping. - **Geolocation Services**: Fast IP-to-location lookups with ISP, ASN, and network information. - **Security Operations**: Asynchronous tools for bulk enrichment, infrastructure scanning,   AI-powered threat investigation, and monitoring.  ## API Design  - **RESTful**: Standard HTTP methods (GET, POST, PUT, DELETE) with JSON request/response bodies. - **Synchronous Endpoints**: Fast responses (&lt;500ms) for indicator enrichment and geolocation. - **Asynchronous Jobs**: Long-running operations return a job ID for polling results. - **Consistent Error Handling**: Standardized error responses with status codes, error codes, and messages.  ## Authentication  All API endpoints require Bearer token authentication. Include your API key in the &#x60;Authorization&#x60; header: &#x60;Authorization: Bearer &lt;your-api-key&gt;&#x60;  ## Rate Limits  Rate limits are applied per-user and vary by endpoint category:  | Endpoint Category | Rate Limit | Description | |- -- -- -- -- -- -- -- -- --|- -- -- -- -- -- -|- -- -- -- -- -- --| | Indicators (&#x60;/v1/indicators/_*&#x60;) | 100 req/sec | Single indicator enrichment | | Location (&#x60;/v1/location/_*&#x60;) | 100 req/sec | Geolocation lookups | | Jobs (&#x60;/v1/ops/jobs/_*&#x60;) | 100 req/sec | Job status and listing | | Bulk Operations (&#x60;/v1/ops/enrichment/bulk&#x60;) | 10 req/sec | Bulk indicator processing | | Screenshots (&#x60;/v1/ops/screenshots/_*&#x60;) | 10 req/sec | Screenshot capture and scheduling | | Scans (&#x60;/v1/ops/scans/_*&#x60;) | 10 req/sec | Infrastructure scanning | | Monitoring (&#x60;/v1/ops/monitoring/_*&#x60;) | 10 req/sec | Uptime monitoring | | Tracking (&#x60;/v1/ops/tracking/_*&#x60;) | 10 req/sec | Change tracking | | AI Investigate (&#x60;/v1/ops/ai/investigate&#x60;) | 5 req/min | Deep threat investigation | | AI Correlate (&#x60;/v1/ops/ai/correlate&#x60;) | 5 req/min | Global correlation | | AI Attribute (&#x60;/v1/ops/ai/attribute&#x60;) | 5 req/min | Threat actor attribution | | AI Pivot (&#x60;/v1/ops/ai/pivot&#x60;) | 5 req/min | Infrastructure pivoting |  When rate limits are exceeded, the API returns HTTP &#x60;429 Too Many Requests&#x60; with a &#x60;Retry-After&#x60; header indicating when you can retry. The response body includes: &#x60;&#x60;&#x60;json {   \&quot;error\&quot;: \&quot;Too Many Requests\&quot;,   \&quot;message\&quot;: \&quot;Rate limit exceeded for &lt;category&gt;. Please retry after N seconds.\&quot;,   \&quot;retryAfter\&quot;: N } &#x60;&#x60;&#x60;  ## Response Conventions  - All timestamps are in ISO 8601 format (UTC). - Pagination uses &#x60;limit&#x60; and &#x60;offset&#x60; parameters. - Field names use camelCase throughout the API.  ## Official SDKs  - **Python**: [github.com/whisper-sec/sdk-python](https://github.com/whisper-sec/sdk-python) - **TypeScript/JavaScript**: [github.com/whisper-sec/sdk-typescript](https://github.com/whisper-sec/sdk-typescript) - **Java**: [github.com/whisper-sec/sdk-java](https://github.com/whisper-sec/sdk-java) - **C#/.NET**: [github.com/whisper-sec/sdk-csharp](https://github.com/whisper-sec/sdk-csharp)  ## Resources  - **Website**: [whisper.security](https://whisper.security) - **Dashboard**: [dash.whisper.security](https://dash.whisper.security) - Manage API keys and view usage - **Documentation**: [docs.whisper.security](https://docs.whisper.security) - Guides and tutorials 

## Build
This C# SDK is automatically generated by the [OpenAPI Generator](https://openapi-generator.tech) project.

- SDK version: 1.0.0
- Generator version: 7.17.0
- Build package: org.openapitools.codegen.languages.CSharpClientCodegen
