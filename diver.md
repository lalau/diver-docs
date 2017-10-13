# Diver - Web Traffic Monitor Tool

Diver is a Chrome extension that allows you to monitor the network requests on a web page. While the browser's network panel provides general information of these requests, Diver's purpose is to monitor specific requests based on the rules set by the user and perform custom processing to present them in a manageable and readable format. In summary, the features include:

* Setup request profile to specify what requests to monitor
* Custom processing of requests to generate a data representation
* Select what data to manage in the request profile
* Export and import request profile to share the monitoring with others

--insert image here--

## Getting Started

1. Install the extension from Chrome Web Store: https://chrome.google.com/webstore/detail/ompelnpholagcjdmfomlhbmmmaneholh

2. It will ask you for permissions to allow the extension to read your traffic for monitoring and download files for exporting the profile. Proceed when prompted.

3. Once installed, open Chrome Developer Tools and there should be a **Diver** tab in the toolbar. <img width="900" alt="diver-in-dev-tool-bar" src="https://user-images.githubusercontent.com/236573/31487406-5daf1ac4-aeef-11e7-819f-560a5804135e.png">

4. Open the **Diver** tab on a web page then refresh the page. You should see that the extension starts receiving traffics. <img width="1085" alt="diver-receive-traffics" src="https://user-images.githubusercontent.com/236573/31487407-5dc6c264-aeef-11e7-83cd-a18df685d90f.png">

Read next about how to setup request profiles and other advanced usage:
1. [Setup Basic Request Profile](request-profile-basic.md)
2. [Advanced Options in Request Profile](request-profile-advanced.md)
3. [Custom Request Processing](https://www.google.com/)
4. [Import/Export Request Profile](https://www.facebook.com/)
