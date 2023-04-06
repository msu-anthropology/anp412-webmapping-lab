## ANP 412 Webmapping (With Leaflet) Lab

In this workshop, we're going to walk through how you load a map into a webpage, how to put a marker on the map, and how you bind a popup to that marker.  We'll be using [Leaflet](https://leafletjs.com/) (one of the most popular and widely used javascript mapping libraries) for the workshop.  

To start off with, open the `basic_html_template.html` file in your code editor of choice (we'll use [Atom](https://atom.io/) for the workshop) - we'll use this file as the base for the workshop and build on it as we progress through the various steps.  

*please note* - Atom has been mostly discontinued (though, you can still download it).  If you want to use another code editor, try [VSCode](https://code.visualstudio.com/). Alternative, there are a bunch of great (free) code editors (both Mac and PC) listed on the [Resources](https://anthropology.msu.edu/anp412-ss23/resources/) page on the course website.  

> How do you download the files that this tutorial is working with?  The easiest way (if you aren't already familiar with Github is just to click the big green download Code button above and choose the Download Zip option.  This will download the file you'll be working with (as well as all of the other supplementary examples files).  After you download it, unzip the folder and stick it somewhere safe and obvious on your computer - your desktop is probably the best.  
> 
Make sure you save the `basic_html_template.html` after every step (just in case).  You might also resave the file using a different filename - `basic_html_template_lastname.html` for example.

### Linking to the Leaflet Javascript Library Files

The first thing we need to do is point to the Leaflet CSS file and the Leaflet Javascript file.  This is basically telling the webpage where it will need to look for the Javascript and CSS it will be executing.  

1\. In the `<head>` section of the `basic_html_template.html` document (below the `<title>`, enter:

`<link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.3/dist/leaflet.css"
     integrity="sha256-kLaT2GOSpHechhsozzB+flnD+zUyjE2LlfWPgU04xyI="
     crossorigin=""/>`

This links in the Leaflet stylesheet.  

2\. Now to link in the javascript library itself.  This is where all of the "code" is that you need to display and manipulate the map in the webpage.  In the <head> section of the `basic_html_template.html` document (below the `<title>` *and* below the CSS link you added above, enter:

` <script src="https://unpkg.com/leaflet@1.9.3/dist/leaflet.js"
     integrity="sha256-WBkoXOwTeyKclOHuWtc+i2uENFpDZ9YPdf5Hf+D7ewM="
     crossorigin=""></script>`

For things to work properly, this block of code **must** be below the previous block that linked to the Leaflet CSS file.  

### Loading and Displaying the Map in your Webpage

From here, you are ready to load and display the map in your page.  The process takes a couple of steps, but is not too complicated. 

1\. In the `<style>` section of the `basic_html_template.html` document, enter the following:

`#mysupermap{ width: 900px; height: 500px; }`

This sets the dimentions of the map you are going to display (it isn't the actual map...think of this as creating the canvas where you map will be displayed...the actual map will come in the next step).  A couple of important things here. First, `mysupermap` is just a silly name I've given for the map I'm going to display later.  Each map you display has to have a unique name - anything you want.  You'll have to use that name several times later in this workshop.  Second, the `#` is not part of the map name.  No matter what you name your map here, you will always have a `#` before it.  Thirdly, the stuff within the curly brackets determines the height and width (in pixels) of the map.  You can enter any value you want - making the map either larger or smaller.  

2\. From here you are going to tell the webpage where you want the map to be displayed.  Enter the following in the `<body>` section of the `basic_html_template.html` file (but not in the `<script>` section).  

`<div id="mysupermap"></div>`

Wherever you put this (in the `<body>` section) is where your map will display.  The `id="mysupermap"` portion of this links to the size you set earlier for your map (which, in this case, we called `mysupermap`).  If you called your map anything else, you'll put its actual name nere instead of `mysupermap`.  

3\.  Now its time to initialize the map (which basically means we need to turn it on).  Tho do this, we will need to write some javascript.  The javascript we're writing is actually executing commands that are contained in the Leaflet javacript mapping library we linked to above.  In the `<script>` section of the `basic_html_template.html`, enter:

`var map = L.map('mysupermap').setView([51.4829377,-0.2420245], 12);`

This does a couple of things.  First, it initializes the map (turns it on).  Make sure you enter the correct map name you set earlier.  Second, it sets the location (in longitude and lattitude) for where the map will initiailly load up.  These are the two numbers in the `setView` section between the square brackets (in this case, `51.4829377,-0.2420245`).  You can choose any location you want.  The number (in this case `12` after the lat/long) sets the map's zoom level.  Basically, how close or how far away the map is zoomed when it is originally loaded.  The higher the number, the closer in the map is zoomed.  The lower the number, the further out it is zoomed. Experiment with the zoom value.  

4\. Now you need to tell the webpage which map tiles to display (and how to display them).  There are lots of options (as we've discussed).  In the case of this workshop, we're going to use the OpenStreetMap tile set.  Enter the following **below** the code you entered in the previosu step.  If you don't put it below. the map won't display:

`L.tileLayer('https://tile.openstreetmap.org/{z}/{x}/{y}.png', {`

5\. **Below** this, enter:

`maxZoom: 18,`

This sets the maximum amount the map can zoom in.  The higher the number, the more the user can zoom in. The lower the number, the less they'll be able to zoom in.  Experiment with the value.

6\.  **Below** this, enter:

`attribution: '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>'` 
			
This adds the tile and data attributions that appear in the lower right hand corner of the map container.  Each tile provider has different requirements for attribution.  You can figure out what you need to enter by reading the tile provider's documentation.  Follow the requirements for attribution.  **Don't skip this**

7\. **Below** this, enter:

`}).addTo(map);`

This esentially closees out the Javasript command you started in step 4.  

At this point, open the `basic_html_template.html` file you've been working on in your browser. If you've done everything correctly, you should see a map of London.  You should be able to zoom in, zoom out, and pan the map.  Congratulations!  You've successfully created a webpage that displays an interactive webmap.  

### Adding a Marker to your Map

Once you've got your map displaying properly, adding a marker is actullay fairly easy (really only one step).  

1\. **Below** the block of code you closed out in step 7 above (in the `<script>` section), enter:

`var marker = L.marker([51.494417, -0.223022]).addTo(map);` 

This is some javascript that tells the browser to create a marker and add it to the map at the coordinates (in lat and long) between the square brackets.  The syntax for the lat/long is identical to the syntax you used to decide the location where the map would initiailly load.  In this case, we've used `51.494417, -0.223022`, but you can use absolutley anything you want.  One thing to remember is that if the initial load location for the map is different from where you are loading the marker, the user won't be able to see the marker, they'll have to zoom out/pan around to find it.  

To view the your handiwork, just save the `basic_html_template.html` you've been working on and open it up in your browser of choice.  To save yourself a couple of steps, you might consider keeping the `basic_html_template.html` file open in a browser.  That way, you can save the file in Atom whenever you want and just hit refresh on the browser.  This will make the browser display the most recent verison of the `basic_html_template.html` file you just saved.  

### Adding a Popup to the Marker

Say you want a little pop-up to open when the user clicks on the marker you've added, to provide some information about that location, for instance.  How do you do that?  Its actually quite simple - just one single line of Javascript.  

1\. **Below** the line of code you added in the previous section, enter:

`marker.bindPopup("<b><center>Hammersmith</center></b>I'm an awesome neighborhood.");`

This "binds" the pop up to that marker.  The text within the quotation marks is what shows up in the pop up.  You can format it using HTML (or style it using CSS).  In this case, I've used a couple of simple HTML tags to formal the text a little.  Nothing complicated.

If you've done everything correctly, a pop up should appear when the user clicks on your marker.  

Do you want the pop up to open automatically when the user loads the page?  Thats pretty simple, you'll just need to add a little command to the code you entered in step 1 above:

`marker.bindPopup("<b><center>Hammersmith</center></b>I'm an awesome neighborhood.").openPopup();`

Everything is the same, except you've added the `.openPopup()` command at the end.  This basically tells the browser "hey, when the user loads the page, automatically open the pop up."
	
Thats it, you're done.  Congratulations, you just created a simmpl little webmap with a pin and an interactive pop up.  Pay yourself on the back and submit the file that you created (should just be one .html file).  

### Next Steps and Going Further

Want to go a little further?   Fom here, you can try:

* Loading in different tiles.  Have a look at `basic_leaflet_stamen_tiles.html` for an example.
* Placing more than one marker on the map.  Have a look at `basic_leaflet_multiple_pins.html` for an example.
* Bind pop ups to multiple markers.  Have a look at `basic_leaflet_multiple_pins_and_popups.html` for an example.
* Make the map fullscreen. Have a look at `fullscreen_leaflet.html` for an example.
* Make the fullscreen map edge to edge in the browser.  Have a look at `edge_to_edge_leaflet.html` for an example.  

### Some Helpful Resources

There are lots of grest resources out there for learning Leaflet (or doing more than we've covered in this lab):

* Leflet itself ahs some pretty good tutorials: [https://leafletjs.com/examples.html](https://leafletjs.com/examples.html)
* Joshua Frazier's Leaflet tutorial (covers some of the same things we looked at, but goes a little further): [https://joshuafrazier.info/leaflet-basics/](https://joshuafrazier.info/leaflet-basics/)
* [Leaflet Tutorial](https://maptimeboston.github.io/leaflet-intro/), written for Maptime Boston by Andy Woodruff and Ryan Mullins that gets into some more advanced techniques such as incorporating jQuery, external geojson files and the Leaflet.markercluster plugin into a project.
* [Leaflet.JS Introduction](https://luxembourgjs.github.io/leaflet-demo/#/), by Thierry Nicola for JS Luxembourg.
* [Leaflet provider map](https://leaflet-extras.github.io/leaflet-providers/preview/index.html), an open source Leaflet extension that contains configurations for various free tile providers.
* [Mapbox Guides](https://docs.mapbox.com/help/) and [examples](https://docs.mapbox.com/mapbox.js/example/v1.0.0/) are great for learning about web maps in general in addition to Mapbox.js, which is built on top of Leaflet.
