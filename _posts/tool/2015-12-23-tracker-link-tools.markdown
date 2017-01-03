---
layout: tool
title: Tracker-Link-Tools
caption: Tracker Link Tools
date: 2015-12-23T14:02:04-09:00
category: tool
tags: []
img: tracker_link_tools.png
---
##About

It is often the case that you need link things to a Tracker node. It could be a Roto, RotoPaint, or SplineWarp layer that has linked transforms, or a Tracker node that links its transforms to a parent tracker. Tracker Link Tools is a script to do these things.

The script has two functions. The first is to create a linked Roto node. If you have a tracker node selected, and have installed it as described, press Alt-O, and a Roto node will be created with a layer linked to the selected Tracker node. Sometimes you might want to create a linked layer in an existing Roto, RotoPaint or SplineWarp node. No problem, just select as many target nodes as you want, along with your Tracker node, and press Alt-O to run the script. All selected target nodes will have a linked layer added to them.

The other function is to create a linked Transform node. Sometimes you have a Tracker or a Transform node, and you need to apply the same transformation in many places in your Nuke script. You could create many copies of your original Tracker or Transform node, or you could use this script to create a TransformLink node. Select as many parent Tracker or Transform nodes, and press Alt-L. Linked Transform nodes will be created for each.

The TransformLink node has some extra features compared to a regular Transform node. By default, when it is created, it will be linked using a relative transform. This means that on the identity frame specified, the transformation will be zeroed out. This identity frame is separate from the parent Tracker node. You can switch the node from Matchmove to Stabilize functionality by checking the ‘invert’ knob.

Sometimes, especially if you are linking to a parent node that is a Transform, you will just want to inherit the exact transformation of the parent node. If this is the case, you can click the Delete Rel button, and it will remove the relative transformation. Once the TransformLink node is created, you can also use the Set Target button to link it to a different Tracker or Transform node. You can also bake the expressions on the transform knobs with the Bake Expressions button.

This node might seem redundant to the built-in functionality of Nuke7’s Tracker node that lets you create a Matchmove or Stabilize transform. Unfortunately the transform nodes that are created using this method are burdened by excessive python code on the ‘invert’ knob, which is evaluating constantly, degrading Nuke’s UI performance. Turn on “Echo python commands to output window” in the Preferences under Script Editor. In a heavy script with a few of these nodes, you will probably notice stuttery UI responsiveness and freezing.

##Installation

Put the tracker_link.py file somewhere in your nuke path. You can add the script as commands to your Nodes panel. This code creates a custom menu entry called “Scripts”. I have them set to the shortcuts Alt-O and Alt-L.

~~~ python
import tracker_link
nuke.toolbar('Nodes').addMenu('Scripts').addCommand('Link Roto', 'tracker_link.link_roto()', 'alt+o')
nuke.toolbar('Nodes').addMenu('Scripts').addCommand('Link Transform', 'tracker_link.link_transform()', 'alt+l')
~~~

## Code

{% gist jedypod/6969051 %}