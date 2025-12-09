# Whisper.Api.Sdk.Model.SimilarDomainsOpsRequest
Request for generating similar/lookalike domains for brand protection

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Domain** | **string** | The target domain to generate variations for | 
**Techniques** | **string** | Techniques to use for generating similar domains. Supported values: typosquatting, homoglyph, bitsquatting, tld_variation, sounding, prefix, suffix, contains, levenshtein. If not specified, defaults to typosquatting. | [optional] 
**Limit** | **int** | Maximum number of similar domains to return per technique | [optional] 
**Options** | **Object** |  | [optional] 

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

