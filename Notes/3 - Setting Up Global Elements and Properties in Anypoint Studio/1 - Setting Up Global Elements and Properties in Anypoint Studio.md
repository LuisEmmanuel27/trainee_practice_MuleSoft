# Setting Up Global Elements and Properties in Anypoint Studio

Open the project from <a href="../2 - Hello World/1 - Hello World.md">Hello Mule</a>.

## Create a global.xml file to keep the global elements

It's good practice to use a global.xml in Anypoint Studio because it allows you to define global elements that can be reused in different application flows. For example, you can configure a connection to a database or a message broker only once and reference it in other flows. This makes application maintenance and modification easier, as it avoids code duplication and improves readability.

1. Click on `Listener`, and the menu will open on the bottom side. Remember the `add` button? Well, click on the `edit` button next to the `add` button.

<div align="center">
    <img src="../../Captures/Global XML Cap/1-muleGlo.png"/>
</div>

2. This will bring up the window we saw when we created the `Connector configuration`. Simply press the `Cancel` button, and you'll notice this new window.

<div align="center">
    <img src="../../Captures/Global XML Cap/2-muleGlo.png"/>
</div>

3. The truth is, we can change the perspective by just clicking on these options.

    <img src="../../Captures/Global XML Cap/3-muleGlo.png"/>

    If you want to return to the window with the blocks, just click on `Message Flow`.

4. Right-click on the `root` file > `New` > `Mule Configuration File`. Give it the name `global.xml` and click on `Finish`.

##

5. Now click on `hellomule` > `Configuration XML` and cut the `http:listener-config`.

<div align="center">
    <img src="../../Captures/Global XML Cap/4-muleGlo.png"/>
</div>

6. Paste the `http:listener-config` inside the `mule` tags of `global` > `Configuration XML`. The program will ask you if you want to do that; click `Yes`, and it will give us an error.

<div align="center">
    <img src="../../Captures/Global XML Cap/5-muleGlo.png"/>
</div>

7. That's because the name has to be unique, but don't worry. Just save all changes, and the error will disappear.

<div align="center">
    <img src="../../Captures/Global XML Cap/6-muleGlo.png"/>
</div>

## Externalize the hardcoded values into properties

1. If we double-click on the global config or just click on the `Edit` button, we can see the properties in the `General` section, and they are `Hard Coded`. However, we don't want that, so click on `Cancel` and continue with the next step.

<div align="center">
    <img src="../../Captures/Global XML Cap/7-muleGlo.png"/>
</div>

2.  Right-click on `src/main/resources` > `New` > `File`. Name it `local.properties` and click on `Finish`.

3.  Add the following properties and save it:

    ```
    http.listener.host=0.0.0.0
    http.listener.port=8081
    ```

4.  Right-click on `src/main/resources` > `New` > `File`. Name it `dev.properties` and click on `Finish`. Add the same properties of `local.properties` and save it.

5.  Now open the properties of `global.xml` again, and we will change it with our new properties using the following syntax:

    ```
    ${http.listener.host}
    ```

    <img src="../../Captures/Global XML Cap/8-muleGlo.png"/>

    Finally, press `Ok` and save the file.

## Set up the Configuration Properties global element

1. In the `Global` window and under `Global Elements`, press the `Create` button. It will open a window; type `Configuration properties` and select it when it appears. Then, click on `Ok`.

2. Another window will appear, and you need to type the following text:

    ```
    ${env}.properties
    ```

    Press `Ok` and save it.

3. Again, press the `Create` button. This time, search for `Global property`, select it, and press `Ok`.

4. It will ask you for a name and a property, so type the following:

    ```
    name: env
    value: local
    ```

    <img src="../../Captures/Global XML Cap/9-muleGlo.png"/>

    Press `Ok` and save it.

5. Now, to be sure, go to `hellomule` > `Message Flow` and run the application. If everything is going well, you can test it again with your API tester.
