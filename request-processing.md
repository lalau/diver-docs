# Request Processing

By default all request profiles come with the **Query** processor, which extracts and decodes all query parameters as data, but in some cases data are not simple string and may need custom processing to become usable.

For example, on a **Twitch** page we want to create a request profile for all `/track` calls, but the data is Base64 encoded. The **Query** processor does not have much use here.

<img width="1211" alt="diver-twitch-unprocessed" src="https://user-images.githubusercontent.com/236573/31573948-3aaeb7c8-b07a-11e7-9f94-5774d03b30c7.png">

To handle cases like this, we can write a custom processor and add to the extension. A processor is comprised of the following things:

1. **name** for display purpose
2. **namespace** as a unique identifier
3. **process** as the function to transform requests to data objects

Here is the default **Query** processor as reference, custom processor should be written in the same format:

https://github.com/lalau/diver-processor/blob/master/query.js

If you prefer a video tutorial or you can't follow the steps below, you can watch the same steps here: https://youtu.be/

## Creating Custom Processor

To make it easier to write the **process** function, the extension allows you to export the request object for local development. Click the export button at the top of the request info pane. The browser will download the request.

<img width="800" alt="diver-twitch-export" src="https://user-images.githubusercontent.com/236573/31573949-3ac7cb32-b07a-11e7-8fee-55e977b601df.png">

E.g. https://github.com/lalau/diver-processor/blob/master/api.mixpanel.com-161.json

Objects with the same format will be passed to the **process** function when the processor is used, so we can use it as a reference. This is a sample processor written based on the exported request.

https://github.com/lalau/diver-processor/blob/master/mixpanel.js

Since the requests it process is common to all Mixpanel **track** call, I call it **Mixpanel** and use **mixpanel** as the namespace so it can be used for other pages that use Mixpanel too. In the **process** function, we do the following to extract the data:

1. Get the **params** query from the request
2. Decode it as query parameter
3. Parse it by removing the `data=` prefix
4. Base64 decode it
5. JSON parse it
6. return the parsed object

Example of parsed object returned.

```javascript
{
    "event": "quality_change_complete",
    "client_app": "twilight",
    "player": "frontpage",
    "channel": "dansgaming"
    //...
}
```

In general, the **process** functions of custom processors follow a similar pattern. Read the attributes in the request, parse them, and return as a key value object. 

## Adding Custom Processor

After creating the custom processor, it needs to be hosted in a place that the extension can load from. Due to Chrome's  security policy for extension, it can only load script from whitelisted domains. Currently the extension has only whitelisted jsDelivr (cdn.jsdelivr.net), so we will put our processor there. ([About jsDelivr](about-jsdelivr.md))

https://cdn.jsdelivr.net/gh/lalau/diver-processor@0.9/mixpanel.js

To add this processor to the extension, click the **Processors** tab at the top of the extension.

<img width="800" alt="diver-processors-tab" src="https://user-images.githubusercontent.com/236573/31573950-3ae0579c-b07a-11e7-8c94-cafafc8ca9da.png">

Before adding any custom processors, the **Processors** view only shows the default **Query** processor. Click the **Add** button at the top left of the extension. There will be text input for you to put the namespace of the processor and the URL to load the processor.

<img width="799" alt="diver-add-processor" src="https://user-images.githubusercontent.com/236573/31573951-3b12e928-b07a-11e7-851c-861a604a8811.png">

After setting these, click the **Add** button at the end of the namespace input to add the processor.

<img width="797" alt="diver-added-processor" src="https://user-images.githubusercontent.com/236573/31573952-3b295280-b07a-11e7-9a68-71587647a6eb.png">

Next, go back to the request view by clicking the **Traffics** tab. Then open the profile detail. In the dropdown of the **Processors** section in the info pane, **Mixpanel** processor should be available to choose from.

<img width="800" alt="diver-profile-select-processor" src="https://user-images.githubusercontent.com/236573/31573953-3b3f8bf4-b07a-11e7-908f-480ef9e6b08d.png">

Select it and then click the **+** button to add the processor to the request profile. Since the **Query** processor doesn't provide much value here. We removed it as well.

<img width="302" alt="diver-profile-processor-added" src="https://user-images.githubusercontent.com/236573/31573954-3b57a324-b07a-11e7-9e75-08c084c79543.png">

We need to reload the page for changes to processors to take effect. After reloading the page, the parsed data starts showing in the info pane.

<img width="754" alt="diver-profile-processor-processed" src="https://user-images.githubusercontent.com/236573/31573955-3b6f1cd4-b07a-11e7-9fe2-c159fdbead41.png">

With these data, we can select the keys we want to show in the table.

<img width="753" alt="diver-profile-processor-table" src="https://user-images.githubusercontent.com/236573/31573956-3b86d770-b07a-11e7-973b-6c3d981bf748.png">

## More Options

The current way of hosting processor on **jsDelivr** is far from ideal but it serves the purpose. The extension will be updated to have better support in terms of processor loading. It will be able to load from anywhere or just inline in the extension. It will also have better support for creating custom processor. For example, a tool that can test the processor against requests within the extension.

Next: [Import and Export Profiles](/)
