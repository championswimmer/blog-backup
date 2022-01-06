---
title: "Open-Event: An attempt to make an OSS framework for event apps and websites"
slug: open-event-an-attempt-to-make-an-oss-framework-for-event-apps-and-websites
date_published: 2015-06-24T00:00:00.000Z
date_updated: 2015-06-24T00:00:00.000Z
---

As I had already mentioned in the [earlier post]({% post_url 2015-05-29-GSOC-An-exciting-beginning %}) as a part of our GSoC project we are making a framework that lets Event/Conference organisers easily generate their own Webapps and Androi Apps for the event.

So the initial step was the concur on a data API. Because for the framework to work seamlessly for multiple events, all of them must be able the collate their data in form of a single API, so that the core components of the web/mobile app that display the data can be consistent.

Fortunately, there existed already an effort to create a standard API for event data - the [re-data API](https://github.com/opendatacity/re-data/blob/master/doc/api.md) made by OpenDataCity for the [re:publica](http://re-publica.de) event.

While trying to remain compliant with the re-data API we started off with a simplified subset of it.

Our API will have semantic versioning, and initially we are establishing v1 of it. So all API endpoints have the prefix `/get/api/v1/`

There is one top level `/event` endpoint that lists the basic info of all the events. If further details of an event is needed, we need to navigate into the namespace `/event/<event-id>/`

As you can see listed on your [API docs here](https://github.com/fossasia/open-event/blob/master/API.md) there are endpoints in the form of
`/event/<event-id>/sessions`
`/event/<event-id>/speakers`
`/event/<event-id>/tracks`

and so on, to return a list of sessions, speakers etc for the given event-id.
