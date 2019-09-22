---
layout: visual
title: Leaflet Clustering
caption:
date: 2014-07-18

img: portfolio/leaflet-cluster.PNG
css: /assets/css/leaflet.css
data: /assets/data/map-points.json
categories: [d3]
tags: [d3]

description: 
---

<link rel="stylesheet" href="https://unpkg.com/leaflet@1.3.4/dist/leaflet.css" integrity="sha512-puBpdR0798OZvTTbP4A8Ix/l+A4dHDD0DGqYW6RQ+9jxkRFclaxxQb/SJAWZfWAkuyeQUytO7+7N4QKrDh+drA==" crossorigin=""/>
<link rel="stylesheet" type="text/css" href="https://cdnjs.cloudflare.com/ajax/libs/leaflet.markercluster/0.4.0/MarkerCluster.css" />
<link rel="stylesheet" type="text/css" href="https://cdnjs.cloudflare.com/ajax/libs/leaflet.markercluster/0.4.0/MarkerCluster.Default.css" />
 
<script src="https://unpkg.com/leaflet@1.3.4/dist/leaflet.js" integrity="sha512-nMMmRyTVoLYqjP9hrbed9S+FzjZHW5gY1TWCHA5ckwXZBadntCNs8kEqAWdrb9O7rxbCaA4lKTIWjDXZxflOcA==" crossorigin=""></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/leaflet.markercluster/1.4.1/leaflet.markercluster.js"></script>
<script src="https://unpkg.com/leaflet.featuregroup.subgroup@1.0.2/dist/leaflet.featuregroup.subgroup.js"></script>
<script src="https://adammertel.github.io/Leaflet.MarkerCluster.PlacementStrategies/dist/leaflet-markercluster.placementstrategies.src.js"></script>
<script src="https://d3js.org/d3.v4.min.js"></script>

<script type="text/javascript">
	var margin = {top: 0, right: 0, bottom: 0, left: 0},
		width = window.innerWidth - margin.left - margin.right,
		height = window.innerHeight - margin.top - margin.bottom,
		top_layer = d3.select("#visual").append("div")
			.attr("id", "map")
			.style("position", "relative")
			.style("width", width + "px")
			.style("height", height + "px");

	var map = L.map('map', { zoomControl: false }).setView([-41.2858, 174.7868], 13),
//	var map = L.map('map', { center: [10.0, 5.0], minZoom: 2, zoom: 2, zoomControl: false }),
		map_url = 'https://cartodb-basemaps-{s}.global.ssl.fastly.net/light_all/{z}/{x}/{y}.png',
		mapLink = '<a href="http://openstreetmap.org">OpenStreetMap</a>';

	new L.Control.Zoom({ position: 'bottomleft' }).addTo(map);				
	L.tileLayer( map_url, {
			attribution: '&copy; ' + mapLink + ' Contributors',
			maxZoom: 18,
		}).addTo(map);

/*		
	var LeafIcon = L.Icon.extend({
		options: {
			shadowUrl: 'leaf-shadow.png',
			iconSize:     [38, 95],
			shadowSize:   [50, 64],
			iconAnchor:   [22, 94],
			shadowAnchor: [4, 62],
			popupAnchor:  [-3, -76]
		}
	});	
	var greenIcon = new LeafIcon({iconUrl: 'leaf-green.png'}),
		redIcon = new LeafIcon({iconUrl: 'leaf-red.png'}),
		orangeIcon = new LeafIcon({iconUrl: 'leaf-orange.png'});
*/	
		
	var options = { elementsPlacementStrategy: "clock-concentric" }			
	var markerClusters = L.markerClusterGroup(options);			
			
	d3.json("{{ page.data }}", function(collection) {
		markerArray = [];
		collection.objects.forEach(function(d) {
			var latitude = d.circle.coordinates[0],
				longitude = d.circle.coordinates[1];

			m = L.marker([latitude, longitude]).bindPopup('A pretty CSS3 popup.<br> Easily customizable.');
//			markerClusters.addLayer(m);
			markerArray.push(m);
		});
				
		mySubGroup = L.featureGroup.subGroup(markerClusters, markerArray);

		markerClusters.addTo(map);
		mySubGroup.addTo(map);
				
//		map.addLayer( markerClusters );
	});	 
</script>
