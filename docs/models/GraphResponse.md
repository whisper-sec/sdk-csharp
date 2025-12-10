# Whisper.Api.Sdk.Model.GraphResponse
Graph visualization data showing relationships between infrastructure elements. Format is compatible with react-force-graph, vis.js, cytoscape.js, and similar libraries.

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Nodes** | [**List&lt;GraphNode&gt;**](GraphNode.md) | List of nodes (vertices) in the graph. Each node represents an infrastructure element. | [optional] 
**Links** | [**List&lt;GraphLink&gt;**](GraphLink.md) | List of links (edges) connecting nodes. Each link represents a relationship between elements. | [optional] 
**TotalNodes** | **int** | Total count of nodes before any limit was applied | [optional] 
**TotalLinks** | **int** | Total count of links before any limit was applied | [optional] 

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

