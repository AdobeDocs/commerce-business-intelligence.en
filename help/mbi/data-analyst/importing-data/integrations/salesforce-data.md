---
title: Expected Salesforce data
description: Learn about supported and unsupported objects in Salesforce data.
exl-id: 6625349f-2ec0-402d-8635-889a1f29811c
---
# Expected [!DNL Salesforce] data

[After the [!DNL Salesforce] setup is complete](../integrations/salesforce.md), a table for each queryable [object](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_objects_concepts.htm) - named `sf_/\{sobject-name}` - will be created in your data warehouse. 

>[!NOTE]
>
>The structure (columns) of each table is dependent on the fields contained in the object.

To get a list of objects available to your organization, refer to the [!DNL Salesforce] [Get a List of Objects documentation](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_describeGlobal.htm). After you have a list of objects, check out the [Entity Relationship Diagram (ERD) section](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_erd_majors.htm) of [!DNL Salesforce] documentation to see how entities relate to each other.

## Unsupported Objects

At this time, [!DNL Salesforce] does not currently expose the following objects in their API:

* `Announcement`
* `Attachment`
* `ContentDocumentLink`
* `External objects` - [What is an External Object?](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_objects_external_objects.htm)
* `CollaborationGroupRecord`
* `ContentDocument`
* `ContentDocumentLink`
* `FeedItem`
* `FieldDefinition`
* `IdeaComment`
* `ListViewChartInstance`
* `Order`
* `PlatformAction`

* `KnowledgeArticleVersion`
* `NewsFeed`
* `RecentlyViewed`
* `TopicAssignment`
* `UserRecordAccess`
* `UserProfileFeed`
* `Vote`

## Related:

* [Connecting [!DNL Salesforce]](../integrations/salesforce.md)
* [Reauthenticating integrations](https://support.magento.com/hc/en-us/articles/360016733151)
