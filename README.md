# Mapping Earthquakes
## Overview
### *Purpose*
The Disaster Reporting Network is a non-profit company that provides data-driven storytelling on disasters around the world. Basil is the head of the Earthquake Disaster Response Team and has asked for the development of website and mobile applications with the latest earthquake GEOJSON data from the US Geological Survey website. Basil would like this data to be used to create insightful data visualizations with interactive features on earthquakes from around the world. These data visualizations should show the difference between the magnitudes of earthquakes for the last seven days.

## Practice
### *Create a Simple Map*
I created an index.html file in my “Simple_Map” folder. I used an exclamation point to create a template in the html file. Then, I changed the document title to “Leaflet-Basic-Map” and in the “head” section, added the Leaflet CSS script:
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Leaflet-Basic-Map</title>
    
    <!-- Leaflet CSS -->
    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.7.1/dist/leaflet.css"
    integrity="sha512-xodZBNTC5n17Xt2atTPuE1HxjVMSvLVW9ocqUKLsCC5CXdbqCmblAshOMAS6/keqq/sMZMZ19scR4PsZChSR7A=="
    crossorigin=""/>

</head>
```
Next, in the body of the file, I added a “div” element with the id tag for the map and the Leaflet JavaScript script:
```
    <!-- The div that holds our map -->
    <div id="mapid"></div>
    <!-- Leaflet JavaScript -->
    <script src="https://unpkg.com/leaflet@1.7.1/dist/leaflet.js"
    integrity="sha512-XQoYMqMTK8LvdxXYG3nZ448hOEQiglfqkJs1NOQV44cWnUrBc8PkAOcXy20w0vlaXaVUearIOBhiXZ5V3ynxwA=="
    crossorigin=""></script>
```
I created two additional folders labelled “static” and “css”. Within the “css” folder, I created a new file called “style.css”. Within this file, I added the following CSS code to set the style for the map:
```
html,
body,
#mapid {
  width: 100%;
  height: 100%;
  padding: 0;
  margin: 0;
}
```
Then, I provided a CSS link in the “head” section of my index.html file to tell the index.html file to use the style.css file:
```
    <!-- Our CSS -->
    <link rel="stylesheet" type="text/css" href="static/css/style.css">
```
In my “static” folder, I created a new folder called “js”. Within the “js” folder, I created two new files, called “config.js” and “logic.js”. The “config.js” file was used to hold my Mapbox API key. Within the “logic.js” file, I added code to ensure that the file was working:
```
// Add console.log to check to see if our code is working.
console.log("working");
```
Within the “logic.js” file, I added the map object and set the geographical center of the map to that of the United States:
```
// Create the map object with a center and zoom level.
let map = L.map('mapid').setView([40.7, -94.5], 4);
```
To create a tile layer, I copied the tile layer code from the Leaflet Quick Start Guide, replacing the URL with the one from the “Static Tiles API” webpage and assigned it to the variable “streets” Within this block of code, I added the “accessToken” attribute and assigned it to the value of my “API_KEY”. Finally, I called the addTo() function with the map object to add the graymap object tile layer:
```
// We create the tile layer that will be the background of our map.
let streets = L.tileLayer('https://api.mapbox.com/styles/v1/mapbox/streets-v11/tiles/{z}/{x}/{y}?access_token={accessToken}', {
    attribution: 'Map data © <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, <a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, Imagery (c) <a href="https://www.mapbox.com/">Mapbox</a>',
    maxZoom: 18,
    accessToken: API_KEY
});

// Then we add our 'graymap' tile layer to the map.
streets.addTo(map);
```
I added the following “script” elements below the Leaflet JavaScript link in my index.html file to allow access to the “logic.js” and “confid.js” scripts:
```
    <!-- API key -->
    <script type="text/javascript" src="static/js/config.js"></script>
    <!-- Our JavaScript -->
    <script type="text/javascript" src="static/js/logic.js"></script>
```
### *Map a Single Point*
In my “Mapping_Earthquakes” folder, I created a new folder named “Mapping_Single_Points”. Within this new folder, I added the files from the “Simple_Map” folder. Then, I used the circleMarker() function to create a yellow circle marker with a radius of 300 over Los Angeles, California. I additionally replaced the “streets-v11” in the titleLayer() code to “dark-v10” to create a dark map:
```
//  Add a marker to the map for Los Angeles, California.
L.circleMarker([34.0522, -118.2437], {
    radius: 300, 
    color: "black",
    fillColor: "#ffffa1"
 }).addTo(map);

