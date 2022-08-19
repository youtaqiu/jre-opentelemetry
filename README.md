## JRE17 Dockerfile for OpenTelemetry

* #### [opentelemetry-java-instrumentation](https://github.com/open-telemetry/opentelemetry-java-instrumentation)
* #### [zulu-openjdk](https://hub.docker.com/r/azul/zulu-openjdk)
* #### [jib](https://github.com/GoogleContainerTools/jib)

### Getting Started

* ##### Build Docker Image

```shell
docker build -t youtaqiu/jre-trace:17 .
```

* ##### Usage(Example for JIB)

```groovy
jib {
//    allowInsecureRegistries = true
    from {
        image = "youtaqiu/jre-trace:17"
    }
    to {
        image = "youtaqiu/java-demo:1.0"
        auth {
            username System.getenv("dockerUsername") ?: dockerUsername
            password System.getenv("dockerPassword") ?: dockerPassword
        }
        tags = ["1.0", "latest"]

    }
    container {
        creationTime = 'USE_CURRENT_TIMESTAMP'
        jvmFlags = ['-Djava.security.egd=file:/dev/./urandom', '-Dfile.encoding=utf-8', '-Duser.timezone=GMT+08', '--add-opens=java.base/java.lang.reflect=ALL-UNNAMED', '-Xshare:off', '-javaagent:/opentelemetry.jar']
    }
}
```
