Raj Singh
	GEO APIs for mapping and more
	https://github.com/rajrsingh/locationtracker - this might be perfect for LyfeCycle

	1. HTML5 Geolocation
		• DeviceOrientation
			• Compass Heading
			• Accelleration
		• Geolocation
			• x, y, altitude
			• once, or contiunuous
		• Geolocation API: interfaces
			• void getCurrentPosition(PositionCallback success, PositionErrorCallback error, PositionOptions options)
			• long watchPsoition(PositionCallback success, PositionErrorCallback error, PositionOptions options)
			• void clearWatch(long watchID)
			• JSON response:
				coords.latitude
				coords.longitude
				coords.altitude
				coords.heading
				coords.speed
				coords.altitudeAccuracy
				timestamp
	2. Replication
	3. Geo Query
		• (Lucene/Solr)
		• Geo Search
		• Only for POINT data
		• Search geo-coordinates by indexing longitude and latitude fields
			• Bounding box
			• Radius
		• Can sort by distance using the following format:
		sort="<distance,<lon field name>,<lat field name>,<longitude>,<latitude>,<mi or km>>"

		https://rajrsingh.cloudant.com/worldcities/_design/wc/_search/byName?q=lat:[40 TO 44] AND lon:[-72 TO -68]
		• NOT only for PIINT data
		• More query types
			• Polygons (e.g. for neighborhoods)
			• NOT within
		• More on a par with Cloudant Geo / CouchDB 2.0
	4. Mapping with Leaflet
		• Best for mobile
		• leafletjs.com
		• tiles.mapbox.com
		• Cloudant or CouchDB - Javascript & JSON everywhere: from front end to databse
		• GeoJSON is a great standard for Javacentric-apps
		• Demos are easy, managing millions of locations is tougher
			• requires really good indexing
			• lightweight mapping apps need to catch up