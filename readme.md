# Generation of access images from lossless JP2 masters demo

##About this repo
This repo serves to demonstrate a number of options that are available to derive lossy access images from losslessly compressed archival JP2s. A discussion of these results can be found in this [blog post](http://www.openplanetsfoundation.org/blogs/2013-08-19-optimising-archival-jp2s-derivation-access-copies). 

## Note on downloading these files
Github doesn't allow you to download individual files in a repo if they are over 10 (I think) MB! As some of the images here are above this limit, you should either clone this repo using *Git*, or use the  [Download ZIP](https://github.com/bitsgalore/JP2AccessGeneration/archive/master.zip) button. 

##Contents

* *profiles* directory - contains XML-formatted [jpwrappa](https://github.com/openplanets/jpwrappa) profiles that were used to generate the lossles JP2s (jpwrappa is a Python wrapper for the [Aware JPEG 2000 SDK](http://www.aware.com/imaging/jpeg2000sdk.html)).
* *outjpylyzer.xml* - [jpylyzer](https://github.com/openplanets/jpylyzer) output of all JP2 and JPX files in this repo.
* For all others files, see the table below (rightmost column shows command-line options used to create each image, use the scrollbar at the bottom to see it!):

|Image name|Format|Source image|Creator tool|Command line|
|:---|:---|:---|:---|:---|
|balloon_eciRGBv2.tif|TIFF|[1783_balloonj.jpg](http://upload.wikimedia.org/wikipedia/commons/a/a8/1783_balloonj.jpg)|-|-|
|balloon_master.jp2|JP2|balloon_eciRGBv2.tif|Aware|Via [jpwrappa](https://github.com/openplanets/jpwrappa), profile [optionsMasterLossless.xml](https://github.com/bitsgalore/JP2AccessGeneration/blob/master/profiles/optionsMasterLossless.xml)|
|balloon_access_kdu.jpf|JPX|balloon_master.jp2|Kakadu|`kdu_transcode -i balloon_master.jp2`<br>`-o balloon_access_kdu.jpf` <br> `-jpx_layers sRGB,0,1,2`<br> `Sprofile=PROFILE2` <br> `-rate 1.2`|
|balloon_access_aw.jp2|JP2|balloon_master.jp2|Aware|`j2kdriver -i balloon_master.jp2` <br> `-R 20` <br> `-w I97`<br> `-t JP2` <br> `-o balloon_access_aw.jp2`|
|balloon_master_layers_precincts.jp2|JP2|balloon_eciRGBv2.tif|Aware|Via [jpwrappa](https://github.com/openplanets/jpwrappa), profile [optionsMasterLosslessLayersPrecincts.xml](https://github.com/bitsgalore/JP2AccessGeneration/blob/master/profiles/optionsMasterLosslessLayersPrecincts.xml)|
|balloon_access_layers_precincts_kdu.jpf|JPX|balloon_master_layers_precincts.jp2|Kakadu|`kdu_transcode -i balloon_master_layers_precincts.jp2`<br>`-o balloon_access_layers_precincts_kdu.jpf` <br> `-jpx_layers sRGB,0,1,2`<br> `Sprofile=PROFILE2` <br> `-rate 1.2`|
|balloon_access_layers_precincts_aw.jp2|JP2|balloon_master_layers_precincts.jp2|Aware|`j2kdriver -i balloon_master_layers_precincts.jp2` <br> `-ql 3` <br> `-t JP2` <br> `-o balloon_access_layers_precincts_aw.jp2`|

##Encoding properties of lossless source images
###balloon_master.jp2 
|Parameter|Value|
|:---|:---|
|File format|JP2 (JPEG 2000 Part 1)|
|Compression type|Lossless (reversible 5-3 wavelet filter)|
|Colour transform|Yes (only for colour images)|
|Number of decomposition levels|5|
|Progression order |RPCL|
|Tile size |1024 x 1024|
|Code block size| 64 x 64 (2<sup>6</sup> x 2<sup>6</sup>)|
|Number of quality layers|	1|
|Error resilience|	Start-of-packet headers; end-of-packet headers; segmentation symbols|

###balloon_master_layers_precincts.jp2

|Parameter|Value|
|:---|:---|
|File format|JP2 (JPEG 2000 Part 1)|
|Compression type|Lossless (reversible 5-3 wavelet filter)|
|Colour transform|Yes (only for colour images)|
|Number of decomposition levels|5|
|Progression order |RPCL|
|Tile size |1024 x 1024|
|Code block size| 64 x 64 (2<sup>6</sup> x 2<sup>6</sup>)|
|Precinct size	|256 x 256 (2<sup>8</sup>) for 2 highest resolution levels; 128 x 128 (2<sup>7</sup>) for remaining resolution levels|
|Number of quality layers|11|
|Target compression ratio layers|2560:1 [1] ; 1280:1 [2] ;  640:1 [3] ; 320:1 [4] ; 160:1 [5] ; 80:1 [6] ; 40:1 [7] ; 20:1 [8] ; 10:1 [9] ; 5:1 [10] ; 2.5:1 [11]\*|
|Error resilience|	Start-of-packet headers; end-of-packet headers; segmentation symbols|

\* Actual compression ratio equals overall image compression ratio (which is usually smaller)

##Software used to create derived images
- [Aware JPEG 2000 SDK](http://www.aware.com/imaging/jpeg2000sdk.html) v 3.19.0.0
- [Kakadu](http://www.kakadusoftware.com/) v 7.2.2


##Image attribution and provenance

All images are derived from the following source image: 

[http://commons.wikimedia.org/wiki/File:1783_balloonj.jpg](http://commons.wikimedia.org/wiki/File:1783_balloonj.jpg "http://upload.wikimedia.org/wikipedia/commons/a/a8/1783_balloonj.jpg")

> 1786 description of the historic Montgolfier Brothers' 1783 balloon flight. Illustration with engineering proportions and description.

Public Domain.
