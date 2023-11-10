# How to deploy from Anypoint Studio using Maven

The MuleSoft Maven plugin integrates the packaging and deployment of your mule application. When the maven commands are executed, your Anypoint Studio project is packaged into a deployable jar file which can then be deployed to any running mule runtime engine either in Cloudhub or OnPrem. For this tutorial, we will be covering how to set up your pom.xml and settings.xml file to deploy your first application on CloudHub using Maven.

## Step 1: How to configure Maven on your computer (Windows 11, Windows Powershell)

1.  Check if Maven is installed by running the following command `mvn --version`:

        PS C:\Users\luisz\OneDrive\Documentos\GitHub\trainee_practice_MuleSoft> mvn --version
        mvn : El término 'mvn' no se reconoce como nombre de un cmdlet, función, archivo de script o programa ejecutable.
        Compruebe si escribió correctamente el nombre o, si incluyó una ruta de acceso, compruebe que dicha ruta es
        correcta e inténtelo de nuevo.
        En línea: 1 Carácter: 1
        + mvn --version
        + ~~~
            + CategoryInfo          : ObjectNotFound: (mvn:String) [], CommandNotFoundException
            + FullyQualifiedErrorId : CommandNotFoundException

    If you get an error like the one you shared, it means Maven is not installed.

2.  You can download Maven from `maven` from <a href="https://maven.apache.org/download.cgi">this link</a> as a zip file:.

<img src="../../Captures/Deploy Maven Cap/1-muleMe.png" />

3.  After downloading and unzipping the file, copy the path to the `bin` directory of Maven.

4.  Add the Maven bin directory to your system's PATH environment variable. You can do this by:

    -   Right-clicking on "This PC" or "My Computer" and selecting "Properties."
    -   Clicking on "Advanced system settings."
    -   Clicking on "Environment Variables..."
    -   In the "System Variables" section, find the "Path" variable and click "Edit..."
    -   Clicking "New" and adding the path to the bin directory of Maven.
    -   Click "OK" to close all the dialogs.

5.  Open a new terminal or command prompt and run the mvn --version command again. You should see the Maven version information displayed without any errors:

        Apache Maven 3.9.5 (57804ffe001d7215b5e7bcb531cf83df38f93546)
        Maven home: C:\Program Files\Java\apache-maven-3.9.5
        Java version: 1.8.0_371, vendor: Oracle Corporation, runtime: C:\Program Files\Java\jre-1.8
        Default locale: es_MX, platform encoding: Cp1252
        OS name: "windows 11", version: "10.0", arch: "amd64", family: "windows"

6.  Search your file system for the `.m2` directory and the `settings.xml` file. These files are typically located in your user's home directory or profile folder. You may need to enable the display of hidden files and folders to find them.

    If you're using Windows, you can usually find them in a path like `C:\Users\<YourUsername>\.m2`. On macOS, the path may be `/Users/<YourUsername>/.m2`. On Linux, look in `/home/<YourUsername>/.m2`.

    The `settings.xml` file contains configuration settings for Maven, including repository definitions and other user-specific configuration.

<div align="center">
    <img src="../../Captures/Deploy Maven Cap/2-muleMe.png" />
</div>

## Creating an App on Anypoint Platform

1. First, we need to go to our Anypoint Platform and navigate to `Access Management`.

<div align="center">
    <img src="../../Captures/Deploy Maven Cap/3-muleMe.png" />
</div>

2. Now, we need to create an App. Click on `Create app`.

<div align="center">
    <img src="../../Captures/Deploy Maven Cap/4-muleMe.png" />
</div>

3. We need to configure the app, so give it a name, select the second type option, and the necessary `Scopes` as shown in the following images.

<div align="center">
    <img src="../../Captures/Deploy Maven Cap/5-muleMe.png" />
    <img src="../../Captures/Deploy Maven Cap/6-muleMe.png" />
</div>

4. Now, you can see the app on the screen. Click on `Copy Id` and `Copy Secret`, and make sure to save both IDs for future use.

## Anypoint Studio, pom.xml and settings.xml

1. Create a new project following the steps outlined in <a href="../2 - Hello World/1 - Hello World.md">Hello World</a> notes, but only complete up to step `7`, with a few differences.

<div align="center">
    <img src="../../Captures/Deploy Maven Cap/8-muleMe.png" />
    <img src="../../Captures/Deploy Maven Cap/9-muleMe.png" />
</div>

2. Now, create a new `settings.xml` file in a location of your choice and use the following code:

    ```
    <settings>
        <servers>
            <server>
                <id>my.anypoint.credentials</id>
                <username>~~~Client~~~</username>
                <password>clientId~?~Secret</password>
            </server>
        </servers>
    </settings>
    ```

    Replace `clientId` and `Secret` with the IDs you saved previously.

3. Open the `Preferences` window and navigate to `Maven` > `Global Settings`. Configure it as shown below:

    <img src="../../Captures/Deploy Maven Cap/10-muleMe.png" />

    Finally click on `Apply and close`.

4. Now, we need to modify our `pom.xml`. We must follow the steps outlined in the following <a href="https://docs.mulesoft.com/mule-runtime/4.4/deploy-to-cloudhub-2">documentation</a>.

