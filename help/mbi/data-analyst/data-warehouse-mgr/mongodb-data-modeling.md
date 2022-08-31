---
title: MongoDB data modeling guide
zendesk_id: 360016731711
---


When Magento BI pulls in MongoDB data, that data is translated into a relational model.

The bad news: While the majority of data patterns don’t pose an issue, there are a few that, because of the translation to a relational model, Magento BI doesn’t support.

The good news: All these patterns can be avoided.

## Sub-nested Arrays {#subnested}

If your collection looks like the example below, Magento BI will only replicate the data in the items array. Data from the subItems array won’t be pulled.

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

Collections that include objects with variable object keys aren’t replicated in Magento BI. For example:

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

This usually occurs where an object is being used and an array would be more appropriate. Let’s rework the above example:

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
