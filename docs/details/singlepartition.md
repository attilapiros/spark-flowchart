# Unexpected coalesce / shuffle down  /  SinglePartition, ENSURE_REQUIREMENTS

In Spark SQL there can be several cases which can cause an unexpected coalesce, exchange, or SinglePartition and these will, almost always, cause Spark to fail.


For Spark users prior to 3.4 working with Iceberg or Deltalake, tables which are partioned or sorted can result in the optimizer being fed unhelpful hints about how to structure the output. Upgradeding to the most recent catalog + Spark > 3.4 will work around the majourity of those situations.


We often know to look out for explicit groupByKeys w/non-partial aggregations, but windowing can have the same effect.
