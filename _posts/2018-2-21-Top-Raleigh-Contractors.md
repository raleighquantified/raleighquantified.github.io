---
layout: post
title:  "The Top 100 Contractors in Raleigh (According to Permit Data)"
---

![_top100.yml]({{ site.baseurl }}/images/bokeh_plot (4).png)

<h2>A Few Caveats</h2>
As regular readers know, I've been working with this dataset for a while now. In past posts (here, here, and here), I was looking mostly at general trends in Raleigh construction, and I trusted that the odd error in the data or flaw in my analysis wouldn't skew my findings that much. A good approximation was good enough. 

In this case, however, I'll be mentioning specific companies by name, so I want to be explicit about what sort of claims I am --and am not-- making.

First of all, the dataset I'm using is a collection of permits available at raleigh open data. There isn't a one-to-one mapping between permits and completed buildings. Some planned projects are never completed at all. 

Also, I suspect that there are some duplicates in this dataset, though they aren't the sort of duplicates that can easily be identified and removed programmatically. And the dataset is just too large to do much of anything manually. 

Additionally, these permits were filed in the city of Raleigh, and many of these companies operate outside of the city as well. In short, any inferences one might make about a contractor's financials based on this data are just that: inferences.

<h2>Introduction</h2>
This analysis was trickier than my previous posts in that it required me to completely restructure the data. In the original dataset, each permit was its own row, and information on different contractors merely features of those rows.

Though it wasn't technically difficult to derive information about contractors from permit data, I had to play with the data for a while to decide what I actually wanted to know about individual contractors.

I'm not convinced that I identified every potentially interesting feature, but I do think I found the most important ones. They include:

**Project Count:**

The number of permits in which a company as listed as the contractor. 

**Total/Aggregate Costs of Planned Projects:** 

The sum of the estimated project costs of the permits in which a company is listed as the contractor. The caveats I've mentioned notwithstanding, this feature is meant to serve as a proxy for total gross revenue from all projects in Raleigh. 

**Primary Permit Class:** 

Each permit has a feature called "Permit Class Mapped," which tells you whether a planned project is residential or non-residential. For the purposes of this post, a contractor's Primary Permit Class is the mode permit class for all of that contractor's projects. 

Keep in mind that this doesn't necessarily tell you where where the majority of a contractor's revenue is coming from. For instance, a contractor that built two houses for $150,000 dollars each, and a large commercial building for $1,000,000, would be listed as residential, even though the majority of its revenue came from non-residential projects.

Still, I think this feature is a "good enough" signal of a contractor's activities.

First, let's take a look at Raleigh contractors in general: 

<h2>Project Count</h2>

The mean project count was just under 8, which is way lower than I would have expected. Even stranger, half of contractors are listed in just one permit, and 75% are listed in three or fewer. 

![_projectcount.yml]({{ site.baseurl }}/images/projectcount.png)

There are a few explanations for this, and determining how much weight to assign to each explanation would take another project altother, but let's go over them in outline: 

**1. Non-residential contractors typically work on fewer, larger projects than their residential counterparts**

It's possible that commercial contractors are bringing down the average some, but most contractors seem to be primarily residential, so there's no way this is the primary driver of the low average project count you observe in the data.

**2. Some contractors do much of their business outside of the city**

Unfortunately, only 46% of contractors in my sample have their home city on record. Of those that do, 38% are based in Raleigh. 

The most frequently appearing contractor cities are located nearby, but it is possible that some contractors are mostly operating outside of the city, though, once again, I don't think this is the primary factor.

**3. Some contractors work mostly as subcontractors**

Each permit record only lists the general contractor overseeing the project. It seems possible that many of these contractors mostly operate as subcontractors.

**4. Some contractors work primarily on smaller jobs that don't require a permit**

