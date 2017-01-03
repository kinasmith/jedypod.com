---
layout: tool
title: PostageStamp-Tools
caption: Postage Stamp Tools
date: 2015-12-23T13:57:19-09:00
category: tool
tags: []
img: circus.png
---
##About

I sometimes like to use PostageStamp nodes in my Nuke scripts when I need to connect one place in my script to another place that is far away. PostageStamp nodes with hidden inputs function as a visual marker for what the thing is that is being “imported” from another place in the script.

There are some frustrations with using PostageStamp nodes though.

First when you Ctrl/Cmd-click a node to select all upstream nodes and move them, nodes are selected through the hidden inputs of postageStamps, so you can accidentally move nodes that might be in a totally different place in your script.

Second, when you want to cut or copy and paste a section of your node graph, all PostageStamps with hidden inputs will be disconnected. This tool posted on Nukepedia got me thinking about how to fix this particular frustration, and I finally got around to writing something that works reliably.

This tool monkeypatches the cut/copy/paste behavior in Nuke to handle PostageStamps as a special exception. It stores what node each one is connected to in a knob on the node itself, so that it can reconnect to the right place when you paste it.

It also adds a shortcut to create a new PostageStamp node, and adds some helpful things like a button to connect it to the selected node (useful if you need to connect it to a node that’s really far away, and don’t want to drag a pipe for hours, or select one and then select the other and hit Y).

##Installation

And here’s how to add it to your menu.py

~~~ python
import postageStampTools
nuke.toolbar('Nodes').addCommand('Other/PostageStamp', 'postageStampTools.create()', 'alt+shift+p')
nuke.menu("Nuke").addCommand('Edit/Cut', lambda: postageStampTools.cut(), 'ctrl+x')
nuke.menu("Nuke").addCommand('Edit/Copy', lambda: postageStampTools.copy(), 'ctrl+c')
nuke.menu("Nuke").addCommand('Edit/Paste', lambda: postageStampTools.paste(), 'ctrl+v')
~~~

##Code

{% gist jedypod/29187fa8c82bbbf4bf5e %}