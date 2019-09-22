---
layout: visual
title: Leaflet Heatmap
caption:
date: 2014-07-18

img: portfolio/leaflet-cluster.PNG
css: /assets/css/leaflet.css
data: /assets/data/map-points.json
categories: [d3]
tags: [d3]

description: 
---

<link rel="stylesheet" href="https://unpkg.com/leaflet@1.3.4/dist/leaflet.css"/>
<script src="https://unpkg.com/leaflet@1.3.4/dist/leaflet.js" integrity="sha512-nMMmRyTVoLYqjP9hrbed9S+FzjZHW5gY1TWCHA5ckwXZBadntCNs8kEqAWdrb9O7rxbCaA4lKTIWjDXZxflOcA==" crossorigin=""></script>
<script src="https://leaflet.github.io/Leaflet.heat/dist/leaflet-heat.js"></script>
<script src="https://d3js.org/d3.v4.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>

 
<script>
	var margin = {top: 0, right: 0, bottom: 0, left: 0},
		width = window.innerWidth - margin.left - margin.right,
		height = window.innerHeight - margin.top - margin.bottom,
		locations = [],
		top_layer = d3.select("body").append("div")
			.attr("id", "map")
			.style("position", "relative")
			.style("width", width + "px")
			.style("height", height + "px");
			
	// initialize the map
	var map = L.map('map', { zoomControl: false }).setView([-41.2858, 174.7868], 10),
		map_url = 'https://cartodb-basemaps-{s}.global.ssl.fastly.net/light_all/{z}/{x}/{y}.png',
		mapLink = '<a href="http://openstreetmap.org">OpenStreetMap</a>';

	new L.Control.Zoom({ position: 'bottomleft' }).addTo(map);	
	L.tileLayer( map_url, {
		attribution: '&copy; ' + mapLink + ' Contributors',
		maxZoom: 18,
	}).addTo(map);
	
	$(function() {
		d3.json("{{ page.data }}", function(data){
			data.objects.forEach(function(d) { 
				var location = [ d.circle.coordinates[0], d.circle.coordinates[1] ]; 
				location.push(1);
				locations.push(location);
			});

			createMap(locations);
		});
	});
	function createMap(data) {
		var heat = L.heatLayer(data,{
			radius: 50,
			blur: 100, 
			maxZoom: 15,
		}).addTo(map);
	}
</script>