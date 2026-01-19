Spark Error Flowchart: Note this uses mermaid.js which may take awhile to load.

```mermaid
flowchart LR

A[Start here] --> B[Slow Running Job]
C[I have an exception or error]
A --> C
click B "./slow"
click C "./error"
```
