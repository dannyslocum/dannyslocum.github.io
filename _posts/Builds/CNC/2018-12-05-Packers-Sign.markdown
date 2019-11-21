---
layout: blog
title: Wood Packers Sign (w/ Epoxy Infill)
caption: Using raster images from the web, I created and carved out a replicated model of Wisconsin and the Packers logo. This was then filled with a white epoxy for the Packers 'G' to mimic the logo and give it a unique look. These steps can be easily replicated with a CNC machine on you're own logos or images.
date: 2014-07-18

img: Packers_Sign/finished_product.png
categories: [Builds]
tags: [CNC]

---

I recently completed a build for a friend of mine, which is a large Green Bay Packers / Wisconsin sign. I was able to create this with a simple raster image of the Packers logo plus an outline of Wisconsin, and the steps to do this are very easy to replicate. This was also the first time I used epoxy for one of my designs, and I think the end results came out really well. If you haven't used epoxy before, it's definitely worth trying out as a part of your projects!

### 0. Getting Started
##### Materials:
- 2x4 sheet of plywood
- Yellow spray paint
- Painters tape 
- Minwax Wood Finish
- Rag
- Drop cloth
- Painters tape
- Respiratory mask
- [Epoxy](https://www.amazon.com/Crystal-Clear-Table-Coating-Tabletop/dp/B01LYK2NAG/ref=sxts_sxwds-bia?keywords=epoxy&pd_rd_i=B01LYK2NAG&pd_rd_r=21374850-59a9-425e-a204-e1b0a620da7b&pd_rd_w=9pcAA&pd_rd_wg=SNdS0&pf_rd_p=1cb3f32a-ccfd-479b-8a13-b22f56c942c6&pf_rd_r=TKFJ36FF7S85RPFA30BS&psc=1&qid=1574306508)
- [Epoxy Colored Powder](https://www.amazon.com/gp/product/B071SB48Z7/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1)
- Large latex gloves
- Safety glasses

##### Tools:
- [CNC Machine](https://www.v1engineering.com/the-lowrider2-cnc/) w/
    - 45 degree or finer router bit
    - 1/8 Upcut router bit
- Orbital Sander...OR...Sand Paper
- Blow Torch...OR...Heat gun...OR...[toothpick+patience](https://www.artresin.com/blogs/artresin/how-to-use-a-torch-with-resin)

##### Software:
- Fusion 360 (or equivalent CAM software)
- Inkscape (or equivalent raster -> vector software)

### 1. Create Design
I first found a high contrast image of [Wisconsin](https://upload.wikimedia.org/wikipedia/en/6/68/Wisconsin_outline.JPG) and the [Green Bay Packers logo](https://upload.wikimedia.org/wikipedia/commons/thumb/5/50/Green_Bay_Packers_logo.svg/1280px-Green_Bay_Packers_logo.svg.png). After copy and pasting these images into Inkscape, they can easily be converted into into vectorized images using the 'Trace bitmap...' feature (<kbd>Path</kbd> tab -> <kbd>Trace bitmap...</kbd>). This opens a sidebar for tweaking various trace settings. In this instance, I used the single scan Brightness cutoff" for the Wisconsin outline and the single scan "Color quantization" for the Packers logo. The brightness cutoff can be adjusted until it shows a quality output, but the color quantization will be more tricky. If you have a simple logo with a set number of colors, you should set the value to equal or less than the total colors in the image. With the Packers logo, I used the total color count of the logo (black, green, yellow, and white). If you have an image with no defined set of colors, this step can be a lot more difficult. You can still accomplish this step, but in a lot of cases the output won't be exactly what you want. 

<div class="row">
    <div style="text-align: center" class="my-3 col-lg-4 col-md-6">
        <img src="\assets\img\posts\Packers_Sign\wisconsin.png">
    </div>
    <div style="text-align: center" class="my-3 col-lg-4 col-md-6">
        <img src="\assets\img\posts\Packers_Sign\wisconsin_traced.png">
    </div>
    <div style="text-align: center" class="my-3 col-lg-4 col-md-6">
        <img src="\assets\img\posts\Packers_Sign\both_traced.png">
    </div>
</div>

These vector images were adjusted slightly in order to get them ready for manufacturing. The Wisconsin image had some sections that appeared like islands after tracing, and there were two lines representing the state's border. This is due to the 'Trace bitmap' attempting to render the image exactly. A line, when represented on an image, is actually two lines in a vector image. This is the case since it's preserving the line width of the image. The easy way to fix this was to just remove one of these lines.

```Hint: Double click oon the vector image or choose the select by node option. Hold ```<kbd>CNTL</kbd>```, hover over one of the nodes on a line you'd like to remove, and then use the scroll bar. This will select the neighboring nodes for each scroll. For larger lines, you'll need to scroll a decent amount.```

For the Packers logo, the same method was applied. All of the lines for the rectangular outer frame were removed, leaving just the "G" and the outer ring. This was then scaled in order to fit inside the Wisconsin vector. The Wisconsin vector was sized so that the it was just shy of 24 inches in the Y direction. My goal was to ensure this could be carved with a 2x4 foot birch board.

I used the basic Inkscape font in order to put text on the design. I chose "Stencil" in this case since I thought it would look good when carved out on the CNC Machine. Typing out one section with "Green Bay" and another section with "Packers". This was also scaled in order to fit on the Wisconsin image, and was converted to a vector path using <kbd>Path</kbd> -> <kbd>Object to path</kbd>. This was saved as an _SVG_ and the design was then complete!

<div class="row">
    <div style="text-align: center" class="my-3 col-lg-4 col-md-6">
        <img src="\assets\img\posts\Packers_Sign\wisconsin_twoline.png">
    </div>
    <div style="text-align: center" class="my-3 col-lg-4 col-md-6">
        <img src="\assets\img\posts\Packers_Sign\wisconsin_oneline.png">
    </div>
    <div style="text-align: center" class="my-3 col-lg-4 col-md-6">
        <img src="\assets\img\posts\Packers_Sign\logo_adjusted.png">
    </div>
    <div style="text-align: center" class="my-3 col-lg-4 col-md-6">
        <img src="\assets\img\posts\Packers_Sign\logo_overlay.png">
    </div>
    <div style="text-align: center" class="my-3 col-lg-4 col-md-6">
        <img src="\assets\img\posts\Packers_Sign\text_to_path.png">
    </div>
    <div style="text-align: center" class="my-3 col-lg-4 col-md-6">
        <img src="\assets\img\posts\Packers_Sign\sign_inkscape.png">
    </div>
    <div style="text-align: center" class="my-3">
        <img src="\assets\img\posts\Packers_Sign\vectorized_compare.png">
    </div>
</div>

### 2. Generate Toolpaths
The first thing to do in Fusion 360 is inserting the _SVG_ (INSERT -> Insert SVG). And that's it! You can create a 3D model if you'd like to to test coloring and ensure you have the look you want, but manufacturing the part can be done all with this 2D model.

Change the workspace from DESIGN to MANUFACTURE. First create a new setup, setting the X,Y,Z axis to the exact dimensions of your board. Adjust the 'Model Position' for the Z axis to ensure the 2D design is on the top of the stock. Change the Work Coordinate System to be one of the corners of your stock part as well to make setting the start position much easier when manufacturing the part.

The first toolpath I generated was the text engravings using the 2D 'Engrave'. For this I used a 0.5 inch - 45 degree bit. The settings were set to the default for my bit, which engraves into the wood 0.25 inches.

The second toolpath is to cut a pocket for the 'G' using the '2D Pocket'. I selected my 0.125 inch upcarve bit and a pocket depth of 0.15 inches. This was chosen so it wouldn't cause the corners to be drastically rounded and it could be carved quickly. The pocket depth was selected to ensure it had enough for the epoxy to fill without wasting too much material, while allowing enough depth to ensure it wasnt translucent. The cut depth for my bit was set to a third of the bit diameter, so 0.0416 inches. This takes 4 passes to complete.

The last toolpath is the outer contour using the '2D Contour'. I kept using the 0.125 inch upcarve bit to reduce the amount of bit changes. The contour depth was set to be the bottom of the stock. I usually take off an additional 0.05 inches to ensure it cuts the material completely through without any hiccups. If you don't intend on using double sided tape of another method to secure the wood to your platform, make sure to add some tabs.

The last thing to do is save these paths off as G-code by right clicking and selecting 'Post Process'. I saved mine off as two separate files, one with the 45 degree engrave, and another with the 0.125 inch pocket and contour.

<div class="row">
    <div style="text-align: center" class="my-3 col-lg-4 col-md-6">
        <img src="\assets\img\posts\Packers_Sign\fusion_svg_import.png">
    </div>
    <div style="text-align: center" class="my-3 col-lg-4 col-md-6">
        <img src="\assets\img\posts\Packers_Sign\fusion_setup.png">
    </div>
    <div style="text-align: center" class="my-3 col-lg-4 col-md-6">
        <img src="\assets\img\posts\Packers_Sign\fusion_engrave.png">
    </div>
    <div style="text-align: center" class="my-3 col-lg-4 col-md-6">
        <img src="\assets\img\posts\Packers_Sign\fusion_pocket.png">
    </div>
    <div style="text-align: center" class="my-3 col-lg-4 col-md-6">
        <img src="\assets\img\posts\Packers_Sign\fusion_contour.png">
    </div>
    <div style="text-align: center" class="my-3 col-lg-4 col-md-6">
        <img src="\assets\img\posts\Packers_Sign\toolpath.gif">
    </div>
</div>

### 3. Make the Cuts
We can finally cut out the design. I'm using the V1 Engineering Low Rider CNC Machine for mine (link provided above). I screw the board into my CNC table, insert my 45 degree bit, set the start position to where I had it in the Fusion 360 design, and start off the first engrave toolpath. Once complete, I switch bits and re-align the z-axis start position, and then start up the pocket and contour toolpath. Voila! I chiseled out the tabs and sanded the outer area smooth and cleaned up some imperfections in the engravings. Now onto the final touches.

<div class="row">
    <div style="text-align: center" class="my-3 col-md-6">
        <img src="\assets\img\posts\Packers_Sign\carve_engrave.gif">
    </div>
    <div style="text-align: center" class="my-3 col-md-6">
        <img src="\assets\img\posts\Packers_Sign\cnc_after.png">
    </div>
</div>

### 4. Finish the build
##### Paint
I tape the surrounding areas of the engravings to help when cleaning up the paint on top of the sign. By sanding the top of the piece after painting, it will leave just the paint inside the engravings. I went with a yellow paint to match the Packers colors (and because I had some extra on hand).
<div class="row">
    <div style="text-align: center" class="my-3 col-12">
        <img src="\assets\img\posts\Packers_Sign\paint.png">
    </div>
</div>

##### Epoxy
The next step was to mix the two part epoxy and fill in the 'G' (the materials I used can all be found in the list at the beginning of the post). Since this was my first time using epoxy in this way, I ran some tests before hand. I was debating between spray painting the 'G' with a white color while adding a clear epoxy to create some depth, or adding some epoxy powder to create a shiny focal point. The later appealed a little more to me so this was the option I stuck with. I didn't measure the amount of powder to an exact amount when mixing the epoxy, but I just added small increments until I got the opacity I was looking for. I used a butane torch to remove the bubbles in the epoxy for this case, but a heat gun or even a toothpick can be used here. The torch worked extremely well and quick in my case. I really like how this turned out. The epoxy has a very unique look to it and makes the 'G' really pop out. I'll be experimenting with epoxy a lot more in future builds. 
<div class="row">
    <div style="text-align: center" class="my-3 col-lg-4 col-md-6">
        <img src="\assets\img\posts\Packers_Sign\epoxy_start.png">
    </div>
    <div style="text-align: center" class="my-3 col-lg-4 col-md-6">
        <img src="\assets\img\posts\Packers_Sign\epoxy_after.png">
    </div>
    <div style="text-align: center" class="my-3 col-lg-4 col-md-6">
        <img src="\assets\img\posts\Packers_Sign\epoxy.gif">
    </div>
</div>

##### Stain
The top of the sign was a 2x4 foot birch wood, which I stained using a dark mahogany to help make the paint and epoxy even more. This was the easiest finishing step of the three. The only thing I had to do was ensure the stain stayed off of the epoxy and the engravings.
<div class="row">
    <div style="text-align: center" class="my-3 col-12">
        <img src="\assets\img\posts\Packers_Sign\finished_product.png">
    </div>
</div>

The final product here came out really well and this method can easily be replicated to create your own wall art or sign. If you don't have a CNC machine but are interested in building one, there are a lot of relatively cheap options out there. Makerspaces also offer very inexpensive opportunities to use these machines. If you have any questions about the process, feel free to [contact me](/#contact)!
