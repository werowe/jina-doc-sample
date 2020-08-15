# Common designs patterns
jina is an AI-powered neural search framework. It lets you frame any pattern as a neural search problem. (To do:  define **pattern**.)

There are basic basic common patterns that show when developing search solutions with jina. Here is a list of some of them.


- CompoundIndexer (Vector + KV Indexers):

To develop neural search applications, you can use a `CompoundIndexer` in same `Pod` for both `index` and `query` flows.  

<p class="callout success">
<table border="1">
  <tr>
    <th colspan="2">Definitions</th>
  </tr>
     <tr> <td>Term</td><td>Definition</td></tr>
     <tr><td><strong>pod</strong></td><td>To do</td>/tr>
     <tr><td><strong>index</strong></td><td>To do</td>/tr>  
     <tr><td><strong>query</strong></td><td>To do</td>/tr> 
     <tr><td><strong>flow</strong></td><td>To do</td>/tr> 
</table>

Here is an example pattern:

```
!CompoundIndexer
components:
  - !NumpyIndexer
    with:
      index_filename: vectors.gz
      metric: cosine
    metas:
      name: vecIndexer
  - !BinaryPbIndexer
    with:
      index_filename: values.gz
    metas:
      name: kvIndexer  # a customized name
metas:
  name: complete indexer
```
 

This constructor will act as an single `indexer`. Some points to note:

* It will let you and `query` this (which?) index.  
* The `embedding` vector can coming from any upstream `encoder`.
* The response message of the pod the corresponding `binary` information is stored inthe key-value index. 

This lets the `VectorIndexer` be responsible for obtaining the most relevant documents.  It does this bying finding similarities in the `embedding` space while targeting the `key-value` database to extract meaningful (useful?  relevnt?) data and fields from those documents.

