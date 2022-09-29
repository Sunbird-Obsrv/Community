# Tracking Pageviews using raw Telemetry Data

Telemetry events with eid `IMPRESSION` can be used to create a time-series pageview graph. [Impression events](http://docs.sunbird.org/latest/developer-docs/telemetry/specification/#impression) are generated when a user visits any page. Impression events look like the one below

```JSON
{
  "eid": "IMPRESSION",
  "ets": 1664162202978,
  "ver": "3.0",
  "mid": "LOAD_TEST_6c029add-7508-43c4-aefc-9591cb53e5f9",
  "actor": {
    "id": "7ec05264-b111-4833-9594-55d807c44084",
    "type": "User"
  },
  "context": {
    "channel": "99fbe3f8-c07a-4ace-b0ac-f2fa7411da07",
    "pdata": {
      "id": "sunbird.app",
      "pid": "sunbird-portal.collectioneditor",
      "ver": "1"
    },
    "env": "user",
    "sid": "74489131-fdbb-448c-b36b-98fe8c70971b",
    "did": "7b238a24-bc15-487d-8a59-b4ad9f37d178",
    "cdata": [],
    "rollup": {
      "l1": "do_21271780182595993616932",
      "l2": "do_9e90c447-7b87-42d9-898b-6e6fbc990957",
      "l3": "do_869422f8-20ea-4e43-9f13-26c666c416d2",
      "l4": "do_3e187467-d966-4e6e-9af1-ea057acce678"
    }
  },
  "object": {
    "id": "do_21274813398450176015065",
    "type": "Community",
    "ver": "3",
    "rollup": {
      "l1": "do_21273610197362278414264",
      "l2": "do_21271780182595993616932",
      "l3": "do_312469507013812224118164",
      "l4": "do_21271780182595993616932"
    }
  },
  "edata": {
    "type": "workflow",
    "subtype": "Scroll",
    "pageid": "c5577e38-6c47-4795-952b-143057fdb15a",
    "uri": "/workspace/content/create",
    "duration": 9,
    "visits": []
  },
  "tags": []
}
```

Here, `ets` is the unix timestamp of when the event ocurred, and `edata.uri` is the relative URL of the page that was visited. Using these 2 attributes from IMPRESSION events, a graph like the below one can be generated. To do this, aggregate the events based on date, and then count the number of events for each date. This data can be used to plot a graph like below. 

![Visits Graph using IMPRESSION events](<../../.gitbook/assets/recipe-visits-bar-graph.png>)


Likewise, by aggregating on the `edata.uri` a table representing page wise total views may be generated.

![Page wise total views](<../../.gitbook/assets/recipe-views-pagewise.png>)