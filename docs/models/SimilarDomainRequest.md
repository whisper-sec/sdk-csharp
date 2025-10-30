# Whisper.Api.Sdk.Model.SimilarDomainRequest
Configuration for generating similar domain variations for brand protection and threat hunting

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Techniques** | **HashSet&lt;string&gt;** | Types of domain variations to generate | [optional] 
**Limit** | **int** | Maximum number of similar domains to generate | [optional] [default to 100]
**CheckRegistration** | **bool** | Check if generated domains are registered | [optional] [default to false]
**IncludeDns** | **bool** | Include DNS resolution data for registered domains | [optional] [default to false]
**IncludeRiskScore** | **bool** | Calculate risk scores for each variation | [optional] [default to true]
**TechniqueConfig** | [**TechniqueConfig**](TechniqueConfig.md) |  | [optional] 

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

