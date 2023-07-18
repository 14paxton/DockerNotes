# [Environment Settings](https://docs.micronaut.io/latest/guide/#environments)
- Deduced environments
- Environments from the micronaut.environments system property
- Environments from the MICRONAUT_ENVIRONMENTS environment variable

- [Available Env Fields](https://docs.micronaut.io/latest/api/io/micronaut/context/env/Environment.html)

Environments specified explicitly through the application context builder
## Run in Development
> replace application
```java
public class Application {
    public static void main(String[] args) {
           Micronaut.build(args)
                .mainClass(Application.class)
                .defaultEnvironments(Environment.DEVELOPMENT)
                .start();
    }
}

```

> add to build.gradle
```groovy
run {
    systemProperty('micronaut.environments', 'dev')
}
```

> cli

```bash
./gradlew -Dmicronaut.environments=dev run
```

> ide 
<img width="1262" alt="image" src="https://user-images.githubusercontent.com/26972590/212477618-198bc498-6520-44d6-8e20-25b7569e735d.png">
