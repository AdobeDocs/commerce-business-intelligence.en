---
title: Expected Salesforce data
description: Learn about supported and unsupported objects in Salesforce data.
---
# Expected Salesforce data

[After the Salesforce setup is complete](../integrations/salesforce.md), a table for each queryable [object](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_objects_concepts.htm) - named **sf_/\{sobject-name}** - will be created in your data warehouse. Note that the structure (columns) of each table is dependent on the fields contained in the object.

To get a list of objects available to your organization, refer to Salesforce's [Get a List of Objects documentation](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_describeGlobal.htm). After you have a list of objects, check out the [Entity Relationship Diagram (ERD) section](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_erd_majors.htm) of Salesforce's documentation to see how entities relate to each other.

## Unsupported Objects

At this time, Salesforce does not currently expose the following objects in their API:

* Announcement
* Attachment
* ContentDocumentLink
* External objects - [What is an External Object?](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_objects_external_objects.htm)
* CollaborationGroupRecord
* ContentDocument
* ContentDocumentLink
* FeedItem
* FieldDefinition
* IdeaComment
* ListViewChartInstance
* Order
* PlatformAction

* KnowledgeArticleVersion
* NewsFeed
* RecentlyViewed
* TopicAssignment
* UserRecordAccess
* UserProfileFeed
* Vote

## Related:

* [Connecting Salesforce](../integrations/salesforce.md)
* [Reauthenticating integrations](https://support.magento.com/hc/en-us/articles/360016733151)
