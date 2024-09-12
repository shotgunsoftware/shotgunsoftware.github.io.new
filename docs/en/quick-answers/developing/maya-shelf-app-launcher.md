---
layout: default
title: How do I add a shelf button to launch a Toolkit app in Maya?
pagename: maya-shelf-app-launcher
lang: en
---

# How do I add a shelf button to launch a Toolkit app in Maya?

Adding a shelf button in Maya to launch Toolkit apps in Maya is pretty straightforward. Here is an example of how to add a custom shelf button that opens the [Loader app](https://developer.shotgridsoftware.com/a4c0a4f1/). 

{% include info title="Note" content="This assumes Toolkit is currently enabled in your Maya session. This example code does not bootstrap Toolkit." %}

Open your Script Editor in Maya and paste in the following Python code: 

```python
import maya.cmds as cmds 

# Define the name of the app command we want to run.
# If your not sure on the actual name you can print the current_engine.commands to get a full list, see below.
tk_app = "Publish..."

try: 
    import sgtk

    # get the current engine (e.g. tk-maya) 
    current_engine = sgtk.platform.current_engine() 
    if not current_engine: 
        cmds.error("ShotGrid integration is not available!") 

    # find the current instance of the app.
    # You can print current_engine.commands to list all available commands.
    command = current_engine.commands.get(tk_app) 
    if not command: 
        cmds.error("The Toolkit app '%s' is not available!" % tk_app) 

    # now we have the command we need to call the registered callback
    command['callback']()

except Exception, e: 
    msg = "Unable to launch Toolkit app '%s': %s" % (tk_app, e)
    cmds.confirmDialog(title="Toolkit Error", icon="critical", message=msg)
    cmds.error(msg)
```

Select this code and drag it on to your custom shelf. See [Maya docs for more info on how to work with custom shelf buttons](https://knowledge.autodesk.com/support/maya/learn-explore/caas/CloudHelp/cloudhelp/2016/ENU/Maya/files/GUID-C693E884-F81A-4858-B5D6-3856EB8F394E-htm.html).

You should be able to use this code example to launch any Toolkit apps that are enabled in Maya by modifying the `tk_app` and `call_func` variables at the top.
