# Gradle Micronaut
## CLI
### Debug
```bash
./gradlew runSingle --debug-jvm -PmainClass=Mai
```
----

## build.gradle
```groovy
test {
    debugOptions {
        enabled = true
        port = 4455
        server = true
        suspend = true
    }
}
```

> or ```run{ ... }```


### Remote Debugging in Gradle

```groovy
tasks.withType(JavaExec) {
    if (System.getProperty('DEBUG', 'false') == 'true') {
        jvmArgs '-Xdebug', '-Xrunjdwp:transport=debug_socket,server=y,suspend=y,address=9099'
    }
}
```

To know what's happening with the arguments read this about the arguments that you need to send to jvm to make remote debugging possible:
```
https://www.eclipse.org/jetty/documentation/9.3.x/enable-remote-debugging.html
```

#### Running instructions

##### Step1:

```bash
gradle -DDEBUG=true run
```

- Now in console you will see something like this:
```bash
Listening for transport debug_socket at address: 9099
```

##### Step2:
configuration>Remote java application
set these fields:

	1. project
	2. host (here its localhost)
	3. port (in this example it will be 9099)


