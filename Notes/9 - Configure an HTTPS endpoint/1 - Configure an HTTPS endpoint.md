# How to configure an HTTPS endpoint in Anypoint Studio

Create a new `hellomule` project following the steps outlined in <a href="../2 - Hello World/1 - Hello World.md">Hello World</a> notes, but only complete up to step `7`.

<div align="center">
    <img src="../../Captures/Config HTTPS Cap/1-muleHtt.png" />
</div>

## Build an HTTPS Service

1. Right-click on `src/main/resources` > `New` > `File`. Name it `local.properties` and click `Finish`.

2. Add the following content to the file:

    ```
    https.port=8082
    ```

    <img src="../../Captures/Config HTTPS Cap/2-muleHtt.png" />

    and save it.

3. Click on `hellomule-2` > `Global Elements` > `Edit` and change the options as follows:

    <img src="../../Captures/Config HTTPS Cap/3-muleHtt.png" />

    If we press `Test connection`, it may fail, but it's normal, so just click `Ok`.

4. To resolve the problem, click on `Create` > `Global Configurations` > `Configuration Properties`. Search for our file `local.properties` and click `Ok`.

<div align="center">
    <img src="../../Captures/Config HTTPS Cap/4-muleHtt.png" />
</div>

--

5. Now, return to the `Edit` window of the `HTTP_Listener_config`, and click on the `TLS` section. In `TLS configuration`, select `Edit inline`.

<div align="center">
    <img src="../../Captures/Config HTTPS Cap/5-muleHtt.png" />
</div>

6. Before proceeding, cancel the previous step, and in your console, obtain the `keytool` (Windows PowerShell):

    ```
    keytool -genkey -alias key-alias -keystore keystore-name.jks -keyalg RSA -storetype JKS
    ```

    After completing the process, locate the `keystore-name.jks` file, and copy it to the `src/main/resources` directory of `hellomule-2`.

7. Repeat step `5`, and complete the inputs based on the information you used when creating the `keystore`.

    <img src="../../Captures/Config HTTPS Cap/6-muleHtt.png" />

    `Test the connection`, and it should work. Finally, click `Ok`.

8. Save the files, run the application, and test it with your `API tester`, but this time use a `POST` method.
