# Whisper.Api.Sdk.Model.MonitorDashboardResponse
Monitoring dashboard summary

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**TotalChecks** | **int** | Total number of checks | [optional] 
**PassingChecks** | **int** | Number of passing checks | [optional] 
**FailingChecks** | **int** | Number of failing checks | [optional] 
**DegradedChecks** | **int** | Number of degraded checks | [optional] 
**OverallStatus** | **string** | Overall status | [optional] 
**AvgUptime24Hours** | **double** | Average uptime percentage over the last 24 hours | [optional] 
**AvgUptime7Days** | **double** | Average uptime percentage over the last 7 days | [optional] 
**AvgUptime30Days** | **double** | Average uptime percentage over the last 30 days | [optional] 
**AvgResponseTime** | **long** | Average response time across all checks in milliseconds | [optional] 
**ChecksByType** | **Dictionary&lt;string, int&gt;** | Count of checks by type | [optional] 
**ChecksByStatus** | **Dictionary&lt;string, int&gt;** | Count of checks by status | [optional] 
**LastUpdated** | **DateTime** | When this dashboard data was last updated | [optional] 

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

