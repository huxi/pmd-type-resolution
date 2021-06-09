# Description

This is a minimal example for [PMD issue 3330](https://github.com/pmd/pmd/issues/3330).


When executing `./gradlew`, PMD will output the following:

```
> Task :project2:pmdMain
Error during type resolution of field 'BZIP' in class project1.Compression due to: java.lang.NoClassDefFoundError: org/apache/commons/compress/compressors/bzip2/BZip2CompressorOutputStream

BUILD SUCCESSFUL in 5s
8 actionable tasks: 8 executed
```

When executing `./gradlew :project2:dependencies`, Gradle prints the following:
```
> Task :project2:dependencies

------------------------------------------------------------
Project ':project2'
------------------------------------------------------------

annotationProcessor - Annotation processors and their dependencies for source set 'main'.
No dependencies

api - API dependencies for source set 'main'. (n)
No dependencies

apiElements - API elements for main. (n)
No dependencies

archives - Configuration for archive artifacts. (n)
No dependencies

compileClasspath - Compile classpath for source set 'main'.
\--- project :project1

compileOnly - Compile only dependencies for source set 'main'. (n)
No dependencies

compileOnlyApi - Compile only API dependencies for source set 'main'. (n)
No dependencies

default - Configuration for default artifacts. (n)
No dependencies

implementation - Implementation only dependencies for source set 'main'. (n)
\--- project project1 (n)

pmd - The PMD libraries to be used for this project.
\--- net.sourceforge.pmd:pmd-java:6.35.0
     +--- net.sourceforge.pmd:pmd-core:6.35.0
     |    +--- org.antlr:antlr4-runtime:4.7.2
     |    +--- com.beust:jcommander:1.48
     |    +--- commons-io:commons-io:2.6
     |    +--- net.sourceforge.saxon:saxon:9.1.0.8
     |    +--- org.apache.commons:commons-lang3:3.8.1
     |    +--- org.ow2.asm:asm:9.1
     |    \--- com.google.code.gson:gson:2.8.5
     +--- net.sourceforge.saxon:saxon:9.1.0.8
     +--- org.ow2.asm:asm:9.1
     +--- commons-io:commons-io:2.6
     \--- org.apache.commons:commons-lang3:3.8.1

runtimeClasspath - Runtime classpath of source set 'main'.
\--- project :project1
     \--- org.apache.commons:commons-compress:1.20

runtimeElements - Elements of runtime for main. (n)
No dependencies

runtimeOnly - Runtime only dependencies for source set 'main'. (n)
No dependencies

testAnnotationProcessor - Annotation processors and their dependencies for source set 'test'.
No dependencies

testCompileClasspath - Compile classpath for source set 'test'.
\--- project :project1

testCompileOnly - Compile only dependencies for source set 'test'. (n)
No dependencies

testImplementation - Implementation only dependencies for source set 'test'. (n)
No dependencies

testRuntimeClasspath - Runtime classpath of source set 'test'.
\--- project :project1
     \--- org.apache.commons:commons-compress:1.20

testRuntimeOnly - Runtime only dependencies for source set 'test'. (n)
No dependencies

(*) - dependencies omitted (listed previously)

(n) - Not resolved (configuration is not meant to be resolved)

A web-based, searchable dependency report is available by adding the --scan option.

BUILD SUCCESSFUL in 1s
```

The dependency required to resolve the mentioned class `BZip2CompressorOutputStream` is present in `runtimeClasspath`.
