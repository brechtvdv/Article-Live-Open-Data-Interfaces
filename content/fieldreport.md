## Field report on live Open datasets
{:#fieldreport}

This section gives an overview of how many live Open datasets are available in the [European](https://www.europeandataportal.eu/data/datasets) and [U.S.](https://data.gov) Open Data portals, what the rate of publication is and which update mechanism is used. Datasets were retrieved by doing a full-text search on “real-time” and only working and up-to-date datasets are mentioned. Note that this is a non-exhaustive overview, because among other reasons not all Open datasets are harvested by these portals.

<figure id="report" class="table" markdown="1">

| Country                  | Datasets | Update interval    | Update mechanism |
| ------------------------ |------------|--------|--------|-----------|-------------|----------|
| Belgium                   | Vehicles position (Public transport MIVB)    | 20s      | Polling      |
| Belgium                   | Bicycle counter    | realtime      | Polling      |
| Belgium                   |  Park+rides       | realtime      |
| France                   |  Parking and bicycle stations availability  |   60s    | Polling      |
| Sweden                   |  Notifications about Lightning Strikes  |   realtime    | Push-based      |
| Ireland                   |  weather station information, the Irish National Tide Gauge Network  |  3600s     | Polling      |
| UK                   |  River level data   |   900s    | Polling      |
| UK                   |  Cycle hire availability & arrival predictions (Transport for London Unified API)  |   300s    | Polling      |
| UK                   |  Arrival predictions (Transport for London Unified API)  |   realtime    | Push-based      |
| U.S.                   |  Real-Time Traffic Incident Reports of Austin-Travis County  |  300s     | Polling      |
| U.S.                   |  True Time API (arrival information and location of public transport vehicles)  |   realtime    | Polling      |
| U.S.                   | Current Bike Availability by Station (Nextbike)   |   300s    | Polling      |
| U.S.                   |  USGS Streamflow Stations  |    24h   | Polling      |
| U.S.                   |  NOAA water level (tidal) data of 205 Stations for the Coastal United States and Other Non-U.S. Sites  |   360s   | Polling      |
| U.S.                   |  [National Renewable Energy Laboratory](cite:cites nrel)  |   60s    | Polling      |
| U.S.                   |  RTC MetStation real time data  |   360s    | Polling      |
| U.S.                   |  Seattle Real Time Fire 911 Calls  |   300s    | Polling      |



<figcaption markdown="block">
Overview of live Open datasets according to their country, how fast it updates and whether a polling or push interface is used.
</figcaption>
</figure>

On [](#report) we see that live Open datasets from only five countries are harvested by the European Open Data portal. While we can argue that there are more relevant datasets than on this overview, for example by browsing for Open Data portals of specific cities or using Google Dataset Search[](cite:cites 10.1145/3308558.3313685), we still get a broad view of the current state-of-the-art interfaces. Only 2 datasets have a push interface available, both using the Websocket protocol, of which only the Transport for London (TfL) API from the U.K. is free to use. Interestingly, the True Time API from the U.S. offers the same functionality as the TfL API with arrival predictions for public transport, but uses polling instead of push-based update mechanism. On the one hand, we found live datasets related to the environment (water level, weather…) that publish at a lower rate (from every minute to every hour) with a polling-based interface. On the other hand, we found mobility related datasets whose update interval fits between realtime (as fast as possible) and 5 minutes. 

We also examined the public transport domain where GTFS-RT, a data specification for publishing live transit updates, takes no position[](cite:cites gtfsrt) on how updates should be published, except that HTTP should be used. OpenTripPlanner (OTP), a world-wide used multi-modal route planner which allows retrieving GTFS-RT updates and bicycle availabilities, also supports both approaches: setup a frequency in seconds for polling or subscribe to a push-based API.

Cryptocurrency trading is another domain which heavily uses push-based mechanisms for their clients. When people want to trade money or digital coins, it is crucial that the latency of prices, trades… are as low as possible, otherwise it can literally cost them money. The rate of publication of these live datasets are typically below 1 second. Websockets are de-facto used as a bidirectional communication channel is required for trading. General information (price tickings, books…) can be retrieved through an Open Web API. We tested three of them (Bitfinex, Bitmex and gdax) and saw over a span of one year that they were still available which makes us believe that Open push-based interfaces are a viable option for other domains as well.
