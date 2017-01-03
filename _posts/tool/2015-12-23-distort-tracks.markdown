---
layout: tool
title: Distort-Tracks
caption: Distort Tracks
date: 2015-12-23T14:08:25-09:00
category: tool
tags: []
img: distort_tracks.png
---
##About

This gizmo reformats and/or distorts tracking data based on a uv distortion map input. When you are working with CG elements in your comp that are undistorted and padded resolution, sometimes it is useful to reconcile tracking data from a 3d position through a camera into screen space. This data can then be used to do stuff in 2d: track in lens flares, matchmove roto or splinewarps, etc. The problem is that when this tracking data comes back from our padded undistorted 3d scene into distorted, unpadded resolution comp land, it doesn’t line up.

##Instructions

Connect the UV input to a uv distortion map and set the channel that holds it, (for example, a LensDistortion node set to output type Displacement, outputting a UV distortion map into the forward.u and forward.v channels)
Set the padded resolution format and the destination format: Padded resolution is the overscan resolution that you are distorting from, Destination format is the comp resolution you end up in. If they are the same, set them both to be the same.
Add as many tracking points as you want and copy or link the data in. You can show or hide the input and output tracks for convenience. (It is easier to copy the data of many tracks in if you don’t see the output track knobs.)
Hit Execute, and all tracks will be distorted. The output tracking data will be copied into each tracks respective trk_out_# knob.

##Notes

iDistort Input will theoretically let you plug an iDistort map in and have your tracking data distorted by it. UVMap Animation enabled will severely limit the speed at which the uvmap image data can be sampled, but will enable animated distortion maps.
Note that right now this only works with reformat types set to center, no resize, such as you would use when cropping a padded resolution cg plate back to comp resolution before distorting it. Theoretically this gizmo should work to ‘reformat’ tracking data as well. If you plug in an ‘identity’ uvmap, the tracking data should be undistorted, but reformatted from the source format to the destination format.
Also note that the distorted track output will switch to the reformatted track at the bounds of frame, so that the distorted track does not suddenly pop to 0,0 where the distortion map turns black.

Huge thanks to Ivan Busquets for the ninja-comp technique used to invert the UV Map using a DisplaceGeo.

##Code

{% gist jedypod/6302723 %}