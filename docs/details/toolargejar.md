# Too Large JAR files

Some Spark systems have limits on the size files of their jars and in other cases large JARs can cause slow executor startup time.

Regardless of if it's a hard limit or slowing your job down there are a few things you can do to try and minimize your JAR.
- Make sure cluster dependencies (Spark, Hadoop, etc.) are marked as `provided` or `compileOnly`
- Extract the uber jar and run `du -h` to look at it's contents
- You can then use dependency tree to see what is bringing in the large dependencies and see if any of them were accidentally included
- Try and see if there are client libraries for desired systems to access which do not bring in the whole system (e.g. open search).
