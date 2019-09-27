# Lab-5-Bus-Tracker (1/18/18)
Created: 1/18/18

# Overview

In this assignment, you will write an application that uses Ajax to dynamically update a web page with data retrieved from a web server.

## IMPORTANT: You will have to acquire two free developer's licenses in order to complete this lab: one is from Google, while the other is from MCTS (the Milwaukee County Transit System). More information on acquiring these keys can be found below.

#### 10 pts: You must demonstrate that you have retrieved your keys by end of W6 lectures.
## Assignment
## Background

The Milwaukee County Transit System maintains a website where you can obtain information about busses currently running on various routes. You can get a feel for the information available by looking at the MCTS real-time online bus map: visit the page, click on Routes, select a route, and zoom in on the map.

This web server can also serve up raw data in JSON format that can be retrieved by anyone who knows how to access it. You can retrieve the data from any route - for instance, the Green Line (Bayshore to the airport) is labeled as “GRE”. NOTE: You need to create an account with the MCTS real-time system and request a developer's key to access the data here. Warning: you will have to be careful about how frequently you retrieve data from the MCTS website; more than one access per second may result in being locked out of the site. This should not be a major limitation for this assignment.

As an example, point your browser at the following url (replacing the XXXXXXXXXXXXXX with your developer's key) to see the JSON response:

http://sapphire.msoe.edu:8080/BusTrackerProxy/BusInfo?key=XXXXXXXXXXXXXXX&rt=31

NOTE: The sapphire server is behind the MSOE firewall. As such, it is only accessible if you are on the MSOE network. If you are off-network, you must use a VPN tunnel.

This request asks the server to supply a JSON collection of bus data for all busses currently on route 31. For details on the API supported by the MCTS web server, consult the online documentation.

The JSON response should look something like this (but it varies in realtime as busses move):

{
	"bustime-response": {
		"vehicle": [
			{
				"vid": "5335",
				"tmstmp": "20160412 21:10",
				"lat": "43.045738220214844",
				"lon": "-88.04097290039063",
				"hdg": "269",
				"pid": 7799,
				"rt": "31",
				"des": "Medical Center (via State St.)",
				"pdist": 46539,
				"dly": false,
				"spd": 56,
				"tatripid": "2409",
				"tablockid": "31 -304",
				"zone": ""
			},
			{
				"vid": "4704",
				"tmstmp": "20160412 21:10",
				"lat": "43.03875574572333",
				"lon": "-87.92199983267949",
				"hdg": "80",
				"pid": 7801,
				"rt": "31",
				"des": "Downtown",
				"pdist": 46594,
				"dly": false,
				"spd": 2,
				"tatripid": "3203",
				"tablockid": "31 -351",
				"zone": ""
			}
		]
	}
}

## Goal
https://faculty-web.msoe.edu/hornick/Courses/se2840/labs/SE28461.jpg

In this assignment, you will write a web page that regularly tracks the Bus Information in a table format as well as on a Google Map (or MapQuest Map), similar to what is shown below:

Note that when the mouse hovers over a marker, the bus number is displayed (not shown here). When the marker is clicked, the bus's destination appears in a popup as shown.
Getting Started

This application has been started for you. In addition to the MCTS developer's key, you must obtain a Google API key following these instructions. Alternately, you can use MapQuest, but you must obtain a MapQuest API key following these instructions. Use the google key in the BusTracker.html or the mapquest key in the BusTrackerMQ.js file below.

BusTracker.html (google version)

BusTracker.js (google version)

BusTrackerMQ.html (mapquest version)

BusTrackerMQ.js (mapquest version)

key.js

The html and js files contain numerous comments that should help you to complete the implementation.
Validation and Testing

Your application must be able to handle errors, such as
*	no response from server (ajax request fails due to a network failure, server timeout, or other server error)
*	missing key or route in ajax request
*	invalid key specified in ajax request
*	invalid route specified in ajax request

In the first error, no JSON response will be received from the server - your ajax error handler will be invoked.

For the latter errors, different JSON responses will be received that you must distinguish from a normal response.

The sapphire server has been purposely modified to allow you to force these errors to occur for testing purposes, as follows:
*	If you supply a route parameter with value 1000, the server will simulate an internal error. The ajax request will succeed, but the JSON response will contain an error indication.
*	If you supply a route parameter with value 1001, the server will pretend it received a bad ajax request. The ajax request will fail.
*	If you supply a route parameter with value 1002, the server will pretend that you didn't supply a key or route. The ajax request will succeed, but the JSON response will contain an error indication.
*	If you supply a route parameter with value 1003, the server will intercept the key you pass and substitute an invalid key. The ajax request will succeed, but the JSON response will contain an error indication.

In all cases, you must present a meaningful error message to the user on the web page.

Extra Credit

You can receive 5 extra credit points (upon final submission) for each of the following features not shown here:
*	implement custom icons for the bus markers in place of pushpins (the default) representing the location of busses
*	delete the markers from the map when the Stop button is pressed
*	show only the last 10 markers (delete older ones) as the busses progress through their routes
*	Plus, you can add two more features of your own (with prior approval from me)
