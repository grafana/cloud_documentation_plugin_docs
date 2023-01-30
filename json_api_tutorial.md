## JSON API quickstart

-------------- START INTRO -------
-------------- END INTRO ---------



From the Grafana Cloud Portal, under "Manage your Grafana Cloud Stack." click "Launch" on the Grafana card.   <br />
(grafana image) <br />
From the home screen, select "+ Connect Data" and it will take you to the Integrations and Connections <br />
![Grafana Cloud Admin Panel](./images/home_admin.png) <br/>

Under "Search itegrations" type in "JSON API" <br />
![Json API Data source](./images/json_api_ds.png) <br />
Select JSON API and it will navigate you to the plugin home page. Select "Installation" <br />
![Json API Data source](./images/installation.png) <br />
On the installation screen, you will see your user on the account and you will be able to install the plugin (might need to word this better) <br />
#### V add screenshot from non personal account V
![Json API Data source](./images/install_json.png) <br />
Once installed, you will see "manage instance" and "remove plugin" <br />
![Json API Data source](./images/removeplugin.png) <br />
Navigate back to the Integrations and Connections screen and type in JSON API and you will now see it is installed. Click on the plugin to enter the plugins main page. <br />
![Json API Data source](./images/green.png) <br />
On the data source's home page ( might need to re word this because i refered to the home page as the page the download link takes you to), click "Create a JSON API data source" to enter the configuration screen.<br />
![Json API Data source](./images/dsscreen.png) <br />
In the configuration screen, you are able to name your data source and configure any auth or http to your liking. Once you select a URL you would like to use, click save and test, you will get a green sucess banner at the bottom of your screen, if you get an error, there is a possibility there are authentication issues or an incorrect URL. <br/>
![Json API Data source](./images/config.png) <br />
Select the dashboards icon on the side navigation and click "New Dashboard"<br />
![Json API Data source](./images/dash.png) <br />
Select add new Panel. <br />
![Json API Data source](./images/newpanel.png) <br />
On the panel page, you will see the data source drop down, select the JSON API data source with its corresponding name you gave it in the configuration. <br />
![Json API Data source](./images/dashpanel.png) <br />
Select Crypto Exchange and you will see "No data" on the panel, in your upper right corner, you will see the vizualizations dropdown. It is currently set to "Time Series", click on it and on the search input select "table" <br />
![Json API Data source](./images/select_table.png) <br />
![Json API Data source](./images/table.png) <br />
On the panel options screen, you can name your vizualization anything you want <br/>
![Json API Data source](./images/table_title.png) <br />
Now we can start to query our data source. <br />
Below you can see that we are getting the first markets base asset, quote asset, exchange ID, and the price in USD <br />
![Json API Data source](./images/first_query.png) <br />
We can now duplicate the query, I will duplicate it twice <br />
![Json API Data source](./images/duplicate.png) <br />
For the new queries, Lets change the market numbers, once the market numbers are changed and we have multiple queries, you can see a drop down being added in our table with A, B , C <br />
![Json API Data source](./images/all_q_table.png) <br />

We can rename our queries by hovering over the letter and clicking to edit <br />
![Json API Data source](./images/rename_market.png) <br />
![Json API Data source](./images/renamed.png) <br />
Now we have a table data source to query and visualize. On the top right, click apply to save our panel. <br />
![Json API Data source](./images/apply_table.png) <br />
Back on the dashboard screen you can see the table you just created. If you hover and click on the panel name "table" and scroll down to "more" and click duplicate, it can duplicate our table. Click the newly duplicated table name "edit"<br />
![Json API Data source](./images/interactive_table.png) <br />
![Json API Data source](./images/duplicate_panel_table.png) <br />
![Json API Data source](./images/edit.png) <br />

On the top right in the visualization drop down, click it and select bar gauge. Once you see the visualization, click apply on top to save. <br />
![Json API Data source](./images//bar_gauge.png) <br />
Our dashboard is looking awesome with two visuzliations. Lets add 1 more visualization that displays time series data. Copy one of the panels, duplicate it, and click edit. <br />
![Json API Data source](./images/exchange_dashboard_2.png) <br />
In the visualization drop down, select time series. Our query changes a little bit. instead of selecting a specific market, add an "*" to select all markets and add the updated.at field with a type of Time <br />
![Json API Data source](./images/time_series.png) <br />
Duplicate the query twice and replace USD with any of the location tickers, I will chose the New Zealand dollar and the Great Brittish Pound <br />
![Json API Data source](./images/final_time_series.png) <br />
Click apply to save. <br />
Now on our dashboard, we have 3 awesome visualizations to help keep up with the crypto markets. <br />
![Json API Data source](./images/final_dash.png) <br />


------ START CONCLUSION ------

------END CONCLUSION ---------
