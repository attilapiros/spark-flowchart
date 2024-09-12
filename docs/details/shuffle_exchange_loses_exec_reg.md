# ShuffleExchangeExec loses track of executor registrations

If you encounter a Spark job failing with a lot of shuffle fetch failures but no corresponding loss of shuffle services

It seems that:
 ``` a fault-tolerance edge-case which can cause Spark jobs to fail if a single external shuffle service process reboots and fails to recover the list of registered executors (something which can happen when using YARN if NodeManager recovery is disabled) and the Spark job has a large number of executors per host.
```

Ultimately the resolution was to add to the config for the sparksql session:
setting spark.files.fetchFailure.unRegisterOutputOnHost" to true

[link to issue tracked in Spark JIRA](https://issues.apache.org/jira/browse/SPARK-27736?page=com.atlassian.jira.plugin.system.issuetabpanels%3Aall-tabpanel)
