# Whisper.Api.Sdk.Model.PredictiveRiskResponse
ML-based predictive risk assessment for an indicator

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Query** | [**QueryInfo**](QueryInfo.md) | Query metadata | [optional] 
**CurrentAssessment** | [**CurrentAssessment**](CurrentAssessment.md) | Current risk assessment | [optional] 
**Predictions** | [**Predictions**](Predictions.md) | Future risk predictions | [optional] 
**Trajectory** | [**TrajectoryInfo**](TrajectoryInfo.md) | Risk trajectory details | [optional] 
**RiskFactors** | [**List&lt;RiskFactor&gt;**](RiskFactor.md) | Contributing risk factors | [optional] 
**PatternMatching** | [**PatternMatching**](PatternMatching.md) | Pattern matching insights | [optional] 
**EarlyWarnings** | [**List&lt;EarlyWarning&gt;**](EarlyWarning.md) | Early warning signals | [optional] 
**SimilarCases** | [**List&lt;SimilarCase&gt;**](SimilarCase.md) | Similar historical cases | [optional] 
**ModelInfo** | [**ModelInfo**](ModelInfo.md) | ML model information | [optional] 

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

