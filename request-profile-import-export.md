# Import/Export Request Profile

Request profiles created persist in the browser so they can be reused across pages locally, but it often occurs that peers need access to similar information. It would be inconvenient for them to create the same profiles. Instead, the extension supports exporting request profiles so they can be shared to others to import to have the same request profiles. They can also modify based on their own needs.

## Export Request Profile

To export a profile, click the **Rules** tab at the top of the extension. It will show the rules view which has all the request profiles in the extension. Click the profile you want to export on the left. The data representation of the rule will be shown on the right.

<img width="751" alt="diver-rules-view" src="https://user-images.githubusercontent.com/236573/31600114-0f49f9e4-b20a-11e7-9181-fc113a0fbedc.png">

Click the **Export** button on the top right. The profile will be exported as a file downloaded by the browser. Share this file with anyone will need access to the similar information.

## Import Request Profile

To import a profile, click the **Import** button at the top left. It will ask you to select the file to import. Note that the extension does not do deduping and merging, imports will not overwrite any current profiles. To remove a profile from the extension, click the **Delete** button at the top of the profile info pane in the **Traffics** tab.
