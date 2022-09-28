---
title: Connect Zendesk
description: Learn how to consolidate your help desk reporting in MBI.
---
# Connect Zendesk

>[!NOTE]
>
>[Requires Admin permissions.](../../../administrator/user-management/user-management.md)

![](../../../assets/Zendesk_logo.png)

Connecting your Zendesk data allows you to consolidate your help desk reporting in MBI. This allows you to optimize customer support and monitor help desk performance alongside your revenue.

Connecting your Zendesk data is a simple three-step process:

1. [Open the Zendesk credentials page in MBI](../#stepone)
1. [Retrieve your Zendesk API Token](../#steptwo)
1. [Enter your Zendesk login info and Token in MBI](../#stepthree)

To complete this process, you will need to open two browser windows or tabs - one for MBI, the other for your Zendesk account.

## Open the Zendesk credentials page in MBI {#stepone}

1. Go to the Integrations page under **Manage Data > Data Sources > Integrations**.
1. Click the **Add Integration** button, located on the right side of the screen.
1. Click the **Zendesk** icon. This will open the Zendesk credentials page.

## Retrieve your Zendesk API token {#steptwo}

1. In the window/tab where you are logged into your Zendesk account, click the **Settings** (gear) icon in the bottom-left corner of the screen.
1. When the Settings menu displays, locate the _Channels_ section. Click the **API** link in this section.
1. In the Token Access section of this page, click the checkbox next to Enabled. A list of Active API Tokens will display.
1. Click the **Add New Token** link.
1. When prompted, enter a label for the token. We recommend using `MBI`, so you will know, at a glance, what application is using the token.
1. Click Create.
1. An API token will be created. Copy this token; it'll be used in the next step.

## Enter Zendesk login info and API token into MBI {#stepthree}

1. Enter your Zendesk site prefix and login email in the Zendesk credentials page in MBI.
1. Enter your API token.
1. Click the Save & Connect button. If the connection is successful, a *Connection Successful!* message will display at the top of the screen.

## Related:

* [Expected Zendesk data](../integrations/exp-zendesk-data.md)
* [Reauthenticating integrations](https://support.magento.com/hc/en-us/articles/360016733151)
