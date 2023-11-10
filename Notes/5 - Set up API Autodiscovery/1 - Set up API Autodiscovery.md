# How to set up API Autodiscovery in Anypoint Studio

API Autodiscovery is a feature in Anypoint Studio that allows you to automatically configure your API to be managed by Anypoint Platform. With API Autodiscovery, you can register your API with the API Manager and apply policies to it without writing any code. To use API Autodiscovery, you need to add the API Autodiscovery element to your Mule flow and specify the API name and version. You also need to have an Anypoint Platform account and a valid client ID and client secret for your API.

## Create a new API in API Manager

1. Go to `Anypoint Platform` > `API Manager`.

<div align="center">
    <img src="../../Captures/Set Api Cap/1-muleApi.png"/>
</div>

2. Click on `Add API` > `Add new API`.

<div align="center">
    <img src="../../Captures/Set Api Cap/2-muleApi.png"/>
</div>

3. Select `Mule Gateway` and click `Next`.

<div align="center">
    <img src="../../Captures/Set Api Cap/3-muleApi.png"/>
</div>

4. Name it as `hellomuleapi`, select `HTTP API`, and click `Next`.

<div align="center">
    <img src="../../Captures/Set Api Cap/4-muleApi.png"/>
</div>

5. Continue with the final options until you see this screen.

    <img src="../../Captures/Set Api Cap/5-muleApi.png"/>

    You can notice the `API instance ID`; save it as we will use it.

## Create a new api.id property per environment

1. Open the properties files and add the new property.

    <img src="../../Captures/Set Api Cap/6-muleApi.png"/>

    Save it.

## Configure Anypoint Studio with API Autodiscovery

1. Go to `global.xml` > `Global Elements` > `Create`. Type `Api Autodiscovery`, select it and click `Ok`. Type the next values:

    ```
    API Id: ${api.id}
    Flow Name: hellomuleFlow
    ```

    <img src="../../Captures/Set Api Cap/7-muleApi.png"/>

    press `Ok`.

## Test your application on your local computer

1. Return to your `Anypoint Platform` and go to `Acces Managment`.

<div align="center">
    <img src="../../Captures/Set Api Cap/8-muleApi.png"/>
</div>

2. Now select `Business Groups` and click on the name of the business.

<div align="center">
    <img src="../../Captures/Set Api Cap/9-muleApi.png"/>
</div>

3. Click on `Environments` > `Sandbox`, and copy the `Client ID` and the `Client Secret` somewhere.

<div align="center">
    <img src="../../Captures/Set Api Cap/10-muleApi.png"/>
    <figcaption>In my case, I took the IDs from the principal settings.</figcaption>
</div>

4. Now open the `Preferences` menu in `Anypoint Studio`. In my case, I have to search for it using the `Help` option and select `Anypoint Studio` > `API Manager`.

<div align="center">
    <img src="../../Captures/Set Api Cap/11-muleApi.png"/>
</div>

5. Input your `Client ID` and the `Client Secret`. Click `Validate`, and you'll see a check icon. Finally, click on `Apply` > `Apply and close` and save it.

<div align="center">
    <img src="../../Captures/Set Api Cap/12-muleApi.png"/>
</div>

6. Run the application and go to your `API tester` to check if everything is right.

## Deploy to CloudHub with your environment credentials

1. Open the `mule-artifact.json` file and add the new properties.

    ```
    {
        "minMuleVersion": "4.3.0",
        "secureProperties": [
            "secure.key",
            "anypoint.platform.client_id",
            "anypoint.platform.client_secret"
        ]
    }
    ```

    Save it and deploy the application.

2. Before you deploy the application, check if the `Client ID` and the `Client Secret` are correct.

    <img src="../../Captures/Set Api Cap/13-muleApi.png"/>

    If they are, proceed to deploy normally and test with your `API tester`.
