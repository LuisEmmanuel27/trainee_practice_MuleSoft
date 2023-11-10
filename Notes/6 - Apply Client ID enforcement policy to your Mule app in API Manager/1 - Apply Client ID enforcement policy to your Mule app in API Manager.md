# How to apply Client ID enforcement policy to your Mule app in API Manager

A Client ID enforcement policy is a way to control who can access your Mule app in API Manager. It requires the client to provide a valid Client ID and Client Secret pair that matches the ones you have registered in API Manager. This way, you can prevent unauthorized or malicious requests from reaching your app and consuming your resources. A Client ID enforcement policy also enables you to track and monitor the usage of your app by different clients, and apply rate limiting or throttling policies if needed.

## Set the Client ID enforcement policy in API Manager

1. Go to `Anypoint Platform` > `API Manager` > `Select your API name`.

<div align="center">
    <img src="../../Captures/Apply Client Cap/1-muleCli.png"/>
</div>

2. Click on `Policies` > `+ Add policy`.

<div align="center">
    <img src="../../Captures/Apply Client Cap/2-muleCli.png"/>
</div>

3. Select `Client ID Enforcement` and click `Next`.

<div align="center">
    <img src="../../Captures/Apply Client Cap/3-muleCli.png"/>
</div>

4. Select the next options and click `Apply`:

<div align="center">
    <img src="../../Captures/Apply Client Cap/4-muleCli.png"/>
</div>

5. You'll see the new policy now appears.

<div align="center">
    <img src="../../Captures/Apply Client Cap/5-muleCli.png"/>
</div>

6. Test the application with your `API tester`, and you will notice that we can't access.

<div align="center">
    <img src="../../Captures/Apply Client Cap/6-muleCli.png"/>
</div>

## Generate the Client ID and Client Secret credentials

1. Go to `Anypoint Platform` > `Exchange`.

<div align="center">
    <img src="../../Captures/Apply Client Cap/7-muleCli.png"/>
</div>

2. Click on the square of `Any assets (root)`.

<div align="center">
    <img src="../../Captures/Apply Client Cap/8-muleCli.png"/>
</div>

3. Select `Request access`.

<div align="center">
    <img src="../../Captures/Apply Client Cap/9-muleCli.png"/>
</div>

4. Select the `API Instance`, and in `Application`, click on `Create a new application` and give it a name.

<div align="center">
    <img src="../../Captures/Apply Client Cap/10-muleCli.png"/>
    <img src="../../Captures/Apply Client Cap/11-muleCli.png"/>
</div>

5. Save the IDs because we need them to access with the `API Tester`.

<div align="center">
    <img src="../../Captures/Apply Client Cap/12-muleCli.png"/>
</div>

## Add the credentials to the REST Client application

1. Select the `Auth` > `Basic` options of your `API Tester` and input the IDs. Try the `GET` request again.

<div align="center">
    <img src="../../Captures/Apply Client Cap/13-muleCli.png"/>
</div>
