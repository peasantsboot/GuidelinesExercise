# Exercise 2 - Exactly Once scenario with receiver not idempotent

In this exercise, we will copy and run an integration flow implementing Exactly Once delivery in case that the receiver is not idempotent. In this case, the actuall call to the receiver needs to be placed within an idempotent process call to avoid duplicate messages.

## Create an integration package

As a prerequisite, you first need to create an integration package where the integration flows are created.

1. In the SAP Integration Suite landing page, navigate to **Design > Integrations and APIs**, and select  **Create**.

<br>![](/exercises/ex2/images/00-01-CreatePackage.png)
   
2. Fill in the **Name** of the integration package, e.g. **User XX** where **XX** is your user number from 00 to 99, and a short **Description**. The technical name is automatically set. Then click **Save**.

<br>![](/exercises/ex2/images/00-02-SavePackage.png)


## Copy provided integration flow

In the following, you will copy the integration flow **Pattern Quality Of Service - Receiver Not Idempotent** provided to you.

1. Navigate back to the list of packages by clicking the **Integrations and APIs** bread crumb.

<br>![image](/exercises/ex2/images/02-00-NavigateBack.png)

2. Open the package **Exactly Once Use Cases** by selecting the same.

<br>![image](/exercises/ex2/images/02-01-EnterEOPackage.png)
   
3. In the package **Exactly Once Use Cases**, switch to tab **Artifacts** and select **Copy** from the **Actions** menue of the integration flow **Pattern Quality Of Service - Receiver Not Idempotent**.

<br>![](/exercises/ex2/images/02-02-Copy.png)
   
4. In the upcoming dialog, click on **Select** to select a target integration package.

<br>![](/exercises/ex2/images/02-03-CopySelect.png)
   
5. From the list of packages, select your beforehand created package, i.e., package **User XX** where **XX** is the number assigned to you.

<br>![](/exercises/ex2/images/02-04-CopySelectPackage.png)

6. In the **Copy "Pattern Quality Of Service - Receiver Not Idempotent"** dialog, maintain the name of the target integration flow by replacing **_copy** with your user number **XX**. Then select **Copy**.

<br>![image](/exercises/ex2/images/02-05-CopyChangeName.png)

7. In the upcoming **Success** dialog, select **Navigate** to navigate to your package.

<br>![](/exercises/ex2/images/02-06-Navigate.png)


## Configure and deploy your integration flow

In the following, you will browse through the integration flow model to understand how Exactly Once delivery is guaranteed in case that the receiver is not idempotent. Furthermore, you will configure and finally deploy your copied integration flow.
    
1.  In your package, select the copied integration flow **Pattern Quality Of Service - Receiver Not Idempotent XX** with **XX** the ID assigned to you to open the model designer.

<br>![](/exercises/ex2/images/02-07-EnterModel.png)
    
2. In the integration flow designer you can browse through the model. Once done, select **Configure** from the top right.

<br>![](/exercises/ex2/images/02-08-IntegrationFlow.png)

3. In the configuration dialog, enter your number **XX** into the **participantNumber** parameter. The parameter value is actually appended to the integration flow end point to ensure a unique end point deployed on the tenant. Then **Save**.

<br>![](/exercises/ex2/images/02-09-ConfigureSave.png)
  
4. Once saved, **Deploy** the integration flow.

<br>![](/exercises/ex2/images/02-10-ConfigureDeploy.png)

5. In the upcoming confirmation dialog, keep the Runtime Profile **Cloud Integration** and select **Yes**. 

<br>![](/exercises/ex2/images/02-11-DeployConfirm.png)
   
6. Close the upcoming deployment information dialog by selecting **OK**.

<br>![](/exercises/ex2/images/02-12-DeploymentOK.png)
   
7. Let's check the deployment status. Navigate to **Monitor > Integrations and APIs** from the menu.

<br>![](/exercises/ex2/images/02-13-NavigateMonitoring.png)

8. In the monitoring overview page, select the tile **Manage Integration Content**.

<br>![](/exercises/ex2/images/02-14-ManageIntegrationContent.png)

9. In the **Manage Integration Content** page, filter for your ID **XX**. You should see your deployed integration flow in status **Started**. Select the **Copy entry point URL to clipboard** button next to the integration flow's end point as we will use it in the next step.

<br>![](/exercises/ex2/images/02-15-CopyEndPoint.png)

Now you are all set to test your scenario!

## Test the integration flow via Insomnia

In this chapter, you will test the integration flow. In the following, Insomnia is used. However you may use any other http client tool.

1. Open Insomnia and click on **Use the local Scratch Pad**.

<br>![image](/exercises/ex2/images/02-15a-Insomnia-ScratchPad.png)  

2. Create a **New HTTP-Request**.

<br>![image](/exercises/ex2/images/02-16-Insomnia-NewHTTPRequest.png)  

3. Change the request method from GET to POST, by clicking the dropdown icon next to GET and selecting entry **POST**.  

<br>![image](/exercises/ex2/images/02-17-Insomnia-SwitchOperation.png)  

4. **Paste the endpoint** from you integration flow as URL.  

<br>![image](/exercises/ex2/images/02-18-Insomnia-PasteEndPoint.png)  

5. Switch to tab **Body**, and select **XML** from the drop down menu.

<br>![image](/exercises/ex2/images/02-19-Insomnia-SelectXML.png)  

6. Enter the following payload into the body section and maintain your ID **XX** in the **PurchaseOrderNumber** attribute of the sample message.

