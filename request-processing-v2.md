# Request Processing

_(This doc applies to version 2 of the extension only. Go here for version 1: [Request Processing](request-processing.md))_

_(For updating version 1 custom processor to run in version 2: [Update V1 Custom Processor to V2](custom-processor-v1-to-v2.md))_

By default all request profiles come with the **Query** processor, which extracts and decodes all query parameters as data, but in some cases the interested data are not as simple as query parameters and they may need custom processing to become useful.

For example, on a **Twitch** page we want to create a request profile for all `/track` calls, but the data is Base64 encoded. The **Query** processor does not have much use here.

<img width="1344" alt="diver-twitch-unprocessed-v2" src="https://user-images.githubusercontent.com/236573/36067433-132264ba-0e72-11e8-9cdf-4bf1ae313268.png">

To handle cases like this, we can write a custom processor and add to the extension. A processor is comprised of the following things:

1. **name** for display purpose
2. **namespace** as a unique identifier
3. **process** as the function to transform requests to data objects

A barebone processor looks like this:

```javascript
function getProcessor() {
    return {
        name: 'Name',
        namespace: 'namespace',
        process: function process(traffic) {
            return {};
        }
    };
}
```

Here is the default **Query** processor for reference:

https://github.com/lalau/diver-processor/blob/master/query2.js

## Video Tutorial

If you prefer a video tutorial or you can't follow the steps below, you can watch the same steps here: https://youtu.be/FIp3W8u6ijY

## Creating Custom Processor

To make it easier to create a custom processor, the extension allows you to develop and test it within the extension using the requests on the page. Click the **Inspect** button of a request at the top of the request info pane. 

<img width="795" alt="diver-twitch-inspect" src="https://user-images.githubusercontent.com/236573/36067559-277fee4e-0e74-11e8-80ad-e8aea1504f69.png">

The extension will load the detail of that request and open it in the **Processors** view. Click the **Add** button to create a new custom processor.

<img width="794" alt="diver-twitch-inspecting" src="https://user-images.githubusercontent.com/236573/36067649-e8f4fa78-0e75-11e8-8aa7-3ac8c894f1e0.png">

The extension supports local processors and external processors. Local processors store the processor locally while external processors are hosted and accessible by URL. They work the same way. By default, the extension asks for processor URL of external processors. At this stage for development purpose, click the **Local** checkbox to toggle creating local processors.

<img width="794" alt="diver-twitch-local" src="https://user-images.githubusercontent.com/236573/36071271-a923391e-0ec0-11e8-930a-9567d51afa2d.png">

The extension gives you the barebone processor to start with. Add the custom namespace and then click the **Add** button to add the processor. Since the requests it processes are common to all Mixpanel **track** calls, I call it **Mixpanel** and use **mixpanel** as the namespace so it can be used for other pages that use Mixpanel too.

<img width="795" alt="diver-twitch-dummy-processor" src="https://user-images.githubusercontent.com/236573/36071268-a8dadea8-0ec0-11e8-8804-bfb7f5aa65b4.png">

Now we can test the processor with the inspecting request. The object in the **Inspecting** section will be passed to the **process** function as the **traffic** parameter.

<img width="794" alt="diver-twitch-added-processor" src="https://user-images.githubusercontent.com/236573/36071267-a8be7b8c-0ec0-11e8-8a05-c6aec87c3768.png">

Next we can click the **Edit** button in the processor section to update the **process** function to work on the request.

<img width="793" alt="diver-twitch-edit" src="https://user-images.githubusercontent.com/236573/36071269-a8f2cf68-0ec0-11e8-99eb-3f5574f13c08.png">

This is a sample processor written for this example:

https://github.com/lalau/diver-processor/blob/master/mixpanel2.js

In the **process** function, we do the following to extract the data:

1. Get the **data** query from the request
2. Decode it as query parameter
3. Base64 decode it
4. JSON parse it
5. return the parsed object

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

The sample processor can be tested by putting it into the extension and click the **Process** button in the **Inspecting** section. The result of the processing will be displayed in the **Processed** section.

<img width="794" alt="diver-twitch-processed" src="https://user-images.githubusercontent.com/236573/36071388-383a75da-0ec2-11e8-9f34-f09278e82e35.png">

Alternatively, the extension also allows you to export the request object for local development instead of developing and testing the processor within the extension. Click the **Export** button at the top of the request info pane. The browser will download the request.

<img width="794" alt="diver-twitch-export-v2" src="https://user-images.githubusercontent.com/236573/36071277-d3f28a0a-0ec0-11e8-9e7a-62297df92505.png">

E.g. https://github.com/lalau/diver-processor/blob/master/api.mixpanel.com-157.json

This is the same object shown in the **Inspecting** section and will be passed to the **process** function of the processor.

## External Processor

The processor created above is stored locally and ready to be used to process traffic, but the extension also supports externally hosted processor. To add an external processor, uncheck the **Local** checkbox and use the processor URL when adding processor.

<img width="794" alt="diver-twitch-external-processor" src="https://user-images.githubusercontent.com/236573/36071270-a90c2062-0ec0-11e8-9270-a67721979020.png">

## Using Custom Processor

To start using the added processor, go back to the request view by clicking the **Traffics** tab. Then open the profile detail. In the dropdown of the **Processors** section in the info pane, **Mixpanel** processor should be available to choose from.

<img width="794" alt="diver-profile-select-processor-v2" src="https://user-images.githubusercontent.com/236573/36071427-eee54d50-0ec2-11e8-8144-ca02ca69c0b4.png">

Select it and then click the **+** button to add the processor to the request profile. Since the **Query** processor doesn't provide much value here. We removed it as well.

<img width="302" alt="diver-profile-processor-added" src="https://user-images.githubusercontent.com/236573/31573954-3b57a324-b07a-11e7-9e75-08c084c79543.png">

We need to reload the page for changes to processors in profile to take effect. After reloading the page, the parsed data starts showing in the info pane.

<img width="943" alt="diver-profile-processor-processed-v2" src="https://user-images.githubusercontent.com/236573/36246514-118996de-11e5-11e8-87dd-bc4e1b20a25b.png">

With these data, we can select the keys we want to show in the table.

<img width="943" alt="diver-profile-processor-table-v2" src="https://user-images.githubusercontent.com/236573/36246555-43a8207c-11e5-11e8-8976-deb5dc7e7d60.png">

If at any time you want to look into a specific request because the processor doesn't work as expected, you can use the **Inspect** feature to tune the **process** function against the request and update the processor accordingly.

This example only shows parsing the query string into data, but the **traffic** object received by the **process** function contains the request header, response header, cookie, request body, and other information too. Custom processor can be written in a flexible way that can support a lot of different use cases.

Next: [Import and Export Profiles](request-profile-import-export.md)