// We create the tile layer that will be the background of our map.
let streets = L.tileLayer('https://api.mapbox.com/styles/v1/mapbox/dark-v10/tiles/{z}/{x}/{y}?access_token={accessToken}', {
    attribution: 'Map data © <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, <a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, Imagery (c) <a href="https://www.mapbox.com/">Mapbox</a>',
    maxZoom: 18,
    accessToken: API_KEY
});
```
### *Map Multiple Points*
To map multiple points, I created a new folder called “Mapping_Multiple_Points” and copied the necessary folders and files from the “Mapping_Single_Points” folder. In a new “cities.js” file, I added the “cities” array containing the five most populous cities:
```
// An array containing each city's location, state, and population.
let cities = [{
    location: [40.7128, -74.0059],
    city: "New York City",
    state: "NY",
    population: 8398748
  },
  {
    location: [41.8781, -87.6298],
    city: "Chicago",
    state: "IL",
    population: 2705994
  },
  {
    location: [29.7604, -95.3698],
    city: "Houston",
    state: "TX",
    population: 2325502
  },
  {
    location: [34.0522, -118.2437],
    city: "Los Angeles",
    state: "CA",
    population: 3990456
  },
  {
    location: [33.4484, -112.0740],
    city: "Phoenix",
    state: "AZ",
    population: 1660272
  }
  ];
```
In the logic.js file, I created a variable “cityData” and assigned it to the “cities” array:
```
// Get data from cities.js
let cityData = cities;
```
Next, I used a forEach() function code to iterate through the “cityData” variable and get the coordinates of each city by adding “city.location” in the L.circlemarker() function. Within the L.circlemarker() function, I set the radius of the circle marker to the population of each city divided by 100000. The bindPopup() method was used on the circleMarker() function to retrieve the name of the city, state, and population. Each city was then added to the map with the addTo() function with the “map” object passed as the argument:
```
// Loop through the cities array and create one marker for each city.
cityData.forEach(function(city) {
    console.log(city)
    L.circleMarker(city.location, {
        radius: city.population/100000
    })
    .bindPopup("<h2>" + city.city + ", " + city.state + "</h2> <hr> <h3>Population " + city.population.toLocaleString() + "</h3>")
  .addTo(map);
});
```
In my index.html file I added the script for the path to the “cities.js” file:
```
    <!-- Our JavaScript -->
    <script type="text/javascript" src="static/js/cities.js"></script>
```
### *Map Lines*
I created a new folder called “Mapping_Lines” and copied the necessary folders and files from my “Mapping_Multiple_Points” folder. To practice mapping lines, I created a line from the Los Angeles International Airport (LAX) to the San Francisco International Airport (SFO) by first changing the coordinates for the centre of the map to a location between the two airports and the zoom level to 7:
```
// Create the map object with a center and zoom level.
let map = L.map('mapid').setView([36.1733, -120.1794], 7);
```
Then, I assigned each array of airport coordinates to the variable “line”:
```
// Coordinates for each point to be used in the line.
let line = [
    [33.9416, -118.4085],
    [37.6213, -122.3790]
  ];
```
Using the Leaflet polyline() function, I created a line on the map:
```
// Create a polyline using the line coordinates and make the line red.
L.polyline(line, {
    color: "red"
  }).addTo(map);
```
I created multiple lines by first adding additional coordinates to the “line” variable:
```
// Coordinates for each point to be used in the polyline.
let line = [
    [33.9416, -118.4085],
    [37.6213, -122.3790],
    [40.7899, -111.9791],
    [47.4502, -122.3088]
  ];
```
Then, I changed the color of the line to yellow by editing the value of the “color” key in the polyline() function:
```
// Create a polyline using the line coordinates and make the line red.
L.polyline(line, {
    color: "yellow"
  }).addTo(map);
