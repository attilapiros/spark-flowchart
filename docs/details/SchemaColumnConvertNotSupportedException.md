# SchemaColumnConvertNotSupportedException with vectorized Parquet reads

It's a known limitation that the vectorized parquet reader for Spark has the following caveats for timestamp-type data:

- a timezone is expected with the timestamp-type data
- timestamp data must not be stored as Int96
- timestamp precision must be in microseconds, higher precision (ie. nanoseconds) not supported

If one of the above requirements is violated by timestamp-type data, then jobs with vectorized parquet scanner enabled may fail with `SchemaColumnConvertNotSupportedException`

To overcome this, do one of the following:

- Consider using dateint instead of timestamp type, since it doesn't have the complexities of timezones and precision, and is simpler for the vectorized reader to handle
- Correct the timestamp-type data to adhere to the requirements above
- Disable the vectorized parquet reader for the job (ie. set `spark.sql.parquet.enableVectorizedReader` to `false`)

There is a [related StackOverflow post SchemaColumnConvertNotSupportedException: column: ](https://stackoverflow.com/questions/78779482/schemacolumnconvertnotsupportedexception-column-col-name-physicaltype-int6) & [databricks KB entry](https://kb.databricks.com/scala/spark-job-fail-parquet-column-convert)
