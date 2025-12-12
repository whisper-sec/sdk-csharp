# Whisper.Api.Sdk.Model.ReputationInfo
Reputation scoring and blacklist information for threat assessment

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**RiskScore** | **double** | Composite risk score (0-10, higher &#x3D; riskier) | [optional] 
**Blacklists** | [**BlacklistScores**](BlacklistScores.md) | Blacklist presence scores across various threat feeds | [optional] 
**DomainReputation** | [**DomainReputationScores**](DomainReputationScores.md) | Domain reputation based on infrastructure IP scoring (domains only) | [optional] 

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

