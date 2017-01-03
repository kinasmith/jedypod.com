---
layout: tool
title: Bake-Roto-Nuke-Script
caption: Bake Roto Nuke Script
date: 2015-12-23T14:05:44-09:00
category: tool
tags: []
img: bake_roto.png
---
##About

Bake Roto is a python script that will bake an arbitrary control vertex on a Nuke Rotopaint shape or stroke into position data. This is inspired by [Magno Borgo‘s](http://www.borgo.tv/) [BakeRotoShapesToTrackers script](http://www.nukepedia.com/python/misc/bakerotoshapestotrackers/). Baking is nearly instantaneous, and takes into account transforms for shapes parented under layers that have animations or expression links.

##Usage

Select a Roto or RotoPaint node and run the script. Don’t forget to turn on the “toolbar label points” button to see the cv numbers. It’s on my list to make the interface for this better. I should learn PySide better and make a selectable list of CV points instead of a dropdown. Soon, when there is time!

##Code

{% gist jedypod/6968830 %}