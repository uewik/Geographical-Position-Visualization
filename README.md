In this project, I use the Google geocoding API to clean up some user-entered geographic locations of university names and then placing the data on a Google Map.

The first problem to solve is that the Google geocoding API is rate limited to 2500 requests per day.  So if you have a lot of data you might need to stop and restart the lookup process several times.  So I break the problem into two phases.  

In the first phase I take our input data in the file (where.data) and read it one line at a time, and retreive the geocoded response and store it in a database (geodata.sqlite). Before I use the geocoding API, I simply check to see if I already have the data for that particular line of input.

You can re-start the process at any time by removing the file geodata.sqlite.

Run the geoload.py program. This program will read the input lines in where.data and for each line check to see if it is already in the database and if I don't have the data for the location, call the geocoding API to retrieve the data and store it in the database.

The geoload.py can be stopped at any time, and there is a counter that you can use to limit the number of calls to the geocoding API for each run.

Once you have some data loaded into geodata.sqlite, you can visualize the data using the (geodump.py) program.  This program reads the database and writes tile file (where.js) with the location, latitude, and longitude in the form of executable JavaScript code.   

The file (where.html) consists of HTML and JavaScript to visualize a Google Map.  It reads the most recent data in where.js to get the data to be visualized.  Here is the format of the where.js file:

myData = [
[42.3396998,-71.08975, 'Northeastern University, 360 Huntington Avenue, Boston, MA 02115, USA'],
[40.6963857,-89.6160811, 'Bradley University, 1501 West Bradley Avenue, Peoria, IL 61625, USA'],
[32.7775,35.0216667, 'Technion, Viazman 87, Kesalsaba, 32000, Israel'],
   ...
];

Simply open where.html in a browser to see the locations.  You can hover over each map pin to find the location that the gecoding API returned for the user-entered input.  If you cannot see any data when you open the where.html file, you might want to check the JavaScript or developer console for your browser.
