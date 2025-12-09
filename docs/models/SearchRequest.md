# Whisper.Api.Sdk.Model.SearchRequest
Search query for finding domains matching WHOIS registration criteria.  **Query Modes:** 1. **Field-based (recommended):** Specify individual fields like `registrantCompany`, `tld`, etc. 2. **Query string:** Use `query` field with `field:value` syntax for compatibility.  Multiple criteria are combined with AND logic. Results are paginated with a maximum of 100 results per page.  **Use Cases:** - Threat hunting: Find domains registered by known malicious actors - Brand protection: Monitor for domains similar to your brand - Infrastructure discovery: Map domains sharing registrants or nameservers - Investigation: Track domains created on specific dates 

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**EffectivePage** | **int** |  | [optional] 
**Query** | **string** | Search query using field:value syntax (alternative to individual field parameters). If individual field parameters are provided, they take precedence.  **Supported Syntax:** - Single field: &#x60;registrantCompany:Google&#x60; - Multiple fields: &#x60;registrantCompany:Google registrantCountry:US&#x60;  **Note:** For new integrations, prefer using individual field parameters instead of query syntax.  | [optional] 
**Field** | **string** | Field to search in when using simple query mode. Use with &#x60;query&#x60; parameter. | [optional] 
**Tld** | **string** | Top-Level Domain to filter by (exact match). Examples: com, org, net, io | [optional] 
**RegistrarName** | **string** | Domain registrar name to filter by (exact match) | [optional] 
**RegistrarIanaId** | **string** | IANA registrar ID to filter by (exact match) | [optional] 
**RegistrantName** | **string** | Registrant name to search for (text search, partial match) | [optional] 
**RegistrantCompany** | **string** | Registrant company/organization to search for (text search, partial match) | [optional] 
**RegistrantEmail** | **string** | Registrant email to search for (text search). Supports wildcards like *@example.com | [optional] 
**RegistrantPhone** | **string** | Registrant phone number to search for (text search) | [optional] 
**RegistrantCountry** | **string** | Registrant country code to filter by (2-letter ISO code) | [optional] 
**RegistrantCity** | **string** | Registrant city to search for (text search) | [optional] 
**NameServer** | **string** | Name server hostname to search for (text search) | [optional] 
**DomainStatus** | **string** | Domain status flag to search for (text search). E.g., clientTransferProhibited | [optional] 
**CreatedDate** | **string** | Domain creation date to filter by (exact match, format: YYYY-MM-DD) | [optional] 
**UpdatedDate** | **string** | Domain last update date to filter by (exact match, format: YYYY-MM-DD) | [optional] 
**ExpiryDate** | **string** | Domain expiry date to filter by (exact match, format: YYYY-MM-DD) | [optional] 
**Limit** | **int** | Maximum number of results to return per page (max 100 for WHOIS searches) | [optional] [default to 100]
**Page** | **int** | Page number for pagination (0-indexed). Alternative to offset. | [optional] [default to 0]
**Offset** | **int** | Number of results to skip for pagination. Converted to page internally. | [optional] [default to 0]

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

