---
layout: visual
title: D3 Circle Packing
caption:
date: 2014-07-18

img: portfolio/circle-packing.PNG
css: /assets/css/circle-packing.css
data: /assets/data/flare.json
categories: [d3]
tags: [d3]

description: 
---
<link rel="stylesheet" href="{{ page.css }}">
<script src="https://d3js.org/d3.v5.min.js"></script>

<script>
	// set the dimensions and margins of the graph
	var margin = {top: 25, right: 25, bottom: 25, left: 25},
		width = Math.max(300, window.innerWidth - margin.left - margin.right),
		height = Math.max(300, window.innerHeight - margin.top - margin.bottom),
		diameter = Math.min(width, height);

	// format variables
//	var format = d3.format(",d"),
//		color = d3.scaleOrdinal(d3.schemePaired);
	var color = d3.scaleLinear()
		.domain([-1, 5])
		.range(["hsl(152,80%,80%)", "hsl(228,30%,40%)"])
		.interpolate(d3.interpolateHcl);

	// append the svg object to the body of the page
	var div = d3.select("body").append("div");
	var svg = div.append("svg")
				.attr("width", width + margin.left + margin.right)
				.attr("height", height + margin.top + margin.bottom);
	var g = svg.append("g").attr("transform", "translate(" + (width + margin.left + margin.right) / 2 + "," + (height + margin.top + margin.bottom) / 2 + ")");

	var pack = d3.pack()
		.size([diameter, diameter])
		.padding(10);

	d3.json("{{ page.data }}").then(function(root) {
	  root = d3.hierarchy(root)
		  .sum(function(d) { return d.size; })
		  .sort(function(a, b) { return b.value - a.value; });

	  var focus = root,
		  nodes = pack(root).descendants(),
		  view;
		  
	  var circle = g.selectAll("circle")
		.data(nodes)
		.enter().append("circle")
		  .attr("class", function(d) { return d.parent ? d.children ? "node" : "node node--leaf" : "node node--root"; })
		  .style("fill", function(d) { return d.children ? color(d.depth) : null; })
		  .on("click", function(d) { if (focus !== d) zoom(d), d3.event.stopPropagation(); });

	  var text = g.selectAll("text")
		.data(nodes)
		.enter().append("text")
		  .attr("class", "label")
		  .style("fill-opacity", function(d) { return d.parent === root ? 1 : 0; })
		  .style("display", function(d) { return d.parent === root ? "inline" : "none"; })
		  .text(function(d) { return d.data.name; });

	  var node = g.selectAll("circle,text");
	  svg.on("click", function() { zoom(root); });
	  zoomTo([root.x, root.y, root.r * 2 + 25]);

	  function zoom(d) {
		var focus0 = focus; focus = d;

		var transition = d3.transition()
			.duration(d3.event.altKey ? 7500 : 750)
			.tween("zoom", function(d) {
			  var i = d3.interpolateZoom(view, [focus.x, focus.y, focus.r * 2 + 25]);
			  return function(t) { zoomTo(i(t)); };
			});

		transition.selectAll("text")
		  .filter(function(d) { return d.parent === focus || this.style.display === "inline"; })
			.style("fill-opacity", function(d) { return d.parent === focus ? 1 : 0; })
			.on("start", function(d) { if (d.parent === focus) this.style.display = "inline"; })
			.on("end", function(d) { if (d.parent !== focus) this.style.display = "none"; });
	  }

	  function zoomTo(v) {
		var k = diameter / v[2]; view = v;
		node.attr("transform", function(d) { return "translate(" + (d.x - v[0]) * k + "," + (d.y - v[1]) * k + ")"; });
		circle.attr("r", function(d) { return d.r * k; });
	  }
	});
</script>