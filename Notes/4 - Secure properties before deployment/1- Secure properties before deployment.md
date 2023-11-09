# Secure properties before deployment

Securing properties before deployment in Anypoint Studio is important for several reasons. First, it prevents unauthorized access to sensitive data such as passwords, tokens, or keys. Second, it allows you to manage different configurations for different environments without modifying the code. Third, it enables you to encrypt and decrypt properties using a secure key stored in a separate file. By securing properties before deployment, you can ensure the security and reliability of your applications in Anypoint Studio.

## Create your environments’ secure properties files

1. Right-click on `src/main/resources` > `New` > `File`. Name it `local.secure.properties` and click on `Finish`. Repeat the process with the name `dev.secure.properties`.

2. In both files, we are going to type the following properties.

    - local.secure:

    ```
    example.username=MyUsernameLocal
    example.password=MyPasswordLocal
    ```

    - dev.secure:

    ```
    example.username=MyUsernameDev
    example.password=MyPasswordDev
    ```

    Finally, save the files.

3. Return to `hellomule` > `Message Flow` and in the `Mule Palette`, select the option `Search in Exchange`. It will open a new window.

<div align="center">
    <img src="../../Captures/Secure Props Cap/1-muleSecure.png"/>
</div>

4. Search and select the option with the name `mule secure configuration properties`, click on `Add`, and then click `Finish`.

5. Now we need to go to `global.xml` > `Global Elements` > `Create`. Search for `Secure Properties Config`, select it, and press `Ok`.

6. In the new window, we need to add a `file` and a `key`, so let's type the following:

<div align="center">
    <img src="../../Captures/Secure Props Cap/2-muleSecure.png"/>
</div>

7. Save the changes

## Set up a logger to read your secure credentials

1. Return to `hellomule` > `Message Flow`. Drag and drop the `Logger (core)` next to the `Set Payload`.

<div align="center">
    <img src="../../Captures/Secure Props Cap/3-muleSecure.png"/>
</div>

2. Now, a new menu will appear at the bottom side.

    <img src="../../Captures/Secure Props Cap/4-muleSecure.png">

    Click on the function button, and after that, a new button will appear on the left side (the dots and lines icon). Press it.

3. Now, you can code in that part using the `DataWeave` language.

4. Type the following code:

    ```dataweave
    output application/java
    ---
    "Username: " ++ Mule::p("secure::example.username")
    ++ " - " ++
    "Password: " ++ Mule::p("secure::example.password")
    ```

    <img src="../../Captures/Secure Props Cap/5-muleSecure.png">

    Finally, click on `Done` to save the code.

    - **Explanation code**: The DataWeave code retrieves and concatenates the values of the secure properties `example.username` and `example.password`. These values are retrieved securely using the `Mule::p` function, ensuring sensitive information remains protected.

## Encrypt your properties files’ values

1. Go to the next <a href="https://docs.mulesoft.com/mule-runtime/latest/secure-configuration-properties#secure_props_tool">Link</a> and download the `Secure Properties Tool Jar file` and we neet to execute it into our porject so open the console in the file where you save the `jar` and use the next comand (Windows Powershell):

    ```
    java -cp secure-properties-tool.jar com.mulesoft.tools.SecurePropertiesTool string encrypt Blowfish CBC MyMuleSoftKey "myUsernameLocal"
    ```

    and we obtain something like this:

    ```
    HbsuWJRjiubchmzQREGdsA==
    ```

2. Copy the result and paste in the `local.secure.properties` like this:

    <img src="../../Captures/Secure Props Cap/6-muleSecure.png"/>

    Do the same thing with the other properties in `local.secure.properties`, `dev.secure.properties` and save the changes.

## Test your application on your local computer

1. Right-click on `root` file > `Run As` > `Run Configurations` > `Environment` > `Add`.

    ```
    Name: secure.key
    Value: MyMuleSoftKey
    ```

    Press `Ok` > `Apply` > `Run`.

<div align="center">
    <img src="../../Captures/Secure Props Cap/7-muleSecure.png"/>
</div>

2. Now go to your API tester and try the `GET` method again. Check the console, and you should see the username and password.

<div align="center">
    <img src="../../Captures/Secure Props Cap/8-muleSecure.png"/>
</div>

## Deploy to CloudHub with your secure credentials

1. Stop the application and go to `Deploy to CloudHub`.

2. A new checkbox will appear, `Overwrite Existing Application`. Leave it checked.

3. Click on the `Properties` tab and add the values:

    ```
    key: env
    value: dev
    ```

    ```
    key: secure.key
    value: MyMuleSoftKey
    ```

    Finally, `Deploy` the application.

4. If we go to our `Runtime Manager` > `Settings` > `Properties`.

    <img src="../../Captures/Secure Props Cap/9-muleSecure.png"/>

    we can notice the properties are visible. So, if we want to hide them, we need to return to our project and make some changes.

5. Open the file `mule-artifact.json` and add the following code:

    ```
    {
        "minMuleVersion": "4.5.0",
        "secureProperties": ["secure.key"]
    }
    ```

    Save it and deploy again. If you check the `Runtime Manager` again, now the properties are hidden.

<div align="center">
    <img src="../../Captures/Secure Props Cap/10-muleSecure.png"/>
</div>
