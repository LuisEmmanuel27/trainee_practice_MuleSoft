# Build your first API Specification with API Designer

Many developers have experience consuming APIs in their daily development work but have never designed a REST API from the ground up. If you have ever wanted to learn how to develop an API, this tutorial will walk you through how easy it is to create your own, fully functional API with MuleSoft’s Anypoint Platform. Even with no API Design experience, this tutorial will teach you how to publish your first API Specification (also known as an API Contract).

The first step in the API development process is to brainstorm how we want our API to operate. Do we want our API to return a 200 valid response on POST requests and return a 405 method not allowed on GET requests? Do we want to design a RESTful API or a SOAP API? Do we want our API to be HTTP, HTTPS or both? What data types do we want to accept in our API request? All of these questions are parameters that we can set while building our API with MuleSoft’s API Designer.

## The problem

Danny works for Northern Trail Outfitters (NTO), a retailer of sports apparel, gear, and nutrition products. NTO has an old customer database that requires special drivers and permissions to access. Danny wants to make this data widely and easily accessible across NTO. To make this possible, Danny decides to build a REST API on top of the database.

<div align="center">
    <img src="../../Captures/Api Specification Cap/1-muleSpec.png" />
    <figcaption><i>Image from the documentation</i></figcaption>
</div>

To start, Danny must first design the API and document it in an API Specification. Next, Danny can build the implementation (logic and connectivity) of the API. MuleSoft’s Anypoint Platform can support Danny’s end to end process, providing both design and implementation tools.

## Create the API Specification

1. Go to `AnyPoint Platform` > `Designer Center`.

<div align="center">
    <img src="../../Captures/Api Specification Cap/2-muleSpec.png" />
</div>

2. Click on `Create +` > `New API Specification`.

<div align="center">
    <img src="../../Captures/Api Specification Cap/3-muleSpec.png" />
</div>

3. Give it a name, select `Guide me through it`, and click `Create API`.

<div align="center">
    <img src="../../Captures/Api Specification Cap/4-muleSpec.png" />
</div>

## Define the specification summary and data types

1. Select and type the following information/options in `API Summary`:

<div align="center">
    <img src="../../Captures/Api Specification Cap/5-muleSpec.png" />
</div>

2. Click on `Data Types +` and give it the name and description from the second image.

<div align="center">
    <img src="../../Captures/Api Specification Cap/6-muleSpec.png" />
    <img src="../../Captures/Api Specification Cap/7-muleSpec.png" />
</div>

3. Click on `Add Property` and add the following properties:

<div align="center">
    <img src="../../Captures/Api Specification Cap/8-muleSpec.png" />
</div>

## Data type 2: Contact

1. Create a new `Data Type`.

<div align="center">
    <img src="../../Captures/Api Specification Cap/9-muleSpec.png" />
</div>

2. Add these new properties:

    <img src="../../Captures/Api Specification Cap/10-muleSpec.png" />

    `deliveryAddress` and `postalAddress` are of `address Type`, not `string Type`, so select that option.

## Define the specification resources

1. Click on `Resources +`.

<div align="center">
    <img src="../../Captures/Api Specification Cap/11-muleSpec.png" />
</div>

2. Provide a `Resource path` and a `Name`.

<div align="center">
    <img src="../../Captures/Api Specification Cap/12-muleSpec.png" />
</div>

3. Now click on `Responses (0)` > `Add New Response`.

<div align="center">
    <img src="../../Captures/Api Specification Cap/13-muleSpec.png" />
</div>

4. Click on `Add Body` and select the same options as in the second image.

<div align="center">
    <img src="../../Captures/Api Specification Cap/14-muleSpec.png" />
    <img src="../../Captures/Api Specification Cap/15-muleSpec.png" />
</div>

## /customers/{customerId}

1. Create a new `Resource` and add a `URI Parameter` as shown below:

<div align="center">
    <img src="../../Captures/Api Specification Cap/16-muleSpec.png" />
</div>

2. Click on `Responses (0)` > `Add New Response` > `Add Body` and change `Type` to `contact`.

<div align="center">
    <img src="../../Captures/Api Specification Cap/17-muleSpec.png" />
</div>

## Test your API using the mocking service

1. Click on the `Try it` icon from the right side of the screen.

<div align="center">
    <img src="../../Captures/Api Specification Cap/18-muleSpec.png" />
</div>

2. Select `Mocking Service`, provide an `Example id`, and send it.

    <img src="../../Captures/Api Specification Cap/19-muleSpec.png" />
    <img src="../../Captures/Api Specification Cap/20-muleSpec.png" />

    You can try with the other `Resource`.

## Publish your API to Anypoint Exchange

1. Click on the top side menu button `Publish` > `Publish to Exchange` and wait. It will return a link to `Exchange` to check our new API.

<img src="../../Captures/Api Specification Cap/21-muleSpec.png" />
<img src="../../Captures/Api Specification Cap/22-muleSpec.png" />

2. Open the link, and now we can see our API published.

<img src="../../Captures/Api Specification Cap/23-muleSpec.png" />
