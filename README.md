# Patch information

This patch is based on backpatching Spark-1.6.1-RELEASE for RandomForests save/load fix from Spark 2.0.0-PRE.

Spark-1.6.1-RELEASE was from:

https://github.com/apache/spark/releases/tag/v1.6.1

The patch also is affected for:

\mllib\src\main\scala\org\apache\spark\ml\classification\DecisionTreeClassifier.scala

\mllib\src\main\scala\org\apache\spark\ml\classification\GBTClassifier.scala

\mllib\src\main\scala\org\apache\spark\ml\classification\RandomForestClassifier.scala

\mllib\src\main\scala\org\apache\spark\ml\feature\RFormula.scala

\mllib\src\main\scala\org\apache\spark\ml\param\params.scala

\mllib\src\main\scala\org\apache\spark\ml\param\shared\sharedParams.scala

\mllib\src\main\scala\org\apache\spark\ml\regression\DecisionTreeRegressor.scala

\mllib\src\main\scala\org\apache\spark\ml\regression\GBTRegressor.scala

\mllib\src\main\scala\org\apache\spark\ml\regression\RandomForestRegressor.scala

\mllib\src\main\scala\org\apache\spark\ml\tree\Split.scala

\mllib\src\main\scala\org\apache\spark\ml\tree\treeModels.scala

\mllib\src\main\scala\org\apache\spark\ml\tree\treeParams.scala

\mllib\src\main\scala\org\apache\spark\ml\util\ReadWrite.scala

\mllib\src\main\scala\org\apache\spark\mllib\tree\impurity\Impurity.scala

\mllib\src\test\scala\org\apache\spark\ml\classification\RandomForestClassifierSuite.scala

\mllib\src\test\scala\org\apache\spark\ml\regression\RandomForestRegressorSuite.scala

## How to build

Advice: build only on unix systems like Linux.

git clone https://github.com/olegnikolaenkoib/spark-1.6.1-patched

cd spark-1.6.1-patched

dev/change-scala-version.sh 2.11

build/mvn -Pyarn -Phive -Phive-thriftserver -Phadoop-2.6 -Dhadoop.version=2.7.2 -Dscala-2.11 -T 1C -DskipTests clean package

dev/make-distribution.sh --name custom --tgz --with-tachyon -Pyarn -Phive -Phive-thriftserver -Phadoop-2.6 -Dhadoop.version=2.7.2 -Dscala-2.11 -T 1C


## Build troubleshooting

Issue:

[error] Required file not found: sbt-interface.jar

Solution:

rm -rf build/zinc-0.3.5.3

and try again


# Apache Spark

Spark is a fast and general cluster computing system for Big Data. It provides
high-level APIs in Scala, Java, Python, and R, and an optimized engine that
supports general computation graphs for data analysis. It also supports a
rich set of higher-level tools including Spark SQL for SQL and DataFrames,
MLlib for machine learning, GraphX for graph processing,
and Spark Streaming for stream processing.

<http://spark.apache.org/>


## Online Documentation

You can find the latest Spark documentation, including a programming
guide, on the [project web page](http://spark.apache.org/documentation.html)
and [project wiki](https://cwiki.apache.org/confluence/display/SPARK).
This README file only contains basic setup instructions.

## Building Spark

Spark is built using [Apache Maven](http://maven.apache.org/).
To build Spark and its example programs, run:

    build/mvn -DskipTests clean package

(You do not need to do this if you downloaded a pre-built package.)
More detailed documentation is available from the project site, at
["Building Spark"](http://spark.apache.org/docs/latest/building-spark.html).

## Interactive Scala Shell

The easiest way to start using Spark is through the Scala shell:

    ./bin/spark-shell

Try the following command, which should return 1000:

    scala> sc.parallelize(1 to 1000).count()

## Interactive Python Shell

Alternatively, if you prefer Python, you can use the Python shell:

    ./bin/pyspark

And run the following command, which should also return 1000:

    >>> sc.parallelize(range(1000)).count()

## Example Programs

Spark also comes with several sample programs in the `examples` directory.
To run one of them, use `./bin/run-example <class> [params]`. For example:

    ./bin/run-example SparkPi

will run the Pi example locally.

You can set the MASTER environment variable when running examples to submit
examples to a cluster. This can be a mesos:// or spark:// URL,
"yarn" to run on YARN, and "local" to run
locally with one thread, or "local[N]" to run locally with N threads. You
can also use an abbreviated class name if the class is in the `examples`
package. For instance:

    MASTER=spark://host:7077 ./bin/run-example SparkPi

Many of the example programs print usage help if no params are given.

## Running Tests

Testing first requires [building Spark](#building-spark). Once Spark is built, tests
can be run using:

    ./dev/run-tests

Please see the guidance on how to
[run tests for a module, or individual tests](https://cwiki.apache.org/confluence/display/SPARK/Useful+Developer+Tools).

## A Note About Hadoop Versions

Spark uses the Hadoop core library to talk to HDFS and other Hadoop-supported
storage systems. Because the protocols have changed in different versions of
Hadoop, you must build Spark against the same version that your cluster runs.

Please refer to the build documentation at
["Specifying the Hadoop Version"](http://spark.apache.org/docs/latest/building-spark.html#specifying-the-hadoop-version)
for detailed guidance on building for a particular distribution of Hadoop, including
building for particular Hive and Hive Thriftserver distributions.

## Configuration

Please refer to the [Configuration Guide](http://spark.apache.org/docs/latest/configuration.html)
in the online documentation for an overview on how to configure Spark.
