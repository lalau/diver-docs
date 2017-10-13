# Request Profile (Advanced)

Following the [basic usage](request-profile-basic.md) of request profile, there are other options that can give you a greater control on the profile:

1. Profile Name
2. Filter Syntax
3. Request Label
4. Data Name
5. Request View

If you prefer a video tutorial or you can't follow the steps below, you can watch the same steps here: https://youtu.be/hyPj-7Fe3yc

## Profile Name

When a request profile is created using the **Dive** button, the profile name defaults to the domain of the request. You can change it in the info pane of the profile. Click the **Edit** button next to the profile name. It will turn to a text field.

<img width="789" alt="diver-profile-name-edit" src="https://user-images.githubusercontent.com/236573/31561032-71cd6e6c-b00b-11e7-9555-77f588306b27.png">

Put the new name of the profile in the text field and click elsewhere. The profile name will be updated and reflected in the table.

<img width="791" alt="diver-profile-name-updated" src="https://user-images.githubusercontent.com/236573/31561033-71f0a120-b00b-11e7-9c87-ac4e4e04c352.png">

## Filter Syntax

Filter value supports exact match, wildcard and regular expression. Some filters also have special syntax.

### Exact Match

<img width="298" alt="diver-filter-exact-match" src="https://user-images.githubusercontent.com/236573/31561034-720ac654-b00b-11e7-945a-cdfb18d122be.png">

### Wildcard

<img width="297" alt="diver-filter-wildcard-match" src="https://user-images.githubusercontent.com/236573/31561035-7223cdf2-b00b-11e7-9600-af7db272a67e.png">

### Regular Expression

<img width="296" alt="diver-filter-regex-match" src="https://user-images.githubusercontent.com/236573/31561036-723e93d0-b00b-11e7-8a41-278871cd5824.png">

### Response Header

<img width="293" alt="diver-filter-header-match" src="https://user-images.githubusercontent.com/236573/31561037-72576270-b00b-11e7-8586-c702e2b4d335.png">

### Larger Than

<img width="296" alt="diver-filter-larger-than" src="https://user-images.githubusercontent.com/236573/31561038-727146ae-b00b-11e7-9c66-5279344337de.png">

## Request Label

Request label is used to give labels to requests that match certain criteria. Here is an example.

We want to monitor beacons made on the page and their timing, but the event is coded so it's not obvious what event they are without looking up reference. We can create labels for them.

<img width="798" alt="diver-label-setup" src="https://user-images.githubusercontent.com/236573/31561039-728a1ad0-b00b-11e7-931d-0e9cb659e519.png">

To create a label, enter the name of the Label in the **Labels** section of the info pane.
 
 <img width="305" alt="diver-new-label" src="https://user-images.githubusercontent.com/236573/31561040-72abcb94-b00b-11e7-9715-3b807f1f477e.png">
 
Then click the **+** button next to it. A label entry is created. There is also a **Label** column added to the front of the table. Next we can set the criteria of the label. Under the name of the label in the **Labels** section. Pick the type of the data (**Query**) and the data (**evt**) for it.

<img width="301" alt="diver-label-criteria" src="https://user-images.githubusercontent.com/236573/31561041-72ca4614-b00b-11e7-8859-8f91aef147c2.png">

Then click the **+** button next to them. An entry will be added with a text input to enter the value. Here we know that **5** means page load. So we put **5** in the text input. As soon as that is set. The request in the table will be updated with the label **Page Load**.

<img width="798" alt="diver-label-set" src="https://user-images.githubusercontent.com/236573/31561042-72e473ae-b00b-11e7-88c6-3331471ef548.png">

Using the same steps, we can create labels for other requests. Since we use **evt** to name the requests, we don't need it in the table now. We can deselect it in the **Data** section.

<img width="798" alt="diver-more-labels" src="https://user-images.githubusercontent.com/236573/31561043-72fe08dc-b00b-11e7-9d49-c4c59cf68961.png">

## Data Name

Following the same example, we want to monitor the timing of the beacon and it's denoted as **t** in the data. To make it more readable in the table, we can give it a name.

In the **Data** section, put the name next to the text input of the selected data.

<img width="304" alt="diver-data-name" src="https://user-images.githubusercontent.com/236573/31561044-7316d2a4-b00b-11e7-9bdb-6f22b7ea5768.png">

The name will be used in the table.

<img width="318" alt="diver-data-name-in-table" src="https://user-images.githubusercontent.com/236573/31561045-73345e50-b00b-11e7-9f0a-e7ea7e0faf5f.png">

## Request View

The data table and the raw table only have limited space. Sometimes they are too long to fit in the table and they will be truncated. In those cases, to view them in full you can click the button at the front of the request in the table. It will open the request view which display the detail of the request. You can also select which data to extract here for the profile it's in.

<img width="304" alt="diver-request-view" src="https://user-images.githubusercontent.com/236573/31561046-73674eb4-b00b-11e7-9c29-a118189275a2.png">

Next: [Custom request processing]()
