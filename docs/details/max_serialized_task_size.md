# Max Serialized Task Size -- Serialized task A:B was X bytes, which exceeds max allowed: C spark.rpc.message.maxSize 

Some common causes of this include:
- Too large task through inadvertant scope capture (think a function on an object needing to bring an object that happens to have a bunch of records in it)
  - sometimes this can be fixed by making those fields transient
  - moving the function out to another class
- Too large task due to intentional/needed data
  - Using broadcast variables can be a way to work around this.
- Intentional coalesece of all data into one task (generally not recommended but sometimes needed)
  - You can increase `spark.rpc.message.maxSize`
