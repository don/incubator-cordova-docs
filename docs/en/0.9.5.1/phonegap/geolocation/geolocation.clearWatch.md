---
license: Licensed to the Apache Software Foundation (ASF) under one
         or more contributor license agreements.  See the NOTICE file
         distributed with this work for additional information
         regarding copyright ownership.  The ASF licenses this file
         to you under the Apache License, Version 2.0 (the
         "License"); you may not use this file except in compliance
         with the License.  You may obtain a copy of the License at

           http://www.apache.org/licenses/LICENSE-2.0

         Unless required by applicable law or agreed to in writing,
         software distributed under the License is distributed on an
         "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
         KIND, either express or implied.  See the License for the
         specific language governing permissions and limitations
         under the License.
---

geolocation.clearWatch
======================

Stop watching for changes to the device's location referenced by the `watchID` parameter.

    navigator.geolocation.clearWatch(watchID);

Parameters
----------

- __watchID:__ The id of the `watchPosition` interval to clear. (String)

Description
-----------

Function `geolocation.clearWatch` stops watching changes to the device's location by clearing the `geolocation.watchPosition` referenced by `watchID`.

Supported Platforms
-------------------

- Android
- BlackBerry (OS 4.6)
- BlackBerry WebWorks (OS 5.0 and higher)
- iPhone

Quick Example
-------------

    // Options: retrieve the location every 3 seconds
    //
    var watchID = navigator.geolocation.watchPosition(onSuccess, onError, { frequency: 3000 });

    // ...later on...

    navigator.geolocation.clearWatch(watchID);


Full Example
------------

    <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN"
                          "http://www.w3.org/TR/html4/strict.dtd">
    <html>
      <head>
        <title>Device Properties Example</title>

        <script type="text/javascript" charset="utf-8" src="phonegap.0.9.5.1.js"></script>
        <script type="text/javascript" charset="utf-8">

        // Wait for PhoneGap to load
        //
        function onLoad() {
            document.addEventListener("deviceready", onDeviceReady, false);
        }

        var watchID = null;

        // PhoneGap is ready
        //
        function onDeviceReady() {
            // Update every 3 seconds
            var options = { frequency: 3000 };
            watchID = navigator.geolocation.watchPosition(onSuccess, onError, options);
        }
    
        // onSuccess Geolocation
        //
        function onSuccess(position) {
            var element = document.getElementById('geolocation');
            element.innerHTML = 'Latitude: '  + position.coords.latitude      + '<br />' +
                                'Longitude: ' + position.coords.longitude     + '<br />' +
                                '<hr />'      + element.innerHTML;
        }

        // clear the watch that was started earlier
        // 
        function clearWatch() {
            if (watchID != null) {
                navigator.geolocation.clearWatch(watchID);
                watchID = null;
            }
        }
    
	    // onError Callback receives a PositionError object
	    //
	    function onError(error) {
	      alert('code: '    + error.code    + '\n' +
	            'message: ' + error.message + '\n');
	    }

        </script>
      </head>
      <body onload="onLoad()">
        <p id="geolocation">Watching geolocation...</p>
    	<button onclick="clearWatch();">Clear Watch</button>     
      </body>
    </html>