# Common designs patterns
jina is an AI-powered neural search framework. It lets you frame any pattern as a neural search problem. (Definition: a **pattern** is YAML document that give the parameters of a neural search.)

There are basic patterns that are common to all searches. Here are some of them.


## CompoundIndexer (Vector + KV Indexers) 

Here we use a `CompoundIndexer`.  We use it in same `Pod` for both `index` and `query` flows.  

 | Term | Definition |
| ----------- | ----------- |
| pattern | To Do |
| pod | To Do |
| index | To Do |
| query | To Do |
| flow | To Do |

 
 

```yaml
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
 

This constructor acts as an single `indexer`. 

Some items to note:

* This pattern will let you `query` this (which?) index.  
* The `embedding` vector can come from any upstream `encoder`.
* The corresponding `binary` pod response message is stored in a key-value index. This lets the `VectorIndexer` be responsible for obtaining the most relevant documents.  It does this bying finding similarities in the `embedding` space while targeting the `key-value` database to extract meaningful (need better word **useful**?  **relevant**?) data and fields.

