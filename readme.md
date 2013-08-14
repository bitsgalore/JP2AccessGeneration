# Generation of access images from lossless JP2 masters demo

##About this repo
This repo serves to demonstrate a number of options that are available to derive lossy access images from losslessly compressed archival JP2s. A discussion of these results can be found in this [blog post](). 

## Note on downloading these files
Github doesn't allow you to download individual files in a repo if they are over 10 (I think) MB! As some of the images here are above this limit, you should either clone this repo using *Git*, or use the  [Download ZIP](https://github.com/bitsgalore/JP2AccessGeneration/archive/master.zip) button. 

##Contents

* *profiles* directory - contains XML-formatted [jpwrappa](https://github.com/openplanets/jpwrappa) profiles that were used to generate the lossles JP2s (jpwrappa is a Python wrapper for the [Aware JPEG 2000 SDK](http://www.aware.com/imaging/jpeg2000sdk.html)).
* *outjpylyzer.xml* - [jpylyzer](https://github.com/openplanets/jpylyzer) output of all JP2 and JPX files in this repo.
* For all others files, see the table below (you may need to use the scrollbar at the bottom to see all columns):

|Image name|Format|Source image|Creator tool|Command line|
|:---|:---|:---|:---|:---|
|balloon_eciRGBv2.tif|TIFF|[1783_balloonj.jpg](http://upload.wikimedia.org/wikipedia/commons/a/a8/1783_balloonj.jpg)|-|-|
|balloon_master.jp2|JP2|balloon_eciRGBv2.tif|Aware|Via [jpwrappa](https://github.com/openplanets/jpwrappa), profile [optionsMasterLossless.xml](https://github.com/bitsgalore/JP2AccessGeneration/blob/master/profiles/optionsMasterLossless.xml)|
|balloon_access_kdu.jpf|JPX|balloon_master.jp2|Kakadu|`kdu_transcode -i balloon_master.jp2`<br>`-o balloon_access_kdu.jpf` <br> `jpx_layers sRGB,0,1,2`<br> `Sprofile=PROFILE2` <br> `-rate 1.2`|
|balloon_access_aw.jp2|JP2|balloon_master.jp2|Aware|`j2kdriver -i balloon_master.jp2` <br> `-R 20` <br> `-w I97`<br> `-t JP2` <br> `-o balloon_access_aw.jp2`|
|balloon_master_layers_precincts.jp2|JP2|balloon_eciRGBv2.tif|Aware|Via [jpwrappa](https://github.com/openplanets/jpwrappa), profile [optionsMasterLosslessLayersPrecincts.xml](https://github.com/bitsgalore/JP2AccessGeneration/blob/master/profiles/optionsMasterLosslessLayersPrecincts.xml)|
|balloon_master_layers_precincts_access_kdu.jpf|JPX|balloon_master_layers_precincts.jp2|Kakadu|`kdu_transcode -i balloon_master_layers_precincts.jp2`<br>`-o balloon_master_layers_precincts_access_kdu.jpf` <br> `jpx_layers sRGB,0,1,2`<br> `Sprofile=PROFILE2` <br> `-rate 1.2`|
|balloon_master_layers_precincts_access_aw.jp2|JP2|balloon_master_layers_precincts.jp2|Aware|`j2kdriver -i balloon_master_layers_precincts.jp2` <br> `-ql 3` <br> `-t JP2` <br> `-o balloon_master_layers_precincts_access_aw.jp2`|

##Software used to create derived images
- [Aware JPEG 2000 SDK](http://www.aware.com/imaging/jpeg2000sdk.html) v 3.19.0.0
- [Kakadu](http://www.kakadusoftware.com/) v 7.2.2


##Image attribution and provenance

All images are derived from the following source image: 

[http://commons.wikimedia.org/wiki/File:1783_balloonj.jpg](http://commons.wikimedia.org/wiki/File:1783_balloonj.jpg "http://upload.wikimedia.org/wikipedia/commons/a/a8/1783_balloonj.jpg")

> 1786 description of the historic Montgolfier Brothers' 1783 balloon flight. Illustration with engineering proportions and description.

Public Domain.
