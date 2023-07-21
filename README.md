# README

Sample project that has a broken build in a docker container

## Reproduction steps

1. Create docker container
    ```shell
    docker run --entrypoint /bin/sh -it  -v $PWD/src:/demo/src:ro \
      -v $PWD/gradle:/demo/gradle:ro \
      -v $PWD/build.gradle.kts:/demo/build.gradle.kts:ro \
      -v $PWD/gradlew:/demo/gradlew \
      -v $PWD/gradle.properties:/demo/gradle.properties \
      -v $PWD/settings.gradle.kts:/demo/settings.gradle.kts \
      --name demo-container --pull missing openjdk:17-alpine
      ```
1. Run buildPlugin task
    ```shell
    cd /demo; ./gradlew buildPlugin
    ```

**Expected result**
Build successful

**Actual result**
Failed with:
```
Execution failed for task ':buildSearchableOptions'.
> Error while evaluating property 'javaLauncher' of task ':buildSearchableOptions'.
   > Failed to calculate the value of task ':buildSearchableOptions' property 'javaLauncher'.
      > Toolchain installation '/root/.gradle/caches/modules-2/files-2.1/com.jetbrains/jbre/jbr_jcef-17.0.6-linux-x64-b469.82/extracted/jbr_jcef-17.0.6-x64-b469' could not be probed: A problem occurred starting process 'command '/root/.gradle/caches/modules-2/files-2.1/com.jetbrains/jbre/jbr_jcef-17.0.6-linux-x64-b469.82/extracted/jbr_jcef-17.0.6-x64-b469/bin/java''
```