```
Furthermore, I changed the style of the map to “satellite-streets-v11”:
```
// We create the tile layer that will be the background of our map.
let streets = L.tileLayer('https://api.mapbox.com/styles/v1/mapbox/satellite-streets-v11/tiles/{z}/{x}/{y}?access_token={accessToken}', {
    attribution: 'Map data © <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, <a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, Imagery (c) <a href="https://www.mapbox.com/">Mapbox</a>',
    maxZoom: 18,
    accessToken: API_KEY
});
```
Finally, I changed the center of the map to SFO and the zoom to 5:
```
// Create the map object with center at the San Francisco airport.
let map = L.map('mapid').setView([37.6213, -122.3790], 5);
```
### *Map GeoJSON Point Type*
I created a new folder called “Mapping_GeoJSON_Points” and copied the necessary folder and files from the previous folder. Then, I added a FeatureCollection object with properties and geometry for the San Francisco Airport:
```
// Add GeoJSON data.
let sanFranAirport =
{"type":"FeatureCollection","features":[{
    "type":"Feature",
    "properties":{
        "id":"3469",
        "name":"San Francisco International Airport",
        "city":"San Francisco",
        "country":"United States",
        "faa":"SFO",
        "icao":"KSFO",
        "alt":"13",
        "tz-offset":"-8",
        "dst":"A",
        "tz":"America/Los_Angeles"},
        "geometry":{
            "type":"Point",
            "coordinates":[-122.375,37.61899948120117]}}
]};
```
In my “logic.js” file, I changed the center of the map to the San Francisco Airport and set the zoom level to 10:
```
// Create the map object with center at the San Francisco airport.
let map = L.map('mapid').setView([37.5, -122.5], 10);
```
I created a GeoJSON layer using L.geoJSON() and added it to the map:
```
// Grabbing our GeoJSON data.
L.geoJSON(sanFranAirport).addTo(map);
```
I added the pointToLayer callback function to the L.geoJSON() layer to add a marker and used the bindPopup() method to the pointToLayer callback function to add data to a popup marker:
```
// Grabbing our GeoJSON data.
L.geoJson(sanFranAirport, {
    // We turn each feature into a marker on the map.
    pointToLayer: function(feature, latlng) {
      console.log(feature);
      return L.marker(latlng)
      .bindPopup(("<h2>" + feature.properties.name + "</h2> <hr> <h3> " + feature.properties.city + ", " + feature.properties.country + "</h3>"));
    }

  }).addTo(map);
```
I edited my “logic.js” file to add a popup marker using the onEachFeature function. Within the bindPopup(0 method I set the marker to show the airport code and name:
```
// Grabbing our GeoJSON data.
L.geoJson(sanFranAirport, {
    onEachFeature: function(feature, layer) {
      console.log(layer);
      layer.bindPopup(("<h2> Airport code :" + feature.properties.faa + "</h2> <hr> <h3> Airport Name: " + feature.properties.name + "</h3>"));
    }

  }).addTo(map);
```
### *Map Multiple GeoJSON Points*
After downloading the “majorAirports.json” file, I added the D3.js library file script to my index.html file in preparation to read the “majorAirports.json” file with the d3.json() method:
```
    <!-- d3 JavaScript -->
    <script src="https://d3js.org/d3.v5.min.js"></script>
```
Then, I edited the “logic.js” file by changing the center of the map to the geographical center of the Earth:
```
// Create the map object with center and zoom level.
let map = L.map('mapid').setView([30, 30], 2);
```
Then, I accessed the “majorAirports.json” file on GitHub with the following airportData variable:
```
// Accessing the airport GeoJSON URL
let airportData = "https://raw.githubusercontent.com/kcharb7/Mapping_Earthquakes/main/majorAirports.json";
```
Next, I added the d3.json() method with the “airportData” variable located within the parentheses. The then() method contained the anonymous function() with the data parameter that referenced the “airportData”. The data parameter was then added to the L.geoJSON() layer and added to the map:
```
// Grabbing our GeoJSON data.
d3.json(airportData).then(function(data) {
    console.log(data);
  // Creating a GeoJSON layer with the retrieved data.
  L.geoJson(data, {
    onEachFeature: function(feature, layer) {
      console.log(layer);
      layer.bindPopup(("<h2> Airport Code: " + feature.properties.faa + "</h2> <hr> <h3> Airport Name: " + feature.properties.name + "</h3>"));
    }
  }).addTo(map);

});
```
### *Add Multiple Maps*
To add multiple maps, I added another titleLayer() to my “logic.js” file to create a dark map:
```
// We create the dark view tile layer that will be an option for our map.
let dark = L.tileLayer('https://api.mapbox.com/styles/v1/mapbox/dark-v10/tiles/{z}/{x}/{y}?access_token={accessToken}', {
attribution: 'Map data © <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, <a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, Imagery (c) <a href="https://www.mapbox.com/">Mapbox</a>',
    maxZoom: 18,
    accessToken: API_KEY
});
```
Then, I added both map variables to a new variable named “baseMaps”:
```
// Create a base layer that holds both maps.
let baseMaps = {
    Street: streets,
    Dark: dark
  };