[According to the city](https://www.raleighnc.gov/business/content/PlanDev/Articles/DevServ/Homeowner/WhenIsAPermitRequired.html), a permit isn't required for all home improvement projects.

<h2>The Most Prolific Constractors</h2>

The most prolific contractors are massive outliers, appearing in thousands of permit records a piece. 

![_projectcount.yml]({{ site.baseurl }}/images/prolific_contractors.png)

Not surprisingly, these are all residential contractors. 

<h2>Aggregate Project Costs</h2>

The distribution of Aggregate Project Costs is similar to that of Project Count. In this case, however, the difference between the median and mean values (eighteen grand vs a million and a half) is far more glaring. 

![_total.yml]({{ site.baseurl }}/images/total_dist.png)

<h2>Top Contractors by Aggregate Project Costs</h2>

Even more interestingly, compare these companies with the contractors we were looking at a moment ago:

![_total_top.yml]({{ site.baseurl }}/images/total_top.png)

While there's some overlap between the two groups, non-residential contractors are overrepresented here, whereas they were completely absent from the other visualization. 

The explanation is actually pretty simple: You have to build a lot of houses to make as much as you could by building a single hospital or government building. 

For additional context, check out the interactive below. 


<html lang="en">
  
  <head>
    
      <meta charset="utf-8">
      <title>test</title>
      
      
        
          
        <link rel="stylesheet" href="https://cdn.pydata.org/bokeh/release/bokeh-1.0.4.min.css" type="text/css" />
        
        
          
        <script type="text/javascript" src="https://cdn.pydata.org/bokeh/release/bokeh-1.0.4.min.js"></script>
        <script type="text/javascript">
            Bokeh.set_log_level("info");
        </script>
        
      
      
    
  </head>
  
  
  <body>
    
      
        
          
          
            
              <div class="bk-root" id="bbbb8b24-8346-4b18-b590-10ddc322b66b" data-root-id="2559"></div>
            
          
        
      
      
        <script type="application/json" id="2703">
          {"792430e0-aac8-455c-83eb-db97f0bc1c50":{"roots":{"references":[{"attributes":{"plot":{"id":"2559","subtype":"Figure","type":"Plot"},"ticker":{"id":"2570","type":"BasicTicker"}},"id":"2573","type":"Grid"},{"attributes":{"fill_alpha":{"value":0.1},"fill_color":{"value":"#1f77b4"},"line_alpha":{"value":0.1},"line_color":{"value":"#1f77b4"},"line_dash":[5,3],"size":{"units":"screen","value":10},"x":{"field":"PROJECT_COUNT"},"y":{"field":"TOTAL"}},"id":"2598","type":"Circle"},{"attributes":{"items":[{"id":"2608","type":"LegendItem"},{"id":"2622","type":"LegendItem"}],"plot":{"id":"2559","subtype":"Figure","type":"Plot"}},"id":"2607","type":"Legend"},{"attributes":{},"id":"2584","type":"HelpTool"},{"attributes":{"callback":null},"id":"2561","type":"DataRange1d"},{"attributes":{"active_drag":"auto","active_inspect":"auto","active_multi":null,"active_scroll":"auto","active_tap":"auto","tools":[{"id":"2579","type":"PanTool"},{"id":"2580","type":"WheelZoomTool"},{"id":"2581","type":"BoxZoomTool"},{"id":"2582","type":"SaveTool"},{"id":"2583","type":"ResetTool"},{"id":"2584","type":"HelpTool"},{"id":"2594","type":"HoverTool"}]},"id":"2585","type":"Toolbar"},{"attributes":{},"id":"2632","type":"UnionRenderers"},{"attributes":{"plot":null,"text":"The Top 100 Contractors in Raleigh (According to Permit Data)"},"id":"2558","type":"Title"},{"attributes":{"data_source":{"id":"2557","type":"ColumnDataSource"},"glyph":{"id":"2610","type":"Circle"},"hover_glyph":null,"muted_glyph":null,"nonselection_glyph":{"id":"2611","type":"Circle"},"selection_glyph":null,"view":{"id":"2613","type":"CDSView"}},"id":"2612","type":"GlyphRenderer"},{"attributes":{"fill_alpha":{"value":0.6},"fill_color":{"field":"color"},"line_color":{"field":"color"},"line_dash":[5,3],"size":{"units":"screen","value":10},"x":{"field":"PROJECT_COUNT"},"y":{"field":"TOTAL"}},"id":"2597","type":"Circle"},{"attributes":{"source":{"id":"2557","type":"ColumnDataSource"}},"id":"2613","type":"CDSView"},{"attributes":{},"id":"2631","type":"Selection"},{"attributes":{"axis_label":"Aggregate Costs of Planned Projects (in Millions)","formatter":{"id":"2605","type":"BasicTickFormatter"},"plot":{"id":"2559","subtype":"Figure","type":"Plot"},"ticker":{"id":"2575","type":"BasicTicker"}},"id":"2574","type":"LinearAxis"},{"attributes":{"axis_label":"Number of Planned Projects","formatter":{"id":"2603","type":"BasicTickFormatter"},"plot":{"id":"2559","subtype":"Figure","type":"Plot"},"ticker":{"id":"2570","type":"BasicTicker"}},"id":"2569","type":"LinearAxis"},{"attributes":{},"id":"2580","type":"WheelZoomTool"},{"attributes":{"callback":null,"tooltips":[["Company name","@NAME"],["Project Count","@PROJECT_COUNT"],["Aggregate Costs of Planned Projects (in Millions)","@TOTAL"]]},"id":"2594","type":"HoverTool"},{"attributes":{},"id":"2575","type":"BasicTicker"},{"attributes":{"source":{"id":"2556","type":"ColumnDataSource"}},"id":"2600","type":"CDSView"},{"attributes":{},"id":"2603","type":"BasicTickFormatter"},{"attributes":{"fill_alpha":{"value":0.1},"fill_color":{"value":"#1f77b4"},"line_alpha":{"value":0.1},"line_color":{"value":"#1f77b4"},"line_dash":[5,3],"size":{"units":"screen","value":10},"x":{"field":"PROJECT_COUNT"},"y":{"field":"TOTAL"}},"id":"2611","type":"Circle"},{"attributes":{"label":{"value":"Non-Residential"},"renderers":[{"id":"2599","type":"GlyphRenderer"}]},"id":"2608","type":"LegendItem"},{"attributes":{"data_source":{"id":"2556","type":"ColumnDataSource"},"glyph":{"id":"2597","type":"Circle"},"hover_glyph":null,"muted_glyph":null,"nonselection_glyph":{"id":"2598","type":"Circle"},"selection_glyph":null,"view":{"id":"2600","type":"CDSView"}},"id":"2599","type":"GlyphRenderer"},{"attributes":{},"id":"2605","type":"BasicTickFormatter"},{"attributes":{},"id":"2620","type":"Selection"},{"attributes":{"callback":null,"data":{"AVERAGECOST":{"__ndarray__":"aYMD/P7fAEFovkBZblIRQS1kIQu3xCpBs/YBQR+XAUEOqQnGKSY+Qc752hDzrgJBAAAAqE4EQEGLWuK1zjsGQXbWkiiuRAJBRGqC8QhDTEFKsySihz0LQa5jFOej/ydBIzdyI7M6Q0HY6F2R20AoQSNoOCnedCNBSVbhnKisF0EVZhPHfh31QB+F61H3eDRBbkelifySEEF2r3vdyKY2QSC9dr96jfdAuClGDa/LEkEzrvOtsuz8QBphuSfGbf9A+YbCZ3tOB0EilxUDTab1QLmZz6a8XgBBlJOTk1Og/kC9rrYntcP+QBEREdH1xlpB1ZPx21uqNUHx5BZPQPMHQcZNmN9F7zBBBbKs+l3D/0BxukxxiqMMQfBs1HcpFzhBWVEaH0UKBUEXB4bLgboIQd1Q2zSaePtAV7hxGRu2AUGMLrroZGr7QLvSGQXwF/RAJUmShD66QUEAAADw4P1OQfmKr/j/xAtBAAAAAG4KjkGrqqqqGvkAQfZlX/YFBfpAYOeUBCD4AEERERERSa4CQQ4VC5qrZQ9BAAAAAMHkFkEiIiIigzc9QQlFKELLcANBPDw8PG9MKUGdgpdTXmcRQSEmVxBb0BFB9Qd6pAxREUExDMOwsK4jQTI4H4Mx8jNBQgghhC1ZOkEAAAB4CDQ5QdFFF12W8jdB","dtype":"float64","shape":[63]},"MAXCOST":{"__ndarray__":"AAAAgCV7R0EAAADAdBxdQQAAADQrAZBBAAAAAMRGF0EAAAAAZtxXQQAAAAB2cTlBAAAAIKqumEEAAAAAgHYdQQAAAAAQDhlBAAAAGJUXhkEAAAAA4CgqQQAAAABuCl5BAAAAAPCzikEAAAAA9AZ0QQAAAACGj2xBAAAAADicfEEAAAAALI8yQQAAAADasXRBAAAAABBQJEEAAABAAAVtQQAAAADAXBVBAAAAQK2GWEEAAAAAgE8yQQAAAADgjBpBAAAAALiMIEEAAAAAKGMvQQAAAAB0EhFBAAAAACCZGUEAAAAAGGEcQQAAAAC2qmpBAAAAAByhZUEAAAAAGOgjQQAAAIByJGBBAAAAALzbHEEAAAAAVCseQQAAAKAFJnNBAAAAAKZEIUEAAAAAgDEXQQAAAAAwjEFBAAAAACRuH0EAAAAA2JcnQQAAAADEJjBBAAAAMFCbh0EAAACAnqFtQQAAAACguCFBAAAAAG4KjkEAAAAAgE8yQQAAAADAIA9BAAAAAJASEkEAAAAAFUhLQQAAAADgyDBBAAAAACApK0EAAADASltSQQAAAAAAjg1BAAAAkI75d0EAAAAA4EIuQQAAAAD84VJBAAAAAKAONUEAAAAAEFdBQQAAAAA4nGxBAAAA4PS5bEEAAAAAsctOQQAAAIBLg3BB","dtype":"float64","shape":[63]},"MEDIANCOST":{"__ndarray__":"AAAAACBh+kAAAAAAgMAEQQAAAAAw9/5AAAAAAOCm/kAAAAAAgIQuQQAAAACAZgBBAAAAAFDb+UAAAAAAyDABQQAAAAAAxf9AAAAAADowNUEAAAAAgOMEQQAAAABgcuRAAAAAAMAQ3EAAAAAAgLb+QAAAAADA0QpBAAAAAABAn0AAAAAAgCPxQAAAAACuZRtBAAAAAIiRDUEAAAAAetItQQAAAAAA6/RAAAAAADAt9kAAAAAAIEX5QAAAAAAAw/tAAAAAAFiMBUEAAAAAAJTxQAAAAADwq/9AAAAAAEAS90AAAAAAANX7QAAAAEC89VxBAAAAADFUNkEAAAAAAGoIQQAAAAAAbedAAAAAAOAF9EAAAAAAgBMMQQAAAAAAahhBAAAAAIBxAUEAAAAAYHYIQQAAAAAARu5AAAAAAEBG/0AAAAAAIHb7QAAAAAAAiPNAAAAAAFDA6EAAAAAAx8lCQQAAAADQLQZBAAAAAG4KjkEAAAAAABfxQAAAAACAbvhAAAAAACAHAEEAAAAAYP36QAAAAACATwJBAAAAAGDjFkEAAACAe3tAQQAAAACAswJBAAAAAACI80AAAAAAYDwNQQAAAABoeQJBAAAAADBADUEAAAAAACriQAAAAAA9NjVBAAAAACjoHkEAAAAAPMY8QQAAAAD6ayRB","dtype":"float64","shape":[63]},"MINCOST":{"__ndarray__":"AAAAAAAA8D8AAAAAAAAAAAAAAAAAAPA/AAAAAAAAWUAAAAAAAADwPwAAAAAAAPA/AAAAAAD0qkAAAAAAAAAAAAAAAAAAQH9AAAAAAABAj0AAAAAAAEB/QAAAAAAAAAAAAAAAAABAf0AAAAAAAAAAAAAAAAAAlLFAAAAAAABAn0AAAAAAAADwPwAAAAAAAAAAAAAAAAAAAAAAAAAAAAB5QAAAAAAAhKVAAAAAAAAA8D8AAAAAAABZQAAAAAAAAFlAAAAAAAAAAAAAAAAAAIBWQAAAAAAAAFlAAAAAAABAf0AAAAAAAAAAAAAAAAAATM1AAAAAAAACwkAAAAAAAIBoQAAAAAAAcJdAAAAAAAAAAAAAAAAAAAAAAAAAAAAAhJBAAAAAAAAgjEAAAAAAAHDHQAAAAAAAAAAAAAAAAABCqEAAAAAAAADwPwAAAAAAAAAAAAAAAACEkkAAAAAAAIizQAAAAAAAAAAAAAAAAG4KjkEAAAAAAAAAAAAAAAAAWLtAAAAAAABAj0AAAAAAAHCXQAAAAAAAAAAAAAAAAABwx0AAAAAAAEzNQAAAAAAA4J9AAAAAAAAA8D8AAAAAAEB/QAAAAAAAwHJAAAAAAAAAAAAAAAAAAECPQAAAAAAAQJ9AAAAAAACgZEAAAAAAAFirQAAAAAAAiMNA","dtype":"float64","shape":[63]},"NAME":["PULTE HOME CORPORATION","TOLL BROTHERS OF NORTH CAROLIN","CHOATE CONSTRUCTION COMPANY","CENTEX HOMES","THE RESOLUTE BUILDING COMPANY","BEAZER HOMES CORP, T/A","METCON, INC","DR HORTON-TORREY HOMES INC","KB HOMES OF RALEIGH-DURHAM, LL","LANDMARK URBAN CONSTRUCTION RA","M I HOMES OF RALEIGH","HAROLD K. JORDAN &amp; COMPANY","FORTUNE-JOHNSON, INC","J. M.THOMPSON COMPANY","BOVIS LEND LEASE","TCR N.C. CONSTRUCTION I, LP","WESTFIELD HOMES OF NC","SAMET CORPORATION","ASHTON RALEIGH RESIDENTIAL, LL","GREYSTAR DEVELOPMENT &amp; CONSTRU","COLONY HOMES LLC","MCDONALD-YORK CONSTRUCTION","STANDARD PACIFIC OF THE CAROLI","PERRY BUILDERS","CHESAPEAKE HOMES OF NC, INC.","NC HOMES  LLC","HOMELIFE COMMUNITIES OF RALEIG","MURDOCK GANNON CONSTRUCTION, I","LENNAR CAROLINAS LLC","W P EAST BUILDERS,  LLC","CAROLINA MULTI FAMILY CONSTRUC","JOHN WIELAND HOMES","C.F. EVANS &amp; COMPANY, INC","DAN RYAN BUILDERS-NORTH CAROLI","THE DREES HOMES COMPANY","ADOLFSON &amp; PETERSON CONSTRUCTI","K. HOVNANIAN HOMES OF NORTH CA","WADE JURNEY HOMES, INC","SIGMON CONSTRUCTION","1ST AMERICAN BUILDERS LLC","JORDAN'S CONSTRUCTION, INC.","FRED SMITH COMPANY","TRG BUILDERS, LLC","CF EVANS CONSTRUCTION","ROYAL OAKS BUILDING GROUP, LLC","HARDIN CONSTRUCTION GROUP","GREG PAUL BUILDERS, INC.","ANDERSON HOMES, INC","FORTIS HOMES, INC.","COMSTOCK HOMES OF RALEIGH, LLC","LEGACY CUSTOM HOMES","PREMIERE HOMES  II, INC","WESTCHASE CONSTRUCTION LTD.","ST. LAWRENCE HOMES","BOYLAN DEVELOPMENT COMPANY","HOMES  BY DICKERSON, INC.","EVERGREEN CONSTRUCTION COMPANY","L AND L OF RALEIGH","FAIRMARK DEVELOPMENT LTD PARTN","JPI APARTMENT CONSTRUCTION LP","WEAVER COOKE CONSTRUCTION, LLC","CROSLAND CONTRACTORS, A NORTH","THOMAS CONSTRUCTION GROUP, LLC"],"NUMBER_OF_NON_RESIDENTIAL":[4,26,270,4,53,1,38,2,1,2,11,14,9,86,57,13,5,43,7,12,3,193,4,9,6,12,2,0,5,0,2,7,13,0,2,11,1,0,119,2,7,69,1,6,5,0,42,0,0,0,8,3,1,0,32,0,6,0,0,7,8,2,2],"NUMBER_OF_RESIDENTIAL":[3785,1781,282,2473,106,1776,74,1276,1324,51,840,212,56,113,179,346,1605,57,484,77,1310,212,1035,919,619,1316,839,850,833,15,69,485,66,673,355,36,427,361,530,491,609,734,27,10,275,1,411,585,447,390,223,153,29,356,36,196,182,193,84,34,23,30,31],"PROJECT_COUNT":[3789,1807,552,2477,159,1777,112,1278,1325,53,851,226,65,199,236,359,1610,100,491,89,1313,405,1039,928,625,1328,841,850,838,15,71,492,79,673,357,47,428,361,649,493,616,803,28,16,280,1,453,585,447,390,231,156,30,356,68,196,188,193,84,41,31,32,33],"TOTAL":{"__ndarray__":"v4BeuFNegEAXR+UmqgaAQBx6i4f3Qn5AwJZXrvdOdkAcmrLTj6JzQLXEymik/3BAiEhNuxhkbUAIq7GEtRhtQPTDCOFRyWhACtY4m46KaECWXTC45rxnQMpUwagkN2ZAgGQ6dHp6ZECtp1Zf3cRjQIE+kSfJzmJASaEsfP1nYUC5iVqa22dhQD25pkBmxWBA/YNIhpyqYEB80okE04NgQETdByC1ql9AQbtDigEuX0Ci0LLuH8ZeQE7soX2s3V1ADI671hjVXUAkSKXY0XBdQNegL739MVxA499nXDioWkAo8E4+PWZaQA/QfTmzUlpAIuNRKuEzWUBUi4hi8iFYQAhyUMJM61VAjPSidr/jVUAlWvJ4WvBUQF6gpMACjVJA8BXdek1xUkAju9IyUkhSQAQ8aeGyQVJATMecZ+zhUUAM6IU7F0tRQCtNSkG3hVBAnP2BcttDUEBB0xIroz9QQB8PfXcr2U9AAAAAAACAT0BRoE/kSX5PQALyJVRwLE9AnfS+8bURT0AF3PP8addNQDVEFf4MtU1AzGH3HcNBTUDHuOLiqLhMQJtxGqIKWUxAqkVEMXkvTEAeGhajrvFLQFZ9rrZib0tAYRxcOuZgS0DZmNcRhxZLQLAApgwczEpAtFa0Oc7DSkABpDZxcm1KQNBDbRtG5UlA","dtype":"float64","shape":[63]},"color":["blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue","blue"],"index":[12651,15764,3058,2887,15549,1306,10529,4651,8664,9155,9780,6821,5622,7946,1783,15396,16805,13743,801,6455,3359,10304,14782,12139,3034,11203,7470,11063,9398,16397,2687,8310,2406,3986,15505,271,8593,16428,14263,14,8495,5702,15879,2907,13576,6792,6428,598,5617,3407,9364,12510,16799,14757,1825,7478,5244,9077,5317,8540,16689,3736,15588],"primary":["res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res","res"],"res_deficit":[-3781,-1755,-12,-2469,-53,-1775,-36,-1274,-1323,-49,-829,-198,-47,-27,-122,-333,-1600,-14,-477,-65,-1307,-19,-1031,-910,-613,-1304,-837,-850,-828,-15,-67,-478,-53,-673,-353,-25,-426,-361,-411,-489,-602,-665,-26,-4,-270,-1,-369,-585,-447,-390,-215,-150,-28,-356,-4,-196,-176,-193,-84,-27,-15,-28,-29]},"selected":{"id":"2631","type":"Selection"},"selection_policy":{"id":"2632","type":"UnionRenderers"}},"id":"2557","type":"ColumnDataSource"},{"attributes":{"callback":null,"data":{"AVERAGECOST":{"__ndarray__":"j1qEPEBrPUH+mh11iapbQfR2Aw/uRTdBob2E9pO2SUGrqqpqMxFWQXo7Q2IvoDRBmpmZEYFxaEEAAAAAhNeXQZ7xjGeEfxhB0DOnjmhNMkEzMzPTQD1cQRqs0BkNUDJBDPqCPuxDCEFVVVWVpaNLQd3TCIuS0DBBc5U0qsdwFEEAAAAAhNeXQQAAAACqrYZB7+7uLtrqRkHO5dnf4IwYQe0WfjXwlyJBP+mTPsiwOkEEiVbY9FogQZVSSqm0uDJBWGCBBeSWKEEAAAAAJq5GQRdddJHE3jZBA2GkHUHFFEGkcD0KbUkaQQAAAACC3klB4uHh4ca0O0EAAAAAojoJQdC6wRRFUDdBAAAAgJVfHEGamZl5fR0VQSlcj0IvaCBBZmZmxvZDJEE=","dtype":"float64","shape":[37]},"MAXCOST":{"__ndarray__":"AAAAAOKMg0EAAADe/s2gQQAAAADeOYpBAAAAAP1DpEEAAAAAkv6eQQAAAAAGgYRBAAAAOB3Zh0EAAAAA3jmaQQAAAKCKQGlBAAAAgDA9gkEAAAAAiCqBQQAAAACE15dBAAAAwBZzcUEAAAAAdrCAQQAAAAA4nHxBAAAAQL+qV0EAAAAAhNeXQQAAAABXppZBAAAAAB8DcEEAAAAAKLFSQQAAAABg43ZBAAAAAG4KjkEAAAAA0BJjQQAAAACE14dBAAAAAKweckEAAAAAdrBwQQAAAADMv2lBAAAAAICETkEAAADAnZ9fQQAAAAA4nHxBAAAA6A6viEEAAADglHNyQQAAAABUtW5BAAAAAJ2kU0EAAAAA2dpJQQAAAAAo5k5BAAAAAMy/WUE=","dtype":"float64","shape":[37]},"MEDIANCOST":{"__ndarray__":"AAAAAPzMCkEAAAAAgDMmQQAAAAAAaghBAAAAAABqCEEAAAAA6nUkQQAAAABuEBFBAAAAADhnQEEAAAAAhNeXQQAAAACQMQFBAAAAADR0AUEAAAAAQHdLQQAAAAAATO1AAAAAAJjZ8EAAAAAAIBPzQAAAAADAegBBAAAAAEBL+kAAAAAAhNeXQQAAAACqrYZBAAAAAN4yJ0EAAAAAgDH3QAAAAABQG/xAAAAAAADb6kAAAAAAAGr4QAAAAAAQjwNBAAAAAOD170AAAAAAbNYWQQAAAABwkxVBAAAAAEBWBEEAAAAAQHTeQAAAAADAXCVBAAAAALRyBkEAAAAAQDXrQAAAAADALA1BAAAAAIC6BUEAAAAA8FT1QAAAAADAdPFAAAAAAMCN+0A=","dtype":"float64","shape":[37]},"MINCOST":{"__ndarray__":"AAAAAAAAAAAAAAAAAABZQAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwPwAAAAAAAPA/AAAAAAAA8D8AAAAAKnWVQQAAAAAAAPA/AAAAAAAAAAAAAAAAAADwPwAAAAAAAPA/AAAAAAAAJEAAAAAAAECvQAAAAAAAiKNAAAAAAAAAAAAAAAAAhNeXQQAAAAAATP1AAAAAAABwx0AAAAAAAADwPwAAAAAAwGJAAAAAAAAA8D8AAAAAAAAAAAAAAAAAAPA/AAAAAAAA8D8AAAAAAAAAAAAAAAAAQJ9AAAAAAAAAVEAAAAAAAADwPwAAAAAA88ZAAAAAAAAAAAAAAAAAAADwPwAAAAAAQI9AAAAAAABwl0AAAAAAAADwPwAAAAAAAE5AAAAAAAAA8D8=","dtype":"float64","shape":[37]},"NAME":["CLANCY AND THEYS CONSTRUCTION","BALFOUR BEATTY CONSTRUCTION","BRASFIELD &amp; GORRIE, L.L.C.","BARNHILL CONTRACTING COMPANY","SKANSKA USA BUILDING, INC.","SHELCO, INC.","HOLDER CONSTRUCTION GROUP LLC","CMG BUILDERS INC","J. D. BEAM, INC.","DUKE CONSTRUCTION L.P.","NARRON CONTRACTING, INC","MACALLAN CONSTRUCTION, LLC","RILEY-LEWIS GENERAL CONTRACTOR","HOAR CONSTRUCTION, LLC","BARKER &amp; LOVETTE GENERAL CONTR","WILLIAMS REALTY &amp; BUILDING COM","NHSF I, LLC","WAKE CNTY","DEVERE CONSTRUCTION COMPANY, I","BOBBIT DESIGN BUILD, INC.","CENTURION CONSTRUCTION COMPANY","HARDIN CONSTRUCTION COMPANY, L","DAVIDSON &amp; JONES CONSTRUCTION","C.T. WILSON CONSTRUCTION COMPA","D.H. GRIFFIN CONSTRUCTION COMP","EDIFICE, INC.","T.A. LOVING COMPANY","RILEY CONTRACTING GROUP","ASHLAND CONSTRUCTION COMPANY","THE WHITING-TURNER CONTRACTING","ROBINS &amp; MORTON GROUP, THE","SPEC CON,INC","RCI BUILDERS, INC","STEEL DYNAMICS, INC.","METROCON","HARROD &amp; ASSOCIATED CONSTRUCTO","HARROD &amp; ASSOCIATES CONSTRUCTO"],"NUMBER_OF_NON_RESIDENTIAL":[588,147,665,162,81,198,20,2,445,134,20,119,688,36,116,370,1,2,30,215,134,45,142,62,93,23,44,190,150,19,34,292,37,120,160,100,80],"NUMBER_OF_RESIDENTIAL":[0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0],"PROJECT_COUNT":[588,147,665,162,81,198,20,2,445,134,20,119,688,36,116,370,1,2,30,215,134,45,142,62,93,23,44,190,150,19,34,292,37,120,160,100,80],"TOTAL":{"__ndarray__":"/tMNFKi2kUBA2v8Ae6iQQC/9S1I5so9Ab9kh/uEPgUB8uOS4E0l9QABV3LhFunBA0ova/eoEcEAAAAAAAABpQC2VtyOcU2ZAFl5Z1E0XZEAHeqhtw4FiQFkV4SYj2mFA85L/yV8YYUBQptHkYk1gQGHB/YAH9V9Anl2+9WH6XkAAAAAAAABZQEjhehSux1dAbToCuFmHVkDqXbwft55VQA677xgeaVRAfnA+daytU0AfEVMiiQZTQF3cRgN4BFNAbsST3cy7UkAhrweT4hdRQCQLmMCtfFBAjniymxkqUEDJzAUujyZQQPZefNEeG1BACp3X2CXeTkBfDOVEuyxOQGiyf54GRExAtTf4wmTkS0DRAx+DFa1LQBlXXByV4UpAWJI81/ePSkA=","dtype":"float64","shape":[37]},"color":["red","red","red","red","red","red","red","red","red","red","red","red","red","red","red","red","red","red","red","red","red","red","red","red","red","red","red","red","red","red","red","red","red","red","red","red","red"],"index":[3144,1056,1899,1144,14359,14180,7364,3248,7939,4717,11164,9814,13261,7303,1111,16980,11340,16448,4367,1683,2896,6791,4093,2416,3931,4940,15256,13258,795,15567,13396,14685,12950,14836,10531,6900,6901],"primary":["non","non","non","non","non","non","non","non","non","non","non","non","non","non","non","non","non","non","non","non","non","non","non","non","non","non","non","non","non","non","non","non","non","non","non","non","non"],"res_deficit":[588,147,665,162,81,198,20,2,445,134,20,119,688,36,116,370,1,2,30,215,134,45,142,62,93,23,44,190,150,19,34,292,37,120,160,100,80]},"selected":{"id":"2620","type":"Selection"},"selection_policy":{"id":"2621","type":"UnionRenderers"}},"id":"2556","type":"ColumnDataSource"},{"attributes":{},"id":"2570","type":"BasicTicker"},{"attributes":{"bottom_units":"screen","fill_alpha":{"value":0.5},"fill_color":{"value":"lightgrey"},"left_units":"screen","level":"overlay","line_alpha":{"value":1.0},"line_color":{"value":"black"},"line_dash":[4,4],"line_width":{"value":2},"plot":null,"render_mode":"css","right_units":"screen","top_units":"screen"},"id":"2587","type":"BoxAnnotation"},{"attributes":{},"id":"2582","type":"SaveTool"},{"attributes":{},"id":"2579","type":"PanTool"},{"attributes":{},"id":"2565","type":"LinearScale"},{"attributes":{"overlay":{"id":"2587","type":"BoxAnnotation"}},"id":"2581","type":"BoxZoomTool"},{"attributes":{"label":{"value":"Residential"},"renderers":[{"id":"2612","type":"GlyphRenderer"}]},"id":"2622","type":"LegendItem"},{"attributes":{"callback":null},"id":"2563","type":"DataRange1d"},{"attributes":{},"id":"2583","type":"ResetTool"},{"attributes":{},"id":"2621","type":"UnionRenderers"},{"attributes":{"below":[{"id":"2569","type":"LinearAxis"}],"left":[{"id":"2574","type":"LinearAxis"}],"renderers":[{"id":"2569","type":"LinearAxis"},{"id":"2573","type":"Grid"},{"id":"2574","type":"LinearAxis"},{"id":"2578","type":"Grid"},{"id":"2587","type":"BoxAnnotation"},{"id":"2607","type":"Legend"},{"id":"2599","type":"GlyphRenderer"},{"id":"2612","type":"GlyphRenderer"}],"title":{"id":"2558","type":"Title"},"toolbar":{"id":"2585","type":"Toolbar"},"x_range":{"id":"2561","type":"DataRange1d"},"x_scale":{"id":"2565","type":"LinearScale"},"y_range":{"id":"2563","type":"DataRange1d"},"y_scale":{"id":"2567","type":"LinearScale"}},"id":"2559","subtype":"Figure","type":"Plot"},{"attributes":{},"id":"2567","type":"LinearScale"},{"attributes":{"fill_alpha":{"value":0.6},"fill_color":{"field":"color"},"line_color":{"field":"color"},"line_dash":[5,3],"size":{"units":"screen","value":10},"x":{"field":"PROJECT_COUNT"},"y":{"field":"TOTAL"}},"id":"2610","type":"Circle"},{"attributes":{"dimension":1,"plot":{"id":"2559","subtype":"Figure","type":"Plot"},"ticker":{"id":"2575","type":"BasicTicker"}},"id":"2578","type":"Grid"}],"root_ids":["2559"]},"title":"Bokeh Application","version":"1.0.4"}}
        </script>
        <script type="text/javascript">
          (function() {
            var fn = function() {
              Bokeh.safely(function() {
                (function(root) {
                  function embed_document(root) {
                    
                  var docs_json = document.getElementById('2703').textContent;
                  var render_items = [{"docid":"792430e0-aac8-455c-83eb-db97f0bc1c50","roots":{"2559":"bbbb8b24-8346-4b18-b590-10ddc322b66b"}}];
                  root.Bokeh.embed.embed_items(docs_json, render_items);
                
                  }
                  if (root.Bokeh !== undefined) {
                    embed_document(root);
                  } else {
                    var attempts = 0;
                    var timer = setInterval(function(root) {
                      if (root.Bokeh !== undefined) {
                        embed_document(root);
                        clearInterval(timer);
                      }
                      attempts++;
                      if (attempts > 100) {
                        console.log("Bokeh: ERROR: Unable to run BokehJS code because BokehJS library is missing");
                        clearInterval(timer);
                      }
                    }, 10, root)
                  }
                })(window);
              });
            };
            if (document.readyState != "loading") fn();
            else document.addEventListener("DOMContentLoaded", fn);
          })();
        </script>
    
  </body>
  
</html>



*There's probably a lot more I could do with this data. Are there any questions you would like me to answer in a future post? Does anything here make you feel curious? You can let me know by commenting below or emailing me at [michaelfosterprojects@gmail.com](mailto:michaelfosterprojects@gmail.com)*