```xml
<?xml version="1.0"?>
<ns0:PurchaseOrder xmlns:ns0="http://demo.sap.com/eip/qos" PurchaseOrderNumber="XX-001" OrderDate="2021-10-05">
	<DeliveryNotes>This is a test message for EO</DeliveryNotes>
	<Items>
		<Item ItemNumber="10">
			<ProductId>HT-1000</ProductId>
			<ProductName>Notebook Basic 15</ProductName>
			<Category>Notebooks</Category>
			<Quantity>1</Quantity>
			<CurrencyCode>EUR</CurrencyCode>
			<Price>956.00</Price>
		</Item>
		<Item ItemNumber="20">
			<ProductId>HT-1001</ProductId>
			<ProductName>Notebook Basic 17</ProductName>
			<Category>Notebooks</Category>
			<Quantity>1</Quantity>
			<CurrencyCode>EUR</CurrencyCode>
			<Price>1249.00</Price>
		</Item>
		<Item ItemNumber="30">
			<ProductId>HT-1030</ProductId>
			<ProductName>Ergo Screen</ProductName>
			<Category>Flat screens</Category>
			<Quantity>2</Quantity>
			<CurrencyCode>EUR</CurrencyCode>
			<Price>460.00</Price>
		</Item>
	</Items>
</ns0:PurchaseOrder>
```

<br>![image](/exercises/ex2/images/02-20-Insomnia-ChangeOrderNumber.png)  

7. Switch to tab **Auth** and choose **Basic Auth**.

<br>![image](/exercises/ex2/images/02-21-Insomnia-Auth.png)  

8. Provide following credentials:

<br>USERNAME =
```yaml
sb-3009327f-3dc1-4e3e-9853-5bd7c23e221d!b44358|it-rt-cpisuite-europe-03!b18631
```
<br>PASSWORD = 
```yaml 
e507568e-892c-443f-a6ba-4d53f76fecac$wS5Kq2nV25PlNT-U8bh8Yd-HGoBZpO-XW7Za9X3URE0=
```

<br>![image](/exercises/ex2/images/02-22-Insomnia-MaintainBasicAuth.png)  

9. Click **Send**. The request should return HTTP code 200 and a response confirming that the order has been successfully created.

<br>![image](/exercises/ex2/images/02-23-Insomnia-SendFirstTime.png)  

10. Keep the same order number and **Resend** the message. The request should return HTTP code 200 and a response informing you that the duplicate message has been discarded.

<br>![image](/exercises/ex2/images/02-24-Insomnia-SendSecondTime.png)  

## Retest the integration flow with trace switched on (Optional)

In the following, you may retest your integration flow with trace switched on. This chapter is optional. You may also skip this chapter and proceed to the [next exercise](../ex3/README.md).

1. Navigate back to the **Manage Integration Content** page of the monitor overview, and change the **Log Level** of your deployed integration flow to **Trace**.

<br>![image](/exercises/ex2/images/02-27-SwitchOnTrace.png)

2. Confirm the upcoming dialog by clicking **Change**.

<br>![image](/exercises/ex2/images/02-28-ConfirmTrace.png)

3. As you can see from the information below the Log Level settings, the trace has been switched on for a limited time.

<br>![image](/exercises/ex2/images/02-29-TraceInfo.png)

4. Navigate back to Insomnia, increment the purchase order number by **1**, and click **Send**. The request should return HTTP code 200 and a response confirming that the order has been successfully created.

<br>![image](/exercises/ex2/images/02-30-SendNewOrder.png)

5. Keep the same order number and **Resend** the message. The request should return HTTP code 200 and a response informing you that the duplicate message has been discarded.

<br>![image](/exercises/ex2/images/02-31-SendNewOrderAgain.png)

6. Navigate back to the **Manage Integration Content** page of the monitor overview, and select the **Monitor Message Processing** link below the **Artifact Details** of your deployed integration flow.

<br>![image](/exercises/ex2/images/02-32-NavigateMessageMonitor.png)

7. In the message monitor, you should see two new logs in status **Completed**. Select the **second** log entry from the top. Then select the **Trace** link next to the **Log Level** to open the trace.

<br>![image](/exercises/ex2/images/02-33-OpenTrace.png)

8. In the trace, you should see that the request reply step within the idempotent local integration process **Send message to receiver** has been carried out. Furthermore, in the local integration process **Send reply** the lower path has been carried out defining the default message reponse that the purchase order has been successfully created.

<br>![image](/exercises/ex2/images/02-34-Trace4FirstMessage.png)

9. Switch back and select the **uppermost** log entry. Then select the **Trace** link next to the **Log Level** to open the trace.

<br>![image](/exercises/ex2/images/02-35-OpenSecondTrace.png)

10. In the trace, you should now see that the idempotent local integration process **Send message to receiver** was skipped. Furthermore, in the local integration process **Send reply** the upper path has been carried out defining the message response in case of a duplicate.

<br>![image](/exercises/ex2/images/02-36-Trace4SecondMessage.png)

11. Finally, select the **Process Call** run step, then on the top switch to the **Message Content** tab, then switch to tab **Exchange Properties**. As you can see, the exchange property **CamelDuplicateMessage** was set to **true**.

<br>![image](/exercises/ex2/images/02-37-CamelDuplicateMessage.png)

## Summary

Congratulations. You have successfully tested your scenario.

Continue to - [Exercise 3 - Extend the Exactly Once scenario with Splitter step](../ex3/README.md)

