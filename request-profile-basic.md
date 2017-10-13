# Request Profile

Request profile allows you to setup rules on what requests to monitor, the processing you want on these requests and the what data to look at in the processed requests. The profile persists in your browser so you only need to set up once. In general, typical steps are:

1. Find the requests to monitor
2. Set up the filters for these requests
3. Select the data to extract in the requests

Here is an example of how to create and edit a request profile. If you prefer a video tutorial or you can't follow the steps below, you can watch the same steps here: https://youtu.be/HemkTs4aG_A

## Finding Requests

To create a request profile, open the **Diver** tab and go to the web page you want to monitor. You should see requests showing in the `Traffics` table. We need to find the requests you want to create profile for.

<img width="1212" alt="diver-no-request-profile" src="https://user-images.githubusercontent.com/236573/31485495-de7ebdb4-aee8-11e7-996a-6290801cbb47.png">

By default, this table only shows the first 30 requests. To change it, click on the dropdown saying `Trimmed`. You have the options to paginate through the requests or show all requests, but note that showing all requests will have performance impact on the extension when there are a lot of requests on the page.

<img width="403" alt="diver-view-options" src="https://user-images.githubusercontent.com/236573/31485496-de997e7e-aee8-11e7-905d-d4fe16d49d96.png">

The best way to find the requests we want is to use the filter, which matches the request url. Here we are interested in the `/data` call. By using that as the filter, now there are only see two requests.

<img width="786" alt="diver-filtered-requests" src="https://user-images.githubusercontent.com/236573/31485497-deb22528-aee8-11e7-93a7-06e991264381.png">

## Filtering Requests

We want to monitor the `/data` requests that go to **news.google.com**. Click on the **Dive** button next to that. A request profile is created. You should see a new table titled **news.google.com**.

<img width="787" alt="diver-new-request-profile" src="https://user-images.githubusercontent.com/236573/31485957-99e2f560-aeea-11e7-91ff-6bdc586fb425.png">

The profile created by the **Dive** button defaults to filter the requests using the domain only, so the table includes other requests as well. To change the profile, click the **Edit** button on the profile.

<img width="787" alt="diver-edit-request-profile" src="https://user-images.githubusercontent.com/236573/31485958-99fa7e24-aeea-11e7-8593-8db3a35a8c3a.png">

In the **Filters** section on the info pane, select path from the filter dropdown and click the **+** button next to it. A **path** filter is added to the list. Use `*/data` as the list value. Now the table only shows requests that match the domain and the path.

<img width="792" alt="diver-profile-filter-path" src="https://user-images.githubusercontent.com/236573/31485500-df0f8c54-aee8-11e7-9d2e-9829c7785779.png">

## Extracting Data

Next we want to extract data from the request and show them in the table. By default, profile comes with the **Query** processor that extract the query parameters in the request. Select the data we want to add to the table in the **Data** section. Once any data are selected in the **Data** section, you can toggle the table between **Raw** and **Data** view. Click on the **Data** button to look at the data table. The table now shows the selected data.

<img width="789" alt="diver-data-table" src="https://user-images.githubusercontent.com/236573/31485501-df2bd526-aee8-11e7-8999-e65685359c22.png">

Close the info pane. Click on the **Local** tab and the **For You** tab on the page. Now we see three entries in the table. It means there are three requests matching our profile and their data are extracted. Now you can refresh your page or navigate around to monitor these requests.

<img width="1219" alt="diver-data-table-more" src="https://user-images.githubusercontent.com/236573/31485713-99497ec2-aee9-11e7-9abf-12924820f07d.png">

You can follow these steps to create more request profiles.

Next: [Advanced Request Profile Usage](https://www.yahoo.com/)