```
Following this, I added the map object:
```
// Create the map object with center, zoom level and default layer.
let map = L.map('mapid', {
    center: [30, 30],
    zoom: 2,
    layers: [streets]
});
```
I used the “control.layers” to control the layers displayed on the map:
```
// Pass our map layers into our layers control and add the layers control to the map.
L.control.layers(baseMaps).addTo(map);
```
Finally, I used the same code as above to access the airport data:
```
// Accessing the airport GeoJSON URL
let airportData = "https://raw.githubusercontent.com/kcharb7/Mapping_Earthquakes/main/majorAirports.json";

// Grabbing our GeoJSON data.
d3.json(airportData).then(function(data) {
    console.log(data);
  // Creating a GeoJSON layer with the retrieved data.
  L.geoJson(data, {
    onEachFeature: function(feature, layer) {
      console.log(layer);
      layer.bindPopup(("<h2> Airport Code: " + feature.properties.faa + "</h2> <hr> <h3> Airport Name: " + feature.properties.name + "</h3>"));
    }
  }).addTo(map);

});
```
### *Map GeoJSON LineStrings*
To create GeoJSON LineStrings, I created a new folder called “Mapping_GeoJSON_Linestrings” containing the necessary files and folders. Then, I added the “torontoRoutes.json” file to my main repository. After inspecting the data, I edited the “logic.js” file from the “Mapping_GeoJSON_Points” repository, replacing the streets title layer to “light” and the API URL to “light-v10”:
```
// We create the tile layer that will be the background of our map.
let light = L.tileLayer('https://api.mapbox.com/styles/v1/mapbox/light-v10/tiles/{z}/{x}/{y}?access_token={accessToken}', {
    attribution: 'Map data © <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, <a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, Imagery (c) <a href="https://www.mapbox.com/">Mapbox</a>',
    maxZoom: 18,
    accessToken: API_KEY
});
```
The key-value pair in the “baseMaps” base layer was additionally changed to include the light map:
```
// Create a base layer that holds both maps.
let baseMaps = {
    "Day Navigation": light,
    "Night Navigation": dark
  };
