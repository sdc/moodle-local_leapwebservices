# Moodle 2 Web Services for Leap

This plugin contains the web services required for integration between Moodle 2 and Leap, South Devon College's eILP (electronic individual learning plan) system. More info about Leap can be found at [leap-ilp.com](http://leap-ilp.com).

Web services for Leap already existed as they were written for our launch of Moodle 2.1, however they were added to core Moodle code in the first instance, and were becoming increasingly difficult to manage.

Now that Leap is being increasingly used in other colleges, the Moodle-Leap integration need to be seperated out, so now we have rewritten them as a seperate local Moodle plugin.

This local Moodle plugin has it's own repository located at [github.com/sdc/moodle-local_leapwebservices](https://github.com/sdc/moodle-local_leapwebservices), where bugs can be reported and issues raised.

**Note:** This plugin is only required if you are using Leap ILP from south Devon College. It has no use in any other circumstance. :)

## Files

Before installation, please check you have the following files and structure:

    leapwebservices/
    |-- db
    |   \-- services.php
    |-- externallib.php
    |-- lang
    |   \-- en
    |       \-- local_leapwebservices.php
    |-- pix
    |   \-- icon.png
    |-- readme.md
    \-- version.php


## Installation

* Copy the folder this readme is in into your Moodle's *local* folder
* Ensure the folder is named *leapwebservices* (removing any other text which may have appeared as part of the cloning or un-Zipping process)
* Log in to your Moodle site as an Administrator and visit the Notifications page
* The plugin should install without error. If you receive an error, please report it [here](https://github.com/sdc/moodle-local_leapwebservices/issues)

## Configuration

(This guide has been written using Moodle 2.5: your mileage may vary.)

This plugin has no configuration itself, however your Moodle 2.x installation will require configuration to correctly use web services. 

1. Log in to your Moodle as administrator. Click on Administration (block) &rarr; Site Administration &rarr; Plugins &rarr; Web services &rarr; Overview.

    This page shows an overview of Moodle's current web service configuration. You may wish to keep this page open, and open any links in a new tab or window, refreshing this page on your return.

2. Click *1. Enable web services*. Check the box (a tick, cross or other identifying mark will appear, depending on your web browser) to turn web services on, then click *Save settings*. Return to the *Web services &rarr; Overview* screen. 

    The overview screen should now show **yes** next to *1. Enable web services* in the *status* column next.

3. 

## History

* 2013-09-25, v0.3: Documentation changes only: how to configure Moodle to use web services. No code changes.
* 2013-05-24, v0.3: Minor update as the mdl_course table has had some columns re/moved elsewhere in Moodle 2.5.
* 2012-11-20, v0.2: Initial release of the plugin.
