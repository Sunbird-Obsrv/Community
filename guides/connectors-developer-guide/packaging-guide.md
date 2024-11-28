# Packaging Guide

## Bundling Streaming Connectors

### Java / Scala

{% hint style="info" %}
The below document outlines the structure if you are using `mvn` as your build tool. If you are using `sbt` or others, use the following as reference and update accordingly to generate the package structure.
{% endhint %}

The stream connectors are expected to be bundled as a Single JAR (Fat JAR). We recommend using some thing like `maven-shade-plugin` to build the final JAR file.

Additionally, we recommend using `maven-assembly-plugin` to bundle all required files and JAR into a single distribution.

Here is a sample using `maven-shade-plugin` and `maven-assembly-plugin`

{% code title="pom.xml" %}
```xml
<build>
    ...
    <plugins>
        ...
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>3.2.1</version>
            <executions>
                <execution>
                    <phase>package</phase>
                    <goals>
                        <goal>shade</goal>
                    </goals>
                    <configuration>
                        <shadedArtifactAttached>false</shadedArtifactAttached>
                        <artifactSet>
                            <excludes>
                                <exclude>com.google.code.findbugs:jsr305</exclude>
                            </excludes>
                        </artifactSet>
                        <filters>
                            <filter>
                                <!-- Do not copy the signatures in the META-INF folder.
                                Otherwise, this might cause SecurityExceptions when using the JAR. -->
                                <artifact>*:*</artifact>
                                <excludes>
                                    <exclude>META-INF/*.SF</exclude>
                                    <exclude>META-INF/*.DSA</exclude>
                                    <exclude>META-INF/*.RSA</exclude>
                                </excludes>
                            </filter>
                        </filters>
                        <transformers>
                            <transformer
                                    implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                                <mainClass>org.sunbird.obsrv.connector.ExampleSourceConnector</mainClass>
                            </transformer>
                            <!-- append default configs -->
                            <transformer
                                    implementation="org.apache.maven.plugins.shade.resource.AppendingTransformer">
                                <resource>reference.conf</resource>
                            </transformer>
                        </transformers>
                    </configuration>
                </execution>
            </executions>
        </plugin>
        <plugin>
            <artifactId>maven-assembly-plugin</artifactId>
            <executions>
                <execution>
                    <id>distro-assembly</id>
                    <phase>package</phase>
                    <goals>
                        <goal>single</goal>
                    </goals>
                    <configuration>
                        <descriptors>
                            <descriptor>src/main/assembly/src.xml</descriptor>
                        </descriptors>
                    </configuration>
                </execution>
            </executions>
        </plugin>
        ...
    </plugins>
</build>
```
{% endcode %}

And here is a sample of `src/main/assembly/src.xml` for building the distribution

{% code title="src.xml" %}
```xml
<?xml version="1.0" encoding="UTF-8"?>

<assembly xmlns="http://maven.apache.org/ASSEMBLY/2.2.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://maven.apache.org/ASSEMBLY/2.2.0 https://maven.apache.org/xsd/assembly-2.2.0.xsd">
    <id>distribution</id>
    <formats>
        <format>tar.gz</format>
    </formats>
    <fileSets>
        <fileSet>
            <directory>${basedir}/src/main/resources</directory>
            <outputDirectory>/</outputDirectory>
            <includes>
                <include>*</include>
            </includes>
            <excludes>
                <exclude>obsrv-connector-config.conf</exclude>
            </excludes>
        </fileSet>
        <fileSet>
            <directory>target</directory>
            <outputDirectory>/</outputDirectory>
            <includes>
                <include>*.jar</include>
            </includes>
        </fileSet>
    </fileSets>
</assembly>
```
{% endcode %}

Run `mvn clean package` to generate the distribution

The contents of the distribution should be in the following format

```
example-connector-0.1.0-distribution.tar.gz
├── example_connector.jar
├── alerts.yaml
├── metadata.json
├── metrics.yaml
├── ui-config.json
└── icon.svg
```

## Bundling Batch Connectors

### Java / Scala

The batch connectors are bundled as a standalone JAR file, where the dependent JARs are to be included in the `libs` folder in the bundle, by using the `maven-assembly-plugin.`

&#x20;Here is a sample of including the `maven-assembly-plugin` to your build

{% code title="pom.xml" %}
```xml
<build>
    ...
    <plugins>
        ...
        <plugin>
            <artifactId>maven-assembly-plugin</artifactId>
            <executions>
                <execution>
                    <id>distro-assembly</id>
                    <phase>package</phase>
                    <goals>
                        <goal>single</goal>
                    </goals>
                    <configuration>
                        <descriptors>
                            <descriptor>src/main/assembly/src.xml</descriptor>
                        </descriptors>
                    </configuration>
                </execution>
            </executions>
        </plugin>
        ...
    </plugins>
</build>
```
{% endcode %}

