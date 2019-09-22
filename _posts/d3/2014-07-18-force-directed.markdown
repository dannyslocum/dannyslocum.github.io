---
layout: visual
title: D3 Force Directed
caption: Risus commodo viverra maecenas accumsan lacus vel facilisis. Suscipit adipiscing bibendum estultricies integer quis auctor elit sed.
date: 2014-07-18

img: portfolio/force-directed.PNG
css: /assets/css/force-directed.css
data: /assets/data/miserables.json
categories: [d3]
tags: [d3]

description: 
---
<link rel="stylesheet" href="{{ page.css }}">
<script src="https://d3js.org/d3.v5.min.js"></script>

<script>

	var width = window.innerWidth,
		height = window.innerHeight,
		svg = d3.select("#visual").append("svg").attr("class", "mx-auto").attr("width", width).attr("height", height),
		g = svg.append("g"),
		color = d3.scaleOrdinal(d3.schemeDark2),
		simulation = d3.forceSimulation()
			.force("link", d3.forceLink().distance(10).strength(.5))
			.force("charge", d3.forceManyBody().strength(-50))
			.force("center", d3.forceCenter(width / 2, height / 2))
			.force("collide", d3.forceCollide().radius(2));

	d3.json("{{ page.data }}").then(function(graph) {
//	d3.json("{{ page.data }}", function(error, graph) {

	  var nodes = graph.nodes,
		  nodeById = d3.map(nodes, function(d) { return d.id; }),
		  links = graph.links,
		  bilinks = [];

	  links.forEach(function(link) {
		var s = link.source = nodeById.get(link.source),
			t = link.target = nodeById.get(link.target),
			i = {label: "label"}; // intermediate node
		nodes.push(i);
		links.push({source: s, target: i}, {source: i, target: t});
		bilinks.push([s, i, t]);
	  });

	  g.append("defs")
		 .append("marker")
			.attr("id", "arrow")
			.attr("viewBox", "0 -3 10 10")
			.attr("refX", 15)
			.attr("refY", 0)
			.attr("markerWidth", 8)
			.attr("markerHeight", 8)
			.attr("orient", "auto")
			  .append("svg:path")
				.attr("d", "M0,-5L10,0L0,5"); 
		  
	  link = g.selectAll(".link")
		.data(bilinks)
		.enter().append("path")
			.attr("class", "link")
			.attr('marker-end','url(#arrow)')
			.attr('id', function (d, i) {return 'edgepath' + i})
			.style("pointer-events", "none");

	  edgelabels = g.selectAll(".edgelabel")
		.data(bilinks)
		.enter().append('text')
			.style("pointer-events", "none")
			.style("font-size", 8)
			.style("opacity", 0)
			.style("fill", "grey");

	  edgelabels
		.append('textPath')
			.attr('xlink:href', function (d, i) {return '#edgepath' + i})
			.style("text-anchor", "middle")
			.style("pointer-events", "none")
			.attr("startOffset", "50%")
			.text(function(d,i){ return d[1].label + i; });	

	  var node = g.selectAll(".node")
		.data(nodes.filter(function(d) { return d.id; }))
		.enter().append("g")
		   .call(d3.drag()
			  .on("start", dragstarted)
			  .on("drag", dragged)
			  .on("end", dragended));
			  
	/*	
	  node.append("svg:image")
		.attr("xlink:href", function() { return "/img/portfolio/cabin.png"})
		.attr("x", -25)
		.attr("y", -25)
		.attr("height", 50)
		.attr("width", 50);
	*/
		
	  nodePath = node.append("path")
		.attr("class", "node")
		.attr("fill", function(d) { return color(d.group); })
		.attr("d", d3.symbol().size(64).type(d3.symbolDiamond))
		.on("mouseover, pointerover", mouseover)
		.on("mouseout, pointerout", mouseout);
		
	  nodeText = node.append("text")
		.attr("x", 12)
		.attr("dy", "0.35em")
		.style("opacity", 0)
		.style("pointer-events", "none")
		.text(function(d) { return d.id; });

	  var zoom_handler = d3.zoom().on("zoom", zoom_actions);
	  zoom_handler(svg); 
		
	  simulation
		  .nodes(nodes)
		  .on("tick", ticked);

	  simulation.force("link")
		  .links(links);

	  for (var i = 0; i < 500; ++i) simulation.tick();
	  
	  function mouseover(d) {
		var node_highlight = [d.id];
		link
			.style("opacity",0.1)
			.filter(function(l) { 
				check = (l[0].id == d.id || l[2].id == d.id);
				if (check) { node_highlight.push(l[0].id); node_highlight.push(l[2].id); }
				return check; })
			.style("opacity",1);
		edgelabels		
			.style("opacity",0)
			.filter(function(l) { return (l[0].id == d.id || l[2].id == d.id); })
			.style("opacity",1);
		nodePath		
			.style("opacity",0.1)
			.filter(function(l) { return (node_highlight.indexOf(l.id) > -1); })
			.style("opacity",1);	
		nodeText		
			.style("opacity",0)
			.filter(function(l) { return (node_highlight.indexOf(l.id) > -1); })
			.style("opacity",1);
	  }  
	  function mouseout(d) {
		link.style("opacity",1);
		edgelabels.style("opacity",0);
		nodePath.style("opacity",1);	
		nodeText.style("opacity",0);
	  }
	  function ticked() { link.attr("d", positionLink); node.attr("transform", positionNode); }
	  function zoom_actions(){ g.attr("transform", d3.event.transform) }
	});

	function positionLink(d) { return "M" + d[0].x + "," + d[0].y + "S" + d[1].x + "," + d[1].y + " " + d[2].x + "," + d[2].y; }
	function positionNode(d) { return "translate(" + d.x + "," + d.y + ")"; }
	function dragstarted(d) { if (!d3.event.active) simulation.alphaTarget(0.3).restart(); d.fx = d.x, d.fy = d.y; }
	function dragged(d) { d.fx = d3.event.x, d.fy = d3.event.y; }
	function dragended(d) { if (!d3.event.active) simulation.alphaTarget(0); d.fx = null, d.fy = null; }

</script>