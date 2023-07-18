# Micronaut

## Reflective Access

- add a reflect-config.json so Graal recognizes imported classes that need to be reflective

```bash
touch /src/main/resources/META-INF/native-image/com/ssi/reflect-config.json
```

[MicroStream Source Reference](https://gist.github.com/14paxton/d51cc2f493b8d8f4271c0cf55f2aefab)

> ex.

```json
{
  "name": "fts.marketing.utils.deserializers.CampaignEmailStatusDeserializer",
  "allDeclaredConstructors": true,
  "allPublicConstructors": true,
  "allDeclaredMethods": true,
  "allPublicMethods": true,
  "allDeclaredClasses": true,
  "allPublicClasses": true
}
```

## GraalVM annotation processor

> gradle import:

```groovy
annotationProcessor("io.micronaut:micronaut-graal")
```

***This processor generates additional classes that implement the ***
***[GraalReflectionConfigurer](https://docs.micronaut.io/latest/api/io/micronaut/core/graal/GraalReflectionConfigurer.html) inteface and programmatically register*** ***reflection configuration.***

- For example the following class:

```java 

@ReflectiveAccess
@Serdeable
public class Integration {
      ...
}
```

> > ***If you have more advanced requirements and only wish to include certain fields or methods, use the annotation on any constructor,***
> > ***field or method to include only the specific field, constructor or method.***

# TidBit

## Due to a bug with GraalVM and Java Records it is necessary to include the flag

```
--report-unsupported-elements-at-runtime when building the native executable. Create the file native-image.properties:
```

at
> src/main/resources/META-INF/native-image/example.micronaut/guide/native-image.properties

```bash
Args = --report-unsupported-elements-at-runtime
```

# Gradle

> The Gradle plugin has a new testNativeImage task that builds the GraalVM Native Image and uses the native application as an embedded
> server enabling the ability to write native integration tests.

## add tool chain to gradle

You can already build a native executable by running ./gradlew nativeCompile or run it directly by invoking ./gradlew nativeRun. However, at this stage, running the native executable will fail because
this application requires additional metadata: you need to provide it with a list of resources to load.

Instruct the plugin to automatically detect resources to be included in the native executable. Add this to your build.gradle file:

```groovy
graalvmNative {
    binaries.all {
        resources.autodetect()
    }
    toolchainDetection = false
}
```

Another thing to note here, the plugin may not be able to properly detect the GraalVM installation, because of limitations in Gradle. By default, the plugin selects a Java 11 GraalVM Community
Edition. If you want to use GraalVM Enterprise, or a particular version of GraalVM and Java, you need to explicitly tell in plugin’s configuration. For example:

```groovy
graalvmNative {
    binaries {
        main(({
            javaLauncher = javaToolchains.launcherFor {
                languageVersion = JavaLanguageVersion.of(8)
                vendor = JvmVendorSpec.matching("GraalVM Community")
            }
        } as java.lang.String))
    }
}
```

> my working example

```groovy
graalvmNative {
    toolchainDetection = false

    binaries {
        main(({
            javaLauncher = javaToolchains.launcherFor {
                languageVersion = JavaLanguageVersion.of(17)
                vendor = JvmVendorSpec.matching("GraalVM Community")
            }
            imageName.set('graal-vm-ssi')
            buildArgs.add('--verbose')
        } as java.lang.String))
    }
}
```

The workaround to this is to disable toolchain detection with this command
```toolchainDetection = false```.

### get java toolchains

```shell
./gradlew-q javaToolchains
```

> output
> ...

+ Oracle JDK 11.0.18+9-LTS-jvmci-22.3-b11
  | Location:           /Library/Java/JavaVirtualMachines/graalvm-ee-java11-22.3.1/Contents/Home
  | Language Version:   11
  | Vendor:             Oracle
  | Architecture:       x86_64
  | Is JDK:             true
  | Detected by:        Current JVM
  ...

# Plugins

- [Java Assist](https://mvnrepository.com/artifact/org.javassist/javassist)
- [GraalVM Hibernate](https://mvnrepository.com/artifact/org.hibernate/hibernate-graalvm/6.1.5.Final)

# Resources

- [Gradle Plugin](https://micronaut-projects.github.io/micronaut-gradle-plugin/latest/#_micronaut_graalvm_plugin)
- [Micronaut Docs: GraalVM ](https://docs.micronaut.io/latest/guide/index.html#graal)
- [Gradle plugin for GraalVM Native Image building : Config Doc](https://graalvm.github.io/native-build-tools/0.9.13/gradle-plugin.html#configuration-options)
- [Gradle Plugin for Micronaut : io.micronaut.graalvm](https://plugins.gradle.org/plugin/io.micronaut.graalvm)
- [GraalVM Docs : Reflection](https://www.graalvm.org/22.2/reference-manual/native-image/metadata/)
- [reflect-config.json Graal SourceCode](https://github.com/oracle/graal/blob/master/docs/reference-manual/native-image/Reflection.md)
- [Micronaut graalvm Tests Source Code](https://github.com/micronaut-graal-tests/micronaut-liquibase-graal/tree/2.3.x_h2)