And here is a sample of `src/main/assembly/src.xml` for building the distribution

{% code title="src.xml" %}
```xml
<?xml version="1.0" encoding="UTF-8"?>

<assembly xmlns="http://maven.apache.org/ASSEMBLY/2.2.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://maven.apache.org/ASSEMBLY/2.2.0 https://maven.apache.org/xsd/assembly-2.2.0.xsd">
    <id>distribution</id>
    <formats>
        <format>tar.gz</format>
    </formats>
    <fileSets>
        <fileSet>
            <directory>${basedir}/src/main/resources</directory>
            <outputDirectory>/</outputDirectory>
            <includes>
                <include>*</include>
            </includes>
            <excludes>
                <exclude>obsrv-connector-config.conf</exclude>
            </excludes>
        </fileSet>
        <fileSet>
            <directory>target</directory>
            <outputDirectory>/</outputDirectory>
            <includes>
                <include>*.jar</include>
            </includes>
        </fileSet>
    </fileSets>
    <dependencySets>
        <dependencySet>
            <outputDirectory>libs</outputDirectory>
            <useTransitiveFiltering>true</useTransitiveFiltering>
        </dependencySet>
    </dependencySets>
</assembly>
```
{% endcode %}

Run `mvn clean package` to generate the distribution

The contents of the distribution should be in the following format

```
example-connector-0.1.0-distribution.tar.gz
├── libs
    └── sample-dependency.jar
├── example_connector.jar
├── alerts.yaml
├── metadata.json
├── metrics.yaml
├── requirements.txt
├── ui-config.json
└── icon.svg
```

### Python

Since we use PySpark for building the batch connectors in Python, we are required to include the dependent JARs as a part of the distribution.

Here are the steps if you are using `poetry` as a package manager for Python Connectors.

Add a `build_dist.py` script to the `scripts` folder with the following contents. Briefly the script does the following

* It exports the python requirements to `requirements.txt` file, so that these can be installed on the runtime.
* It downloads all the dependent JARs that are to be included in the package using `mvn`

{% code title="scripts/build_dist.py" %}
```python
import subprocess
import os

def main():
    # remove dirs recursively
    subprocess.Popen("rm -rf dist", shell=True).wait()

    # Path to the directory containing the JAR files
    jar_dir = os.path.join(os.path.dirname(__file__), '..', 'libs')
    os.makedirs(jar_dir, exist_ok=True)

    subprocess.Popen("""poetry export --without-hashes --format=requirements.txt | awk '{split($0,a,"; "); print a[1]}' > requirements.txt""", shell=True).wait()
    # TODO: Only uncomment the below line, if you have Java dependencies for your script, which have to be included in the libs folder
    # subprocess.Popen("mvn dependency:copy-dependencies -DrepoUrl=http://repo1.maven.org/maven2/ -DexcludeTrans -DoutputDirectory=libs", shell=True).wait()
    subprocess.Popen("poetry build -f sdist", shell=True).wait()
    subprocess.Popen("rm -rf requirements.txt libs", shell=True).wait()

if __name__ == '__main__':
    main()
```
{% endcode %}

The packaging instructions have to be included in the `pyproject.toml` file.&#x20;

```toml
packages = [
    { include = "example_connector", from = ".", format = "sdist" },
]

include = [
    "requirements.txt",
    # "libs/*.jar", # TODO: Only uncomment the below line, if you have Java dependencies for your script, which have to be included in the libs folder
    "ui-config.json",
    "metadata.json",
    "alerts.yaml",
    "metrics.yaml",
    "icon.svg" # Add additional files like the icons that are to be included in the bundle
]

[build-system]
requires = ["poetry-core"]
build-backend = "poetry.core.masonry.api"

[tool.poetry.scripts]
package = "scripts.build_dist:main"
```

Add a `pom.xml` file to the root and specify the dependent JARs required by the connector

{% code title="pom.xml" %}
```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>in.sanketika.connectors</groupId>
    <artifactId>example-connector</artifactId>
    <version>1.0.0</version>
    <dependencies>
        <dependency>
            <groupId> </groupId>
            <artifactId> </artifactId>
            <version> </version>
        </dependency>
        ...
    </dependencies>
</project>
```
{% endcode %}

Run `poetry run package` to build the distribution that can be installed on Obsrv.

The contents of the distribution should be in the following format

```
example-connector-0.1.0-distribution.tar.gz
├── libs
    └── sample-dependency.jar
├── example_connector
    └── main.py
├── alerts.yaml
├── metadata.json
├── metrics.yaml
├── requirements.txt
├── ui-config.json
└── icon.svg
```