5. When reviewing the section `Configure the CloudHub 2.0 Deployment Strategy`, we need to copy the following code into our `pom.xml`:

    ```
    <build>
            <plugins>
                <plugin>
                    <groupId>org.mule.tools.maven</groupId>
                    <artifactId>mule-maven-plugin</artifactId>
                    <version>3.7.1</version>
                    <extensions>true</extensions>
                    <configuration>
                        <cloudhub2Deployment>
                            <uri>https://anypoint.mulesoft.com</uri>
                            <provider>MC</provider>
                            <environment>Sandbox</environment>
                            <target>CloudHub</target>
                            <muleVersion>4.4.0</muleVersion>
                            <!-- It will be setted on settings.xml -->
                            <!-- <username>${user}</username> -->
                            <!-- <password>${pass}</password> -->
                            <applicationName>maven-tutorial</applicationName>
                            <replicas>1</replicas>
                            <vCores>0.1</vCores>
                        </cloudhub2Deployment>
                    </configuration>
                </plugin>
            </plugins>
    </build>
    ```

6. Another section in the documentation indicates we need this part:

    ```
    <secureProperties>
        <https.port>8082</https.port>
    </secureProperties>
    ```

7. After many configurations, the `pom.xml` file looks like this:

    ```
    <?xml version="1.0" encoding="UTF-8"?>
    <project xmlns="http://maven.apache.org/POM/4.0.0"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
        <modelVersion>4.0.0</modelVersion>

        <groupId>e948195c-b740-4973-9a35-0ff08b534084</groupId>
        <artifactId>maven-tutorial</artifactId>
        <version>1.0.0-SNAPSHOT</version>
        <packaging>mule-application</packaging>

        <name>maven-tutorial</name>

        <properties>
            <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
            <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>

            <app.runtime>4.5.1</app.runtime>
            <mule.maven.plugin.version>3.8.1</mule.maven.plugin.version>
        </properties>

        <build>
            <plugins>
                <plugin>
                    <groupId>org.mule.tools.maven</groupId>
                    <artifactId>mule-maven-plugin</artifactId>
                    <version>4.0.0</version>
                    <extensions>true</extensions>
                    <configuration>
                        <cloudhub2Deployment>
                            <uri>https://anypoint.mulesoft.com</uri>
                            <provider>MC</provider>
                            <environment>Sandbox</environment>
                            <target>CloudHub</target>
                            <muleVersion>4.4.0</muleVersion>
                            <!-- It will be setted on settings.xml -->
                            <!-- <username>${user}</username> -->
                            <!-- <password>${pass}</password> -->
                            <server>my.anypoint.credentials</server>
                            <applicationName>maven-tutorial</applicationName>
                            <replicas>1</replicas>
                            <vCores>0.1</vCores>
                            <properties>
                                <http.port>8081</http.port>
                            </properties>
                            <secureProperties>
                                <https.port>8082</https.port>
                            </secureProperties>
                        </cloudhub2Deployment>
                    </configuration>
                </plugin>
            </plugins>
        </build>

        <distributionManagement>
            <repository>
                <id>my.anypoint.credentials</id>
                <name>Corporate Repository</name>
                <url>https://maven.anypoint.mulesoft.com/api/v3/organizations/${project.groupId}/maven</url>
                <layout>default</layout>
            </repository>
        </distributionManagement>

        <dependencies>
            <dependency>
                <groupId>org.mule.connectors</groupId>
                <artifactId>mule-http-connector</artifactId>
                <version>1.8.0</version>
                <classifier>mule-plugin</classifier>
            </dependency>
            <dependency>
                <groupId>org.mule.connectors</groupId>
                <artifactId>mule-sockets-connector</artifactId>
                <version>1.2.3</version>
                <classifier>mule-plugin</classifier>
            </dependency>
        </dependencies>

        <repositories>
            <repository>
                <id>anypoint-exchange-v3</id>
                <name>Anypoint Exchange</name>
                <url>https://maven.anypoint.mulesoft.com/api/v3/maven</url>
                <layout>default</layout>
            </repository>
            <repository>
                <id>mulesoft-releases</id>
                <name>MuleSoft Releases Repository</name>
                <url>https://repository.mulesoft.org/releases/</url>
                <layout>default</layout>
            </repository>
        </repositories>

        <pluginRepositories>
            <pluginRepository>
                <id>mulesoft-releases</id>
                <name>MuleSoft Releases Repository</name>
                <layout>default</layout>
                <url>https://repository.mulesoft.org/releases/</url>
                <snapshots>
                    <enabled>false</enabled>
                </snapshots>
            </pluginRepository>
        </pluginRepositories>

    </project>
    ```

### **Notes**

-   `<mule.maven.plugin.version>3.8.1</mule.maven.plugin.version>`: The `POM` file has several issues, one of which is due to an incorrect plugin version. To resolve this, follow the instructions provided in this <a href="https://help.mulesoft.com/s/article/Error-The-packaging-for-this-project-did-not-assign-a-file-to-the-build-artifact-while-deploying-an-application-to-Runtime-Fabric-using-Maven">link</a>, so change your actual version for the `3.8.1`.

-   `<groupId>e948195c-b740-4973-9a35-0ff08b534084</groupId>`: The `groupId` was derived from the main URL from `Anypoint Platform`:

<div align="center">
    <img src="../../Captures/Deploy Maven Cap/11-muleMe.png" />
</div>

-   `<server>my.anypoint.credentials</server>` & `<id>my.anypoint.credentials</id>`: These are the same as the `<id>` in the `settings.xml` file.

## Tring to deploy the app

1. Open your terminal and enter the command (for Windows PowerShell):

    ```
    mvn clean deploy -DmuleDeploy
    ```

2. If everything is right, it will work.

## The problem

I've tried a lot of possible solutions, but I'm facing a major issue:

<img src="../../Captures/Deploy Maven Cap/12-muleMe.png" />
<img src="../../Captures/Deploy Maven Cap/13-muleMe.png" />

So the big question is, `How can I fix this problem?`
