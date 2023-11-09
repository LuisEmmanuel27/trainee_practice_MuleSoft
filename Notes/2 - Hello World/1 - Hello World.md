# WARNING:

**Please check your JDK version because Anypoint Studio is only compatible with JDK 8 and 11.**

# Don't suffer like me (I'm on Windows 11)

1. Check if you have installed `jre-1.8` or `JDK 8`. If you don't have it, please install it.

2. Change the environment variable `JAVA_HOME` to use `jre-1.8`.

3. In the Anypoint Studio file, open `AnypointStudio.ini`, and change the lines:

    ```ini
    # -vm
    # C:\Program Files\Java\bin\javaw.exe
    ```

    to your current `javaw.exe` location, like this:

    ```ini
    -vm
    C:\Program Files\Java\jre-1.8\bin\javaw.exe
    ```

    Save and start Anypoint Studio.

# Tutorials Build your first Hello Mule application

We're going to follow the instructions of the official <a href="https://developer.mulesoft.com/tutorials-and-howtos/getting-started/hello-mule/">documentation of MuleSoft</a>

## Before to start

1. Open `Anypoint Studio` and first check if appears a loading bar on the botton right zone, if it appears wait for the load.

<div align="center">
    <img src="../../Captures/Hello World Cap/1-muleHello.png" />
</div>

2.  If you're starting a new repository on GitHub, you can use this `.gitignore` file to avoid potential issues:

        # Ignore Anypoint Studio metadata folders
        .metadata/
        .mule/

        # Ignore system configuration files
        *.DS_Store
        Thumbs.db

        # Ignore compilation and package files
        *.class
        *.jar
        *.war
        *.ear
        *.logs
        *.zip
        *.tar.gz
        *.rar

        # Ignore target folder generated during project compilation
        target/

        # Ignore IDE configuration files and folders
        .idea/
        *.iml
        *.iws
        *.ipr
        .classpath
        .project
        .settings/
        bin/

        # Ignore log files
        *.log

        # Ignore temporary files
        *.tmp
        *.bak
        *.swp
        *~.nib
        local.properties
        .recommenders

## Creating a new project in Anypoint Studio

1. Select the `Create a Mule Project` option from the _left menu_, provide it with a name, and then press the `Finish` button.

<div align="center">
    <img src="../../Captures/Hello World Cap/2-muleHello.png" />
</div>

2. After building the project, you'll see something like this:

<div align="center">
    <img src="../../Captures/Hello World Cap/3-muleHello.png" />
    <figcaption><i>Image from the official documentation</i></figcaption>
</div>

<div align="center">
    <table>
    <thead>
        <tr>
        <th>Color</th>
        <th>Area Name</th>
        <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
        <td>Red</td>
        <td>Package Explorer</td>
        <td>This is where you can view your project structure (files and folders).</td>
        </tr>
        <tr>
        <td>Blue/Purple</td>
        <td>Properties Editor and Console</td>
        <td>This is where you can configure attributes of connectors and see the logs to catch any errors in your application.</td>
        </tr>
        <tr>
        <td>Pink</td>
        <td>Mule Palette</td>
        <td>The Mule Palette allows you to select from hundreds of prebuilt Anypoint Connectors from Exchange or the Core Connector components to build your application.</td>
        </tr>
        <tr>
        <td>Green</td>
        <td>Canvas</td>
        <td>This is where you can drag and drop Modules located in the Mule Palette to create a message flow.</td>
        </tr>
    </tbody>
    </table>
</div>

## Add and configure the HTTP Listener connector

1. Drag and drop the `Listener (HTTP)` option from the `Mule Palette` onto the `canvas screen`. Don't worry if an error appears, it's normal for the moment.

<div align="center">
    <img src="../../Captures/Hello World Cap/4-muleHello.png" />
</div>

2. On the bottom menu, in the `Listener` section, you'll find the `Connector configuration` option and a `plus` button. Click on that, and simply press `OK`.

<div align="center">
    <img src="../../Captures/Hello World Cap/5-muleHello.png" />
</div>

3. On the `path` option, simply type `/hellomule`.

4. Drag and drop the `Set Payload (Core)` from the `Mule Palette` onto the `Canvas screen`, just to the _right_ of the `Listener`.

<div align="center">
    <img src="../../Captures/Hello World Cap/6-muleHello.png" />
</div>

5. In the `Set Payload` section on the bottom menu, click on the `Function` button and type `Hello Mule`.

<div align="center">
    <img src="../../Captures/Hello World Cap/7-muleHello.png" />
</div>

6. Right-click on the `Canvas` screen and run the program.

<div align="center">
    <img src="../../Captures/Hello World Cap/8-muleHello.png" />
</div>

7. If everything is correct, you'll see something like this in the `console`.

<div align="center">
    <img src="../../Captures/Hello World Cap/9-muleHello.png" />
</div>

8. Now, in an API tester like `Postman` or `Insomnia`, we'll test our URL `0.0.0.0:8081/hellomule` or `localhost:8081/hellomule`. I'll use `Thunder Client` in `VSCode` and try a `GET` method.

<div align="center">
    <img src="../../Captures/Hello World Cap/10-muleHello.png" />
</div>

9. Stop the program by right-clicking on the `Canvas` screen and selecting `Stop project` or simply clicking on the red button.

<div align="center">
    <img src="../../Captures/Hello World Cap/11-muleHello.png" />
</div>

## Deploy the Mule Application to CloudHub

1. Right-click on the `main project file` > `Anypoint Platform` > `Deploy to CloudHub`.

2. This will open a sign-in window, so log in and continue.

3. Select the `SANDBOX` option, and you'll see something like this.

<div align="center">
    <img src="../../Captures/Hello World Cap/12-muleHello.png" />
</div>

4. Change the option in `Deployment Target` to `CloudHub` and modify the name as follows.

<div align="center">
    <img src="../../Captures/Hello World Cap/13-muleHello.png" />
</div>

5. Click on `Deploy Application` and wait.

6. The window will change, and you'll see a message along with a button indicating you can close the window. Click the button to close it.

7. Navigate to the Anypoint Platform page and select the `Runtime Manager` section.

<div align="center">
    <img src="../../Captures/Hello World Cap/14-muleHello.png" />
</div>

8. You will see the application listed, and you can click on it.

<div align="center">
    <img src="../../Captures/Hello World Cap/15-muleHello.png" />
</div>

9. Go to `Settings` and copy the `App URL`.

<div align="center">
    <img src="../../Captures/Hello World Cap/16-muleHello.png" />
</div>

10. Test the URL with your API tester, like this `http://hellomule-test-1.us-e2.cloudhub.io/hellomule`, and you'll see it works!
