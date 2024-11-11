# Prepare - Setup Bruno API client

To run the integration scenarios, you can use any API test client of your choice. In our exercise scripts,
we use the open source API client Bruno for which we have prepared a collection.
The collection contains sample requests and environment parameters to authenticate at the provided tenant.

## Download and install Bruno's desktop application

Skip this chapter if you run the exercises on the laptop provided by us. Here, the tool has been already installed.
Otherwise, if you run the exercises on your own laptop, you first need to download and install the Bruno API client.

See [Download Bruno's Desktop Application](https://docs.usebruno.com/get-started/bruno-basics/download).

## Import collection

Import the provided collection if not already done.

1. Download the collection **Guidelines-Exercises.json** from [here](/exercises/prep/download/Guidelines-Exercises.json).
2. Open Bruno and select **Import Collection** either from the menu or from the home screen.

<br>![](/exercises/prep/images/bruno-import-collection.png)

3. On the upcoming dialog, select the type **Bruno Collection**.

<br>![](/exercises/prep/images/bruno-import-collection-bruno.png)

4. Navigate to the location where you saved the beforehand downloaded collection and select the same.

<br>![](/exercises/prep/images/bruno-import-collection-file.png)

5. Browse to define a location, eventually create a new folder. Then select **Import**.

<br>![](/exercises/prep/images/bruno-import-collection-location.png)

## Select environment

As part of the collection, environment parameters have been maintained, that is **client id** and **client secret** to be able to authenticate at the Cloud Integration tenant.

1. You should see two requests. In order to be able to select an environment, you need to open any request.

<br>![](/exercises/prep/images/bruno-import-collection-requests.png)

2. If you select a request for the first time, you need to select the security level. Select **Safe Mode**.

<br>![](/exercises/prep/images/bruno-open-save-mode.png)

3. By default, no environment has been selected. From the drop down on the upper right corner, select the environment **eu03**.

<br>![](/exercises/prep/images/bruno-environment-configure.png)

## Summary

You've now prepared the API test client.

Navigate back to - [Main page](/README.md)
