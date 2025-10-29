# Whisper.Api.Sdk.Model.DomainReputationScores
Domain reputation calculated from infrastructure IP scores

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**OverallScore** | **double** | Overall reputation score (0-100, higher &#x3D; more suspicious) | [optional] 
**RiskLevel** | **string** | Risk classification based on overall score | [optional] 
**DomainIpScore** | **double** | Average IP reputation score for domain&#39;s A records | [optional] 
**NameserverIpScore** | **double** | Average IP reputation score for nameserver IPs | [optional] 
**MailserverIpScore** | **double** | Average IP reputation score for mail server IPs | [optional] 
**Details** | [**DomainReputationDetails**](DomainReputationDetails.md) |  | [optional] 
**ScoringMethod** | **string** | Scoring methodology used | [optional] 
**Weights** | **Dictionary&lt;string, double&gt;** | Weighting strategy applied to infrastructure components | [optional] 

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

