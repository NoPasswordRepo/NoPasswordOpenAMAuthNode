![image alt text](/images/nopassword_logo.png)

# NoPassword Authentication Node

The NoPassword Authentication Node allows ForgeRock users to integrate their AM instance to the NoPassword authentication services.
This document assumes that you already have an AM 5.5+ instance running with an users base configured.

## Installation

Follow this steps in order to install the node:

1. Download the jar file from [here](target/nopassword-openam-auth-node-1.0.jar).
2. Copy the **nopassword-openam-auth-node-1.0.jar** file on your server: `/path/to/tomcat/webapps/openam/WEB-INF/lib`
3. Restart AM.
4. Login into NoPassword admin portal and open the `Keys` menu on the left side. Copy the **Generic API**, **AES Key** and **AES IV** values by clicking in the green button and save it for later.

![image alt text](/images/generic_api_key.png)

5. Login into AM console as an administrator and go to `Realms > Top Level Real > Authentication > Trees`.
6. Click on **Add Tree** button. Name the tree NoPassword and click **Create**.

![image](/images/add_tree.png)

7. Add 4 tree nodes: Start, Username Collector, NoPassword Service Initiator and Failure.
8. Connect them as shown in the image below.

![image](/images/tree_1.png)

9. Select the NoPassword node and set the Generic API Key and AES keys. Paste the keys values from step 4 on the field on the right side.
10. Add 3 nodes: Polling Wait Node, NoPassword Service Decision and Success and connect them as show in the image below.

![image](/images/tree_2.png)

11. Select the Polling Wait Node and set **Seconds To Wait** to 4.
12. Add a Retry Decision Limit node and connect it as show in the image below.

![image](/images/tree_3.png)

13. Select the Retry Decision Limit and set the **Retry Limit** to 15.
14. Save changes.
15. You can test the NoPassword authentication tree by accessing this URL in your browser `https://YOUR_AM_SERVER HERE/openam/XUI/?realm=/#login/&service=NoPassword`.</br>
16. Enter your username and hit enter. An authentication request will be send to NoPassword through the AM authentication tree. NoPassword will verify you username and key. If everything is correct you should get an authentication request on your phone.

![image](/images/demo_auth.png)

**Note:** If you wish to compile the project from sources then you'll have to install nopassword-commons dependency with maven which can be downloaded [here](https://github.com/NoPasswordRepo/nopassword-commons.git).