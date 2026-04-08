---
title: Onboarding Adobe Commerce Intelligence
description: Learn about onboarding Adobe Commerce Intelligence.
exl-id: e0cce957-af2c-4514-9afd-c9aaa651a4f0
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
TQID: https://experienceleague.adobe.com/36wmj-7QyDdemBWFwHTf1NJkd4H06tED9FZPqhFz8eg
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: b5f00040-57a0-4a6d-a39e-383b1936c2c9
    internal-label: Compliance
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
    internal-label: Reporting
subfeature_v2:
  - id: bcbf87e7-9b75-4596-bffe-0f376b4c73a7
    internal-label: GDPR
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
---
# Onboarding [!DNL Adobe Commerce Intelligence]

The onboarding questions related to `store` and `database` settings ensure that you set up your reporting correctly. With these answers, Adobe delivers your reports that are precisely tailored to your store's setup.

## Store settings

-  *Does your store accept guest checkout?* - Select **yes** if you allow customers to make a purchase from your store without registering for an account.

-  `Timezone` - Select the `timezone` that you would like to see your reporting in.

-  `Currency` - Select the `currency` that your store operates in.

-  `Your week starts on...` - Select the day of the week that you would like to be the start of the week in your reports.

-  *Which version of Commerce do you use?* - Select the `currency` that your store operates in.

-  *Is your store based in the European Union?* - If you answer `Yes` to this question, Adobe host your Data Warehouse and all of your data in the European Union, in compliance with GDPR.

## Database settings

-  `Database name` - What is the *name of the [!DNL MySQL] database* where your Commerce transactional data resides?

-  `Table prefix (optional)` - Are the tables contained in your Commerce database prepended by anything (for example, `store_`)? This is not normally the case, but it is a customization that can be made.