```
As the data was for Toronto, I changed the center of the map to Toronto with a zoom level of 2 and changed the default layer in the map object to “dark”:
```
// Create the map object with center, zoom level and default layer.
let map = L.map('mapid', {
    center: [44.0, -80.0],
    zoom: 2,
    layers: [dark]
});
```
I created a “torontoData” variable and assigned it to the URL for the “torontoRoutes.json” file on GitHub:
```
// Accessing the Toronto airline routes GeoJSON URL.
let torontoData = "https://raw.githubusercontent.com/kcharb7/Mapping_Earthquakes/main/torontoRoutes.json";
```
Finally, I edited the d3.json() to show flight routes in light yellow with a weight of 2:
```
// Grabbing our GeoJSON data.
d3.json(torontoData).then(function(data) {
    console.log(data);
  // Creating a GeoJSON layer with the retrieved data.
  L.geoJson(data, {
    color: '#ffffa1',
    weight: 2,
    onEachFeature: function(feature, layer) {
      console.log(layer);
      layer.bindPopup(("<h2> Airline: " + feature.properties.airline + "</h2> <hr> <h3> Destination: " + feature.properties.dst + "</h3>"));
    }
  }).addTo(map);
```
To make the code easier to read, I created an object called “myStyle” with the style parameters before the d3.json() code:
```
// Create a style for the lines.
let myStyle = {
  color: "#ffffa1",
  weight: 2
};
```
This object was then assigned to the “style” key:
```
// Grabbing our GeoJSON data.
d3.json(torontoData).then(function(data) {
    console.log(data);
  // Creating a GeoJSON layer with the retrieved data.
  L.geoJson(data, {
    style: myStyle,
    onEachFeature: function(feature, layer) {
      console.log(layer);
      layer.bindPopup(("<h2> Airline: " + feature.properties.airline + "</h2> <hr> <h3> Destination: " + feature.properties.dst + "</h3>"));
    }
  }).addTo(map);
```
### *Map GeoJSON Polygons*
I created a new folder named “Mapping_GeoJSON_Polygons” and added the necessary folders and files. Then, I downloaded the “torontoNeighborhoods.json” file to my GitHub repository. To map this data, I changed the map styles to “streets” and “satellite streets”:
```
// We create the tile layer that will be the background of our map.
let streets = L.tileLayer('https://api.mapbox.com/styles/v1/mapbox/streets-v11/tiles/{z}/{x}/{y}?access_token={accessToken}', {
    attribution: 'Map data © <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, <a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, Imagery (c) <a href="https://www.mapbox.com/">Mapbox</a>',
    maxZoom: 18,
    accessToken: API_KEY
});

// We create the dark view tile layer that will be an option for our map.
let satelliteStreets = L.tileLayer('https://api.mapbox.com/styles/v1/mapbox/satellite-streets-v11/tiles/{z}/{x}/{y}?access_token={accessToken}', {
attribution: 'Map data © <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, <a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, Imagery (c) <a href="https://www.mapbox.com/">Mapbox</a>',
    maxZoom: 18,
    accessToken: API_KEY
});
```
The code for the base layer was similarly changed:
```
// Create a base layer that holds both maps.
let baseMaps = {
    "Streets": streets,
    "Satellite Streets": satelliteStreets
  };
```
I changed the center of the map to Toronto with a zoom level of 11. I selected the “streets” tile layer as the default layer:
```
// Create the map object with center, zoom level and default layer.
let map = L.map('mapid', {
    center: [43.7, -79.3],
    zoom: 11,
    layers: [streets]
});
```
Next, I created the variable “torontoHoods” and assigned it to the GitHub URL for the “torontoNeightborhoods.json” file:
```
// Accessing the Toronto neighborhoods GeoJSON URL.
let torontoHoods = "https://raw.githubusercontent.com/kcharb7/Mapping_Earthquakes/main/torontoNeighborhoods.json";
```
I created a “myStyle” object to create a polygon with blue lines and a yellow fill color:
```
// Create a style for the polygon.
let myStyle = {
  color: "#3182bd",
  weight: 1,
  fillColor: "#ffffa1"
};
```
Finally, I edited the d3.json() method to include the “torontoHoods” variable and create a popup to show each neighborhood name:
```
// Grabbing our GeoJSON data.
d3.json(torontoHoods).then(function(data) {
  console.log(data);
// Creating a GeoJSON layer with the retrieved data.
L.geoJson(data, {
  style: myStyle,
  onEachFeature: function(feature, layer) {
    console.log(layer);
    layer.bindPopup(("<h2> Neighborhood: " + feature.properties.AREA_NAME + "</h2>"));
  }
}).addTo(map);
```
## Map Earthquake Data
### *Add Earthquake Data to a Map*
To create a map with all recorded earthquakes from the past seven days, I created a new folder called “Earthquakes_past7days” and added the necessary files and folders. Then, I created a file called “logicStep1.js”. Within this file, I applied the “streets” and “satelliteStreets” map styles used for the GeoJSON polygon mapping but changed the text for the map on the base layer to “Streets” and “Satellite”:
```
// Create a base layer that holds both maps.
let baseMaps = {
    "Streets": streets,
    "Satellite": satelliteStreets
  };
```
Then, I changed the geographic center to the United States and the zoom level to 3. The “streets” tile layer was set as the default:
```
// Create the map object with center, zoom level and default layer.
let map = L.map('mapid', {
    center: [39.5, -98.5],
    zoom: 3,
    layers: [streets]
});
```
I visited the USGS website to obtain the earthquake GeoJSON data recorded for the past seven days:
```
// Retrieve the earthquake GeoJSON data.
d3.json("https://earthquake.usgs.gov/earthquakes/feed/v1.0/summary/all_week.geojson").then(function(data) {
  // Creating a GeoJSON layer with the retrieved data.
  L.geoJson(data).addTo(map);

});
```
### *Add Style to the Earthquake Data*
To add style to the earthquake data map, I made a copy of the “logicStep1.js” file and renamed it “logicStep2.js”. Then, I changed the basic marker to a circleMarker by using the pointToLayer function:
```
// Retrieve the earthquake GeoJSON data.
d3.json("https://earthquake.usgs.gov/earthquakes/feed/v1.0/summary/all_week.geojson").then(function(data) {
  // Creating a GeoJSON layer with the retrieved data.
  L.geoJson(data, {
    // We turn each feature into a circleMarker on the map.
    pointToLayer: function(feature, latlng) {
      console.log(data);
      return L.circleMarker(latlng);
    },
  }).addTo(map);

});
```
Next, I created a function called “styleInfo()” containing all the style parameters for each earthquake plotted. Within this function, an additional function called “getRadius()” was created to calculate the radius for each earthquake:
```
  // This function returns the style data for each of the earthquakes we plot on
  // the map. We pass the magnitude of the earthquake into a function
  // to calculate the radius.
  function styleInfo(feature) {
    return {
      opacity: 1,
      fillOpacity: 1,
      fillColor: "#ffae42",
      color: "#000000",
      radius: getRadius(feature.properties.mag),
      stroke: true,
      weight: 0.5
    };
  }
```
The getRadius() function passed the “magnitude” as its argument in reference to the “feature.properties.mag” in the styleInfo() function. A conditional statement was used that set the magnitude to 1 if the magnitude of the earthquake in the JSON file was 0 so it could be plotted on the map. If the magnitude was greater than 0, then it was multiplied by 4:
```
  // This function determines the radius of the earthquake marker based on its magnitude.
  // Earthquakes with a magnitude of 0 will be plotted with a radius of 1.
  function getRadius(magnitude) {
    if (magnitude === 0) {
      return 1;
    }
    return magnitude * 4;
  }
```
To add style to the L.geoJson() layer, I added the “style” key and assigned it to the styleInfo function:
```
// Creating a GeoJSON layer with the retrieved data.
  L.geoJson(data, {
    // We turn each feature into a circleMarker on the map.
    pointToLayer: function(feature, latlng) {
      console.log(data);
      return L.circleMarker(latlng);
    },
    // We set the style for each circleMarker using our styleInfo function.
    style: styleInfo
  }).addTo(map);

});
```
### *Add Color and a Popup for Each Earthquake*
To make it easier to identify differences between earthquakes, I color-coded the earthquakes based on magnitude. To do this, I copied my “logicStep2.js” file and renamed it “logicStep3.js”. Then, inside the styleInfo() function, I set the “fillColor” key to a new function called “getColor()”. Inside the parentheses of this new function, I added the dot notation to get the magnitude:
```
// Retrieve the earthquake GeoJSON data.
d3.json("https://earthquake.usgs.gov/earthquakes/feed/v1.0/summary/all_week.geojson").then(function(data) {
  // This function returns the style data for each of the earthquakes we plot on
  // the map. We pass the magnitude of the earthquake into two separate functions
  // to calculate the color and radius.
  function styleInfo(feature) {
    return {
      opacity: 1,
      fillOpacity: 1,
      fillColor: getColor(feature.properties.mag),
      color: "#000000",
      radius: getRadius(feature.properties.mag),
      stroke: true,
      weight: 0.5
    };
  }
```
For the getColor() function, I wrote a conditional expression with logical operators for the magnitudes:
```
  // This function determines the color of the circle based on the magnitude of the earthquake.
  function getColor(magnitude) {
    if (magnitude > 5) {
      return "#ea2c2c";
    }
    if (magnitude > 4) {
      return "#ea822c";
    }
    if (magnitude > 3) {
      return "#ee9c00";
    }
    if (magnitude > 2) {
      return "#eecc00";
    }
    if (magnitude > 1) {
      return "#d4ee00";
    }
    return "#98ee00";
  }
```
After changing the colours of the markers, I edited the GeoJSON layer code to add a popup for magnitude and location by adding the “onEach Feature” function with the bindPopup() method:
```
  // Creating a GeoJSON layer with the retrieved data.
  L.geoJson(data, {
    // We turn each feature into a circleMarker on the map.
    pointToLayer: function(feature, latlng) {
        console.log(data);
        return L.circleMarker(latlng);
      },
    // We set the style for each circleMarker using our styleInfo function.
    style: styleInfo,
    // We create a popup for each circleMarker to display the magnitude and
    //  location of the earthquake after the marker has been created and styled.
    onEachFeature: function(feature, layer) {
    layer.bindPopup("Magnitude: " + feature.properties.mag + "<br>Location: " + feature.properties.place);
  }
  }).addTo(map);
```
### *Add Earthquake Data as an Overlay*
For this step, I copied the “logicStep3.js” file and renamed it “logicStep4.js”. To create an overlay layer for the earthquake data, I used the following code:
```
// Create the earthquake layer for our map.
let earthquakes = new L.layerGroup();
```
Then, I defined the overlay object:
```
// We define an object that contains the overlays.
// This overlay will be visible all the time.
let overlays = {
  Earthquakes: earthquakes
};
```
The “overlays” variable was then added to the Layers Control object:
```
// Then we add a control to the map that will allow the user to change
// which layers are visible.
L.control.layers(baseMaps, overlays).addTo(map);
```
To turn the “earthquakes” overlay button “on” I replaced the “map” variable in the “addTo(map)” function at the end of the L.geoJSON() layer code with “earthquakes” and added the line “earthquakes.addTo(map);” before the closing bracket:
```
  // Creating a GeoJSON layer with the retrieved data.
  L.geoJson(data, {
    // We turn each feature into a circleMarker on the map.
    pointToLayer: function(feature, latlng) {
        console.log(data);
        return L.circleMarker(latlng);
      },
    // We set the style for each circleMarker using our styleInfo function.
    style: styleInfo,
    // We create a popup for each circleMarker to display the magnitude and
    //  location of the earthquake after the marker has been created and styled.
    onEachFeature: function(feature, layer) {
    layer.bindPopup("Magnitude: " + feature.properties.mag + "<br>Location: " + feature.properties.place);
  }
  }).addTo(earthquakes);

    // Then we add the earthquake layer to our map.
    earthquakes.addTo(map);

});
```
### *Add a Legend to the Map*
The final step consisted of adding a legend for the color range of the earthquakes. To do so, I made a copy of the “logicStep4.js” file and renamed it “logicStep5.js”. Then, I created a legend control object with a position in the bottom-right of the map:
```
  // Create a legend control object.
  let legend = L.control({
    position: "bottomright"
  });
```
Next, I created the legend function:
```
  // Then add all the details for the legend.
  legend.onAdd = function() {
    let div = L.DomUtil.create("div", "info legend");
  };
```
Inside the “legend.onAdd” function, I added a “magnitudes” array to hold the magnitude levels and a “colors” array to hold the colors for the magnitudes:
```
  legend.onAdd = function() {
    let div = L.DomUtil.create("div", "info legend");
      const magnitudes = [0, 1, 2, 3, 4, 5];
      const colors = [
        "#98ee00",
        "#d4ee00",
        "#eecc00",
        "#ee9c00",
        "#ea822c",
        "#ea2c2c"
      ];
  };
```
Finally, I created a for loop to iterate through the “magnitudes” array and add the colour and text to the div element using “div.innterHTML +=”. For each iteration, a colour from the “color” array was added by styling the background of an “<i>” tag. Then, the interval between earthquake magnitudes for each color was added:
  
```
    // Looping through our intervals to generate a label with a colored square for each interval.
    for (var i = 0; i < magnitudes.length; i++) {
      console.log(colors[i]);
      div.innerHTML +=
        "<i style='background: " + colors[i] + "'></i> " +
        magnitudes[i] + (magnitudes[i + 1] ? "&ndash;" + magnitudes[i + 1] + "<br>" : "+");
    }
    return div;
  };

  legend.addTo(map);
```
In my “style.css” file, I added code to style the legend:
```
.legend {
  padding: 10px;
  line-height: 18px;
  color: #555;
  background-color: #fff;
  border-radius: 5px;
}
.legend i {
  width: 18px; 
  height: 18px;
  float: left;
  margin-right: 8px;
  opacity: 0.7;
}
```

# Earthquake Challenge
## Overview
### *Purpose*
After reviewing the earthquake maps, Basil asked for three additions:
1.	To see the earthquake data in relation to the tectonic plates’ location
2.	See all the earthquakes with a magnitude greater than 4.5
3.	A third map showcasing the data

## Add Tectonic Plate Data
I created a new folder called “Earthquake_Challenge” with the necessary folders and files. Then, I downloaded the starter code and renamed it “challenge_logic.js”. Within this code, I added a second layer group variable called “tectonicPlate” for the tectonic plate data below the “allEarthquakes” layer group:
```
// Add a 2nd layer group for the tectonic plate data.
let allEarthquakes = new L.LayerGroup();
let tectonicPlates = new L.LayerGroup();
```
Within the overlay object, I added a reference to the tectonic plate data:
```
// Add a reference to the tectonic plates group to the overlays object.
let overlays = {
  "Earthquakes": allEarthquakes,
  "Tectonic Plates": tectonicPlates
};
```
I used d3.json() to retrieve the tectonic plate data. Within the d3.json() method, I passed the tectonic plate data to the geoJSON() layer. I created a variable called “myStyle” to style the lines as red with a weight of 2. I assigned this variable to the “style” parameter in the geoJSON() layer. Then, I added the geoJSON() layer to the “tectonicPlates” layer. Finally, I added the “tectonicPlates” layer to the map:
```
// Create a style for the lines.
let myStyle = {
  color: "#ff0000",
  weight: 2
};

// Use d3.json to make a call to get our Tectonic Plate geoJSON data.
  d3.json("https://raw.githubusercontent.com/fraxen/tectonicplates/master/GeoJSON/PB2002_boundaries.json").then(function(data) {
    L.geoJson(data, {style: myStyle,}).addTo(tectonicPlates);

  // Then we add the tectonic plate layer to our map.
  tectonicPlates.addTo(map);

});
```
## Add Major Earthquake Data
In my “challenge_logic.js” file, I added a third layer group for the major earthquake data:
```
// Add layer groups for the tectonic plate and major earthquake data.
let allEarthquakes = new L.LayerGroup();
let tectonicPlates = new L.LayerGroup();
let majorEarthquakes = new L.LayerGroup();
```
Then, I added a reference to the major earthquake data within the overlay object:
```
// Add a reference to the tectonic plates and major earthquake groups to the overlays object.
let overlays = {
  "Earthquakes": allEarthquakes,
  "Tectonic Plates": tectonicPlates,
  "Major Earthquakes": majorEarthquakes
};
```
I used d3.json() to retrieve the major earthquake data. Within the d3.json() method, I used the same parameters in the styleInfo() function:
```
// Retrieve the major earthquake GeoJSON data >4.5 mag for the week.
d3.json("https://earthquake.usgs.gov/earthquakes/feed/v1.0/summary/4.5_week.geojson").then(function(data) {

  // Use the same style as the earthquake data.
  function styleInfo(feature) {
    return {
      opacity: 1,
      fillOpacity: 1,
      fillColor: getColor(feature.properties.mag),
      color: "#000000",
      radius: getRadius(feature.properties.mag),
      stroke: true,
      weight: 0.5
    };
  }
```
I changed the getColor() function to use three colours for the magnitudes less than 4, magnitudes greater than 4, and magnitudes greater than 5:
```
  // Change the color function to use three colors for the major earthquakes based on the magnitude of the earthquake.
  function getColor(magnitude) {
    if (magnitude > 5) {
      return "#ea2c2c";
    }
    if (magnitude >= 4) {
      return "#ea822c";
    }
    if (magnitude < 4) {
      return "#eecc00";
    }
  }
```
I used the same parameters for the getRadius() function:
```
  // Use the function that determines the radius of the earthquake marker based on its magnitude.
  function getRadius(magnitude) {
    if (magnitude === 0) {
      return 1;
    }
    return magnitude * 4;
  }
```
Then, I passed the major earthquake data into the geoJSON() layer. Within the geoJSON() layer, I turned each feature into a circleMarker on the map, styled each circle with the styleInfo() function, created a popup circle to display the magnitude and location of the earthquake, and added the “majorEarthquakes” variable to the map:
```
  // Creating a GeoJSON layer with the retrieved data that adds a circle to the map 
  // sets the style of the circle, and displays the magnitude and location of the earthquake
  //  after the marker has been created and styled.
  L.geoJson(data, {
    // We turn each feature into a circleMarker on the map.
    pointToLayer: function(feature, latlng) {
        console.log(data);
        return L.circleMarker(latlng);
      },
    // We set the style for each circleMarker using our styleInfo function.
    style: styleInfo,
    // We create a popup for each circleMarker to display the magnitude and location of the earthquake
    //  after the marker has been created and styled.
    onEachFeature: function(feature, layer) {
    layer.bindPopup("Magnitude: " + feature.properties.mag + "<br>Location: " + feature.properties.place);
    }
  }).addTo(majorEarthquakes);
  // Add the major earthquakes layer to the map.
  majorEarthquakes.addTo(map);

  // Close the braces and parentheses for the major earthquake data.
});
```
## Add an Additional Map
I added a third map style, “dark”, as a tile layer object using the following code:
```
// We create the third tile layer that will be the background of our map.
let dark = L.tileLayer('https://api.mapbox.com/styles/v1/mapbox/dark-v10/tiles/{z}/{x}/{y}?access_token={accessToken}', {
  attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, <a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, Imagery (c) <a href="https://www.mapbox.com/">Mapbox</a>',
  maxZoom: 18,
  accessToken: API_KEY
});
```
I added this “dark” map variable to the base layer object:
```
// Create a base layer that holds all three maps.
let baseMaps = {
  "Streets": streets,
  "Satellite": satelliteStreets, 
  "Dark": dark
};
```

