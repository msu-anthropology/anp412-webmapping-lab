## ANP 412 Webmapping (With Leaflet) Lab

In this workshop, we're going to walk through how you load a map into a webpage, how to put a marker on the map, and how you bind a popup to that marker.  We'll be using [Leaflet](https://leafletjs.com/) for the workshop.  

To start off with, open the `basic_html_template.html` file in your code editor of choice (we'll use [Atom](https://atom.io/) for the workshop) - we'll use this as the base for the workshop and build on it as we progress through the various steps.  

> How do you download the files that this tutorial is working with?  The easiest way (if you aren't already familiar with Github is just to click the big green download Code button above and choose the Download Zip option.  This will download all of the files you'll be working with (as well as all of the other supplementary examples files.  

### Linking to the Leaflet Javascript Library Files

The first thing we need to do is point to the Leaflet CSS file and the Leaflet Javascript file.  This is basically telling the webpage where it will need to look for the Javascript it will be executing.  

1\. In the `<head>` section of the `basic_html_template.html` document (below the `<title>`, enter:

`<link rel="stylesheet" href="https://unpkg.com/leaflet@1.6.0/dist/leaflet.css"/>`

This links in the Leaflet stylesheet.  

2\. Now to link in the javascript library itself.  This is where all of the "code" is that you need to display and manipulate the map in the webpage.  In the <head> section of the basic_html_template.html document (below the `<title>`, enter:

`<script src="https://unpkg.com/leaflet@1.6.0/dist/leaflet.js"></script>`

For things to work properly, this block of code **must** below the previous block that linked to the LEaflet CSS file.  

### Loading and Displaying the Map in your Webpage

From here, you are ready to load and display the map in your page.  The process takes a couple of steps, but is not too complicated. 

1\. In the `<style>` section of the `basic_html_template.html` document, enter the following:

`#mysupermap{ width: 900px; height: 500px; }`

This sets the dimentions of the map you are going to display (it isn't the actual map...think of this as creating the canvas where you map will be displayed...the actual map will come in the next step).  A couple of important things here. First, `mysupermap` is just a silly name I've given for the map I'm going to display later.  Each map you display has to have a unique name - anything you want.  You'll have to use that name several times later in this workshop.  Second, the `#` is not part of the map name.  No matter what you name your map here, you will always have a `#` before it.  Thirdly, the stuff within the curly brackets determines the height and width (in pixels) of the map.  You can enter any value you want - making the map either larger or smaller.  

2\. From here you are going to tell the webpage where you want the map to be displayed.  Enter the following in the `<body>` section of the `basic_html_template.html` file.  

`<div id="mysupermap"></div>`

Wherever you put this (in the `<body>`section) is where your map will display.  The `id="mysupermap"` portion of this links to the size you set earlier for your map (which, in this case, we called `mysupermap`).  If you called your map anything else, you'll put its actual name nere instead of `mysupermap`.  

3\.  Now its time to initialize the map (which basically means we need to turn it on).  Tho do this, we will need to write some javascript.  The javascript we're writing is actually executing commands that are contained in the Leaflet javacript mapping library we linked to above.  In the `<script>` section of the `basic_html_template.html`, enter:

`var map = L.map('mysupermap').setView([51.4829377,-0.2420245], 12);`

This does a couple of things.  First, it initializes the map (turns it on).  Make sure you enter the correct map name you set earlier.  Second, it sets the location (in longitude and lattitude) for where the map will initiailly load up.  These are the two numbers in the `setView` section between the square brackets (in this case, `51.4829377,-0.2420245`).  You can choose any location you want.  The number (in this case `12` after the lat/long) sets the map's zoom level.  Basically, how close or how far away the map is zoomed when it is originally loaded.  The higher the number, the closer in the map is zoomed.  The lower the number, the further out it is zoomed. Experiment with the zoom value.  

4\. Now you need to tell the webpage which map tiles to display (and how to display them).  There are lots of options (as we've discussed).  In the case of this workshop, we're going to use Mapbox's streettile set.  Enter the following **below** the code you entered in the previosu step.  If you don't put it below. the map won't display:

`L.tileLayer('https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}?access_token=pk.eyJ1IjoibWFwYm94IiwiYSI6ImNpejY4NXVycTA2emYycXBndHRqcmZ3N3gifQ.rJcFIG214AriISLbB6B5aw', {`

Depending on the tile provider you are using, you'll have to enter a unique access token string.  As we've discussed, this is a unique indentifier (think of it as a password) that you get when you sign up for an account with the tile provider. The access token is passed to the tile provider's API (remember, you are making an API call to get the map tiles).

5\. **Below** this, enter:

`maxZoom: 18,`

This sets the maximum amount the map can zoom in.  The higher the number, the more the user can zoom in. The lower the number, the less they'll be able to zoom in.  Experiment with the value.

6\.  **Below** this, enter:

`attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, ' +
'<a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, ' +'Imagery © <a href="https://www.mapbox.com/">Mapbox</a>',` 
			
This adds the tile and data attributions that appear in the lower right hand corner of the map container.  Each tile provider has different requirements for attribution.  You can figure out what you need to enter by reading the tile provider's documentation.  Follow the requirements for attribution.  **Don't skip this**

7\. **Below** this, enter:

`id: 'mapbox/streets-v11'`

This sets the specific map tile style.  What goes here will varry from provider to provider.  **Read the provider's docuentation.**

8\. **Below** this, enter:

`}).addTo(map);`

This esentially closees out the Javasript command you started in step 4.  

At this point, your map should load in the browser.  It won't have anything on it - that comes next.  

### Adding a Marker to your Map

Once you've got your map displaying properly, adding a marker is actullay failry easy (really only one step).  

1\. **Below** the block of code you closed out in step 8 above (in the `<script>` section, enter:

`var marker = L.marker([51.494417, -0.223022]).addTo(map);` 

This is some javascript that tells the browser to create a marker and add it to the map at the coordinates (in lat and long) between the square brackets.  The syntax for the lat/long is identical to the syntax you used to decide the location where the map would initiailly load.  In this case, we're used `51.494417, -0.223022`, but you can use absolutley anything you want.  One thing to remember is that if the initial load locatio for the map is different from where you are loading the marker, the user won't be able to see the marker, they'll have to pan/zoom around to find it.  

### Adding a Popup to the Marker

Say you want a little pop-uo to open when the user clicks on the marker you've added to provide some information about that location.  How do you do that?  Its actually quite simple - just one single line of Javascript.  

1\. **Below** the line of code you added in the previous section, enter:

`marker.bindPopup("<b><center>Hammersmith</center></b>I'm an awesome neighborhood.");`

This "binds" the pop up to that marker.  The text within the quotation marks is what shows up in the pop up.  You can format it using HTML (or style it using CSS).  In this case, I've used a couple of simple HTML tags to formal the text a little.  Nothing complicated.

If you've done everything correctly, a pop up should appear when the user clicks on your marker.  

Do you want the pop up to open automatically when the user loads the page?  Thats pretty simple, you'll just need to add a little command to the code you entered in step 1 above:

`marker.bindPopup("<b><center>Hammersmith</center></b>I'm an awesome neighborhood.").openPopup();`

Everything is the same, except you've added the `.openPopup()` command at the end.  This basically tells the browser "hey, when the user loads the page, automatically open the pop up."

### Next Steps and Going Further

At this point, your page should load a map (in a specific location and a specific level of zoom) that has one marker on it.  When the user clicks the marker, a little pop up should open.  

Fom here, you can try:

* Loading in different tiles.  Have a look at `basic_leaflet_stamen_tiles.html` or `basic_leaflet_osm_tiles.html` for some examples
* Placing more than one marker on the map.  Have a look at `basic_leaflet_multiple_pins.html` for an example
* Bind pop ups to multiple markers.  Have a look at `basic_leaflet_multiple_pins_and_popups.html` for an example
* Make the map fullscreen. Have a look at `fullscreen_leaflet.html` for an example
* Make the fullscreen map edge to edge in the browser.  Have a look at `edge_to_edge_leaflet.html` for an example.  

### Some Helpful Resources

There are lots of grest reseources out there for learning Leaflet (or doing more than we've covered in this lab):

* Leflet itself ahs some pretty good tutorials: [https://leafletjs.com/examples.html](https://leafletjs.com/examples.html)
* Joshua Frazier's Leaflet tutorial (covers some of the same things we looked at, but goes a little further) [https://joshuafrazier.info/leaflet-basics/](https://joshuafrazier.info/leaflet-basics/)
* [Leaflet Tutorial](https://maptimeboston.github.io/leaflet-intro/), written for Maptime Boston by Andy Woodruff and Ryan Mullins that gets into some more advanced techniques such as incorporating jQuery, external geojson files and the Leaflet.markercluster plugin into a project.
* [Leaflet.JS Introduction](https://luxembourgjs.github.io/leaflet-demo/#/), by Thierry Nicola for JS Luxembourg.
* [Leaflet provider map](https://leaflet-extras.github.io/leaflet-providers/preview/index.html), an open source Leaflet extension that contains configurations for various free tile providers.
* [Mapbox Guides](https://docs.mapbox.com/help/) and [examples](https://docs.mapbox.com/mapbox.js/example/v1.0.0/) are great for learning about web maps in general in addition to Mapbox.js, which is built on top of Leaflet.
