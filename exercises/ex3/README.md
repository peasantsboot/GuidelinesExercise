# Exercise 3 - Enhancing the Exactly Once scenario with a Splitter

In this exercise, we will enhance the previously copied integration flow with a Splitter step splitting the purchase order into its items. In this case, we need to adapt the idempotent process call configuration because one and the same purchase order number wouldn't be suffcient to find out whether an item has been already sent.

## Adapt your integration flow

In the following, you will enhance your integration flow by adding a Splitter.
    
1.  Navigate back to your package, and select your integration flow **Pattern Quality Of Service - Receiver Not Idempotent XX** with **XX** the ID assigned to you to open the model designer.

<br>![](/exercises/ex3/images/03-04-OpenModel.png)
    
2. In the integration flow designer, switch to **Edit** mode.

<br>![](/exercises/ex3/images/03-05-ChangeEditMode.png)

3. Select the **Get order ID** content modifier in your model, and select the **Plus** icon from the quick menu.

<br>![](/exercises/ex3/images/03-06-AddFlowStep.png)
  
4. In the upcoming screen, enter the search term **General**, and then select the entry **General Splitter** from the search hits.

<br>![](/exercises/ex3/images/03-07-AddSplitter.png)

5. A new splitter flow step should have been added between the **Get order ID** content modifier and the **Set Unique ID** content modifier. Select the **General Splitter** flow step. In the properties section of the **General Splitter**, switch to the **Processing** tab, and maintain the following: 

Expression Type: **XPath**

XPath Expression:
```yaml
//Item
```

Parallel Processing: **unselected**

<br>![](/exercises/ex3/images/03-08-ConfigureSplitter.png)

6. Next, select the **Set Unique ID** content modifier, switch to the **Message Header** tab, and enhance the source value of the **uniqueID** header by adding the splitter index to the purchase order. The header source value should be defined as follows:

```yaml
${property.orderNumber}_${header.CamelSplitIndex}
```

<br>![](/exercises/ex3/images/03-09-ChangeUniqueID.png)

7. Because we split the message, we need to add a gather step to be able to send out one single response. So, select the **Idempotent Process Call** step in your model, and select the **Plus** icon from the quick menu..

<br>![](/exercises/ex3/images/03-10-AddFlowStep.png)

8. In the upcoming screen, enter the search term **Gather**, and then select the entry **Gather** from the search hits..

<br>![](/exercises/ex3/images/03-11-AddGather.png)

9. A new gather flow step should have been added between the **Idempotent Process Call** and the **Process Call**. Select the **Gather** flow step, switch to the **Aggregation Strategy** tab, and maintain the following:.

Incoming Format: **Plain Text**

Aggregation Algorithm: **Concatenate**

<br>![](/exercises/ex3/images/03-12-MaintainGather.png)

10. **Save** your changes.

<br>![](/exercises/ex3/images/03-13-Save.png)

11. Once saved, **Deploy** the integration flow.

<br>![](/exercises/ex3/images/03-14-Deploy.png)

12. In the upcoming confirmation dialog, keep the Runtime Profile **Cloud Integration** and select **Yes**. 

<br>![](/exercises/ex3/images/03-15-ConfirmDeploy.png)
   
13. Close the upcoming deployment information dialog by selecting **OK**.

<br>![](/exercises/ex3/images/03-16-ConfirmOK.png)
   
14. Let's check the deployment status. Navigate to **Monitor > Integrations and APIs** from the menu.

<br>![](/exercises/ex3/images/03-17-NavigateMonitoring.png)

15. In the monitoring overview page, select the tile **Manage Integration Content**.

<br>![](/exercises/ex3/images/03-18-ManageIntegrationContent.png)

16. In the **Manage Integration Content** page, filter for your ID **XX**. You should see your deployed integration flow in status **Started**.

<br>![](/exercises/ex3/images/03-19-ArtifactDeployed.png)

Now you are all set to test your updated scenario!

## Test the splitter integration flow via Insomnia

In this chapter, you will test the integration flow. In the following, Insomnia is used. However you may use any other http client tool.

1. Reopen Insomnia, and select your request that you have created in the previous exercise. As you can see, it contains the previously pasted purchase order with three items. Increment the purchase order number by **1**, and click **Send**. The request should return HTTP code 200 and a response confirming that the order has been successfully created.

<br>![](/exercises/ex3/images/03-20-Insomnia-SendNewOrder.png)

2. Navigate back to **Monitor > Integrations and API**, and select the **All Artifacts** tile below **Monitor Message Processing**.

br>![](/exercises/ex3/images/03-21-MonitorTile.png)

3. In the **Monitor Message Processing** page, expand the filter section, and filter the **Sender** based on your participant number **XX**. You should see four new logs, one for your integration flow, and one for each of the overall three items which have been sent to a mocked receiver.

br>![](/exercises/ex3/images/03-22-MessageMonitor.png)

4. Navigate back to Insomnia. Keep the same order number and **Resend** the message. The request should return HTTP code 200 and a response informing you that the duplicate message has been discarded.

<br>![](/exercises/ex3/images/03-23-Insomnia-SendOrderAgain.png)

5. Navigate back to the **Monitor Message Processing** page, and **Refresh**. You should see only one more log for your integration flow. No further messages have been sent to the mocked receiver because they have been identified as duplicates and hence discarded.

br>![](/exercises/ex3/images/03-24-MessageMonitor.png)


## Summary

Congratulations. You have successfully updated and tested your splitter scenario.
