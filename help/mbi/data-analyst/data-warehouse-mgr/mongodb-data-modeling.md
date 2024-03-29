---
title: MongoDB data modeling
description: Learn how to avoid data patterns that pose an issue.
exl-id: 556c854b-5d7c-4f72-8ed7-5bc08d9ee5b9
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
---
# [!DNL MongoDB] Data Modeling

When [!DNL Adobe Commerce Intelligence] pulls in [!DNL MongoDB] data, that data is translated into a relational model.

The bad news: While most data patterns do not pose an issue, there are a few that are not supported by [!DNL Commerce Intelligence], because of the translation to a relational model.

The good news: All these patterns can be avoided.

## Subnested Arrays {#subnested}

If your collection looks like the example below, [!DNL Commerce Intelligence] only replicates the data in the items array. Data from the subitems array are not pulled.

```bash
    {
        _id: 0000000000000001
        items: [
            {
                _id: 0000000000000002
               subItems: [
                   {
                       _id: 0000000000000003
                      name: "Donut"
                      description: "glazed"
                   }
               ]
            }
        ]
    }
```

## Variable Object Keys {#varobjectkeys}

Collections that include objects with variable object keys are not replicated in [!DNL Commerce Intelligence]. For example:

```bash
    {
        _id: 0000000000000001
        friends: {
            0000000000000002: "Jimmy",
            0000000000000004: "Roger",
            0000000000000005: "Susan"
        },
    }
```

This usually occurs where an object is being used and an array would be more appropriate. Now, rework the above example:

```bash
    {
        _id: 0000000000000001
        friends: [
            { friend_id: 0000000000000002, name: "Jimmy" },
            { friend_id: 0000000000000004, name: "Roger" },
            { friend_id: 0000000000000005, name: "Susan"}
        ]
    }
```
