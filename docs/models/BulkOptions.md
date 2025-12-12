# Whisper.Api.Sdk.Model.BulkOptions
Advanced configuration options for bulk processing including batch size, timeouts, and error handling.

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**ParallelProcessing** | **bool** | Enable parallel processing of indicators for faster results | [optional] [default to true]
**BatchSize** | **int** | Number of indicators to process in each batch. Smaller batches &#x3D; more frequent progress updates | [optional] [default to 10]
**TimeoutPerIndicator** | **int** | Maximum time in milliseconds to wait for each indicator before timing out. Domain enrichment and ip_intelligence require longer timeouts. | [optional] [default to 30000]
**ContinueOnError** | **bool** | Continue processing remaining indicators if one fails. Recommended for large batches. | [optional] [default to true]
**IncludeFailed** | **bool** | Include failed indicators in the response with error details | [optional] [default to false]

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

