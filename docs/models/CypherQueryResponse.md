# Whisper.Api.Sdk.Model.CypherQueryResponse
Response from executing a Cypher query against the graph database.  Contains the query results as a list of records, along with execution metadata including timing and column information. 

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Results** | **List&lt;Dictionary&lt;string, Object&gt;&gt;** | Query results as a list of records. Each record is a map of column name to value. | [optional] 
**ExecutionTimeMs** | **long** | Query execution time in milliseconds | [optional] 
**RowCount** | **int** | Number of rows returned | [optional] 
**Columns** | **List&lt;string&gt;** | Column names in the result set | [optional] 
**Truncated** | **bool** | Whether the result was truncated due to limit | [optional] 
**Error** | **string** | Error message if the query failed | [optional] 

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

