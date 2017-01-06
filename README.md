# connextcms-plugin-template
This is a template for developing your own plugins for [ConnextCMS](https://github.com/skagitpublishing/ConnextCMS)
and [KeystoneJS](https://github.com/keystonejs/keystone).

## Installation
It is assumed that this repository will be cloned into a working copy of [ConnextCMS](http://connextcms.com/). 
You can [clone your own working copy of ConnextCMS](http://connextcms.com/page/clone-your-own) for testing purposes.

To install this example project, clone this repository into your home directory and run the `merge-plugin` script.

This script assumes you are using a [ConnextCMS installation best practices](https://github.com/skagitpublishing/ConnextCMS/wiki/2.-Installation#installation-best-practice).


## File Structure
    |--keystone
    |  This is where the KeystoneJS specific files live.
    |  |--models
    |  |  Add any KeystoneJS models that your plugin needs to this directory.
    |  |--routes
    |  |  This directory contains the handlers for any new APIs
    |  |  |
    |  |  |--exampleRouter.js
    |  |  |  This file be ready by KeystoneJS and any new API paths with be added the KeystoneJS router.
    |  |  |--exampleplugin.js
    |  |  |  This is a demo/example API handler file.
    |--connextcms
    |  This is where ConnextCMS specific files live.
    |  |--models
    |  |  Contains Backbone.js Models and Collections that will be used by the ConnextCMS Backbone application.
    |  |--views
    |  |  Contains Backbone.js Views that will be added to the ConnextCMS Dashboard.
    |  |--templates
    |  |  Contains HTML template files used by ConnextCMS Backbone.js Views.
    |--pluginSettings.json
    |  JSON file containing the information ConnextCMS needs to interface to the plugin
    |--pluginLoader.js
    |  Script executed by ConnextCMS when the Dashboard loads.
    |--merge-plugin
    |  Bash shell script for merging your plugin into a working installation of ConnextCMS


## Design Overview
ConnextCMS now has hooks to allow the development of plugins. Plugins allow new websites and web apps to
develop their code base totally independent of ConnextCMS's code base. ConnextCMS software and plugin
code can be be updated without any manual editing. This plugin template has been developed for two reasons:

1. To give an example on how JavaScript developers can create their own ConnextCMS/KeystoneJS plugins.

2. To illustrate the various interfaces between KeystoneJS and ConnextCMS. To show where and how the two systems interact and where they are independent.


## KeystoneJS
Keystone has its own system for routing API calls, displaying views, and creating database models. ConnextCMS relies heavily on
the API routes and interacts with database models through these APIs. The ConnextCMS dashboard is contained in a single 
KeystoneJS view, but does not interact much with this part of KeystoneJS. This plugin template allows you to create 
new KeystoneJS routes, views, and models as you see fit.

### Keystone Routes
The API routes for this example plugin are defined in `exampleRouter.js`. This file gets read by the `routes/index.js` file
when KeystoneJS starts.

The API handler functions for this example plugin live in `exampleplugin.js`. This is the code that gets executed when your
plugin API is called. 

### Keystone Views
KeystoneJS is configured to use the Handlebar template language for its views. View files end with extension .hbs, but HTML can be
copied and pasted into these files. The ConnextCMS Dashboard is single Keystone View configured for the path `/dashboard`. 
The `/edituser` view which lets users change their password is another example of a Keystone View.

The route for Keystone Views are defined in the `routes/exampleRouter.js` file, but the website content is defined by the .hbs file
in the `templates/views` directory.

### Keystone Models
In many ways KeystoneJS Models act as an API to MongoDB, the database used to power KeystoneJS. Read up on the 
[KeystoneJS model documentation](http://keystonejs.com/docs/database/) for more information.


## ConnextCMS
[ConnextCMS](https://github.com/skagitpublishing/ConnextCMS) is a Backbone.js application and front end
extension for KeystoneJS. The user interface mimics popluar CMS UI such as WordPress and Shopify. This plugin
template allows you to create your own menu items and Backbone Views for extending both ConnextCMS and KeystoneJS.
All plugin files that interact directly with ConnextCMS reside in the `connextcms` directory.

### Backbone Views
Plugins to ConnextCMS have two views they need to interact with. The first is their own View that will get displayed.
This view file resides in the `connextcms/views` directory. 

The second view that a plugin must manage is the Left Menu View, which is the primary UI menu that is used to navigate
around the ConnextCMS Dashboard. The file `pluginLoader.js` is executed by ConnextCMS on page load. This file contains
the code for loading plugin view files as well as creating a menu item in the Left Menu View.

### Backbone Models & Collections
The Backbone Models and Collections used in ConnextCMS often mirror the KeystoneJS models. While the KeystoneJS models
perist in a MongoDB database on the server, the Backbone Models and Collections exist in the memory space of the browser.
They sync with the server via KeystoneJS API calls. 

By storing data in Backbone Models and Collections, data can be managed more efficiently and API calls between the
Backbone application server are reduced. 


