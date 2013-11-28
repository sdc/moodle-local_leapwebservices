# Moodle 2 Web Services for Leap

## Introduction

This plugin contains the web services required for integration between [Moodle](http://moodle.org) 2 and [Leap](http://leap-ilp.com), South Devon College's ILP ( individual learning plan) system. More info about Leap can be found at [leap-ilp.com](http://leap-ilp.com).

## Purpose

Web services for Leap already existed as they were written for our launch of Moodle 2.1, however they were added to core Moodle code in the first instance, and were becoming increasingly difficult to manage.

Now that Leap is being increasingly used in other colleges, the Moodle-Leap integration need to be separated out, so now we have rewritten them as a separate local Moodle plugin.

This local Moodle plugin has it's own repository located at [github.com/sdc/moodle-local_leapwebservices](https://github.com/sdc/moodle-local_leapwebservices), where bugs can be reported and issues raised.

(**Note:** This plugin is only required if you are using Leap ILP from south Devon College. It has no use in any other circumstance. :)

## Licence

Copyright &copy; 2011-2013 South Devon College.

This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with this program.  If not, see <http://www.gnu.org/licenses/>.

## Files

Before installation, please check you have the following files and structure:

    leapwebservices/
    |-- db
    |   \-- services.php
    |-- externallib.php
    |-- gpl-3.0.txt
    |-- lang
    |   \-- en
    |       \-- local_leapwebservices.php
    |-- pix
    |   \-- icon.png
    |-- readme.md
    \-- version.php


## Installation

* Copy the folder containing this readme to your Moodle's **/local** folder
* Ensure the folder is named **leapwebservices** (removing any other text which may have appeared as part of the cloning or un-Zipping process)
* Log in to your Moodle site as an Administrator and visit the Notifications page
* The plugin should install without error. If you receive an error, please report it [here](https://github.com/sdc/moodle-local_leapwebservices/issues)

## Configuration

(**Note:** This guide has been written using Moodle 2.5, which contains many changes from the 2.0 release: your mileage may vary.)

This plugin has no configuration itself, however your Moodle installation will require configuration to correctly use web services. 

1.  Log in to your Moodle as administrator. Click on **Administration (block) &rarr; Site Administration &rarr; Plugins &rarr; Web services &rarr; Overview**.

    (**Note:** *This page shows an overview of Moodle's current web service configuration. You may wish to keep this page open, and open any links in a new tab or window, refreshing this page on your return.*)

2.  Click **1. Enable web services**. Check the box (a tick, cross or other identifying mark will appear, depending on your web browser) to turn web services on, then click **Save settings**. Return to the **Web services &rarr; Overview** screen.

    The overview screen should now show **yes** next to **1. Enable web services** in the **status** column.

3.  Click **2. Enable protocols**. Enable the **REST** protocol: click on the eye with the line through it, it will become **open**.  The other protocols are not required for the Leap web services, however **XML-RPC** is required for the older, unofficial Moodle mobile app and may already be turned on. This is fine: all the protocols can be turned on and won't affect each other, however it is a security concern to run unnecessary protocols, so turn off what you do not need.

    You may benefit from turning on **Web services documentation** (check the checkbox, click **Save settings**) but it is strongly advised to turn it off when it is no longer necessary.

    Return to the **Web services &rarr; Overview** screen. It should now show (at least) **REST** next to **2. Enable protocols** in the **status** column.

4.  A specific user is required to act as Moodle's avatar for incoming web services. You can have one user per web service, or one for all. Our setup uses a user called **Leap User** and it's profile picture is set accordingly.

    Click **3. Create a specific user**.  Create this "Leap user" as you see fit: give it a relevant username ("*leapuser*" in our case) and a **strong** password, as this user will have considerable control over core Moodle functions. 

5.  Create a new role ("web services") with appropriate protocol capabilities allowed (**webservice/rest:use**). Click on **Administration (block) &rarr; Site Administration &rarr; Users &rarr; Permissions &rarr; Define roles**, and click on **Add role**.

    Type in a relevant short (internal) name and a full (human readable) name, as well as a description (will only be seen by admins).  Ignore *Role archetype*. Check only the **system** check box. Search for and **allow** the following capabilities:

    **Web service: REST protocol**
    * webservice/rest:use (Use REST protocol)

    **System**
    * moodle/site:viewparticipants (View participants) 
    * moodle/user:update (Update user profiles)

    **Users**
    * moodle/user:viewalldetails (View user full information)

    **Course**
    * moodle/course:enrolreview (Review course enrolments)
    * moodle/course:movesections (Move sections)
    * moodle/course:update (Update course settings)
    * moodle/course:useremail (Enable/disable email address)
    * moodle/course:view (View courses without participation)
    * moodle/course:viewhiddencourses (View hidden courses)
    * moodle/course:viewparticipants (View participants)
    * moodle/role:review (Review permissions for others)
    * moodle/site:accessallgroups (Access all groups)
    * moodle/user:viewdetails (View user profiles)
    * moodle/user:viewhiddendetails (View hidden details of users)

    (**Note:** the best way is to use your web browser's search feature and search for the text exactly as it appears: it will get you to the exact capability or very close.)

6.  Assign the new *web services role* to the *web services user* as a system role: click on **Administration (block) &rarr; Site Administration &rarr; Users &rarr; Permissions &rarr; Assign system roles**.  Click on *webservices* (or whatever you have named your new role), then search in the box on the right for the new *Leap user*, then **add** the new user so the name appears in the box on the right.  It should be the only name in that box.  Return to the **Web services &rarr; Overview** screen.

7.  Click **4. Check user capability**.  Search for the user just created, then click on the name, then click **Show this user's permissions**.

    The results page should show the user as assigned to the *web service* role (what appears on-screen will be whatever you called the web service) and *authenticated user* in *system* context.

    Check that the list of capabilities in *5, above*, is set to **yes** (highlighted in green).  When done, return to the **Web services &rarr; Overview** screen.

8.  Click **5. Select a service**.  In the **Built-in services** section you should see an entry for *Leap*, and probably also an entry for the *Moodle mobile web service*, which will be greyed out if this is not turned on via the checkbox at the top of the page. (*Moodle mobile web services* are not required to be turned on for Leap web services to work.)

    Clicking on **Authorised users** next to *Leap* will show you a list of users authorised to use the Leap web services. It should show only the user you have assigned, but at the bottom of the page is a section titled **Change settings for the authorised users**: if there are any problems with the assigned user (lacking a particular context) they will be listed here in orange, and will need to be fixed before progressing further. Clicking on the user's name or email address will show some further security options, such as *IP restriction* (so a user can access the web service only from one or a range of IP addresses, blank by default) and a *Valid until* date when the access will cease (off by default). If you change any settings here, click **Update** to save them.

    Clicking the **Edit** button allows you to rename the web service (not recommended) and enable/disable the service. It is enabled as default.

    When done, return to the **Web services &rarr; Overview** screen.

9.  **6. Add functions** and **7. Select a specific user** have already been completed as part of **5. Select a service**, so ignore them. 

10. Click **8. Create a token for a user**.

    In the *Username / user id*  box, type in the exact username of the user created / selected in **step 4**, above.  This is a required field.

    (**Note:** For us, our authentication system [Shibboleth](http://shibboleth.net/) uses usernames in the form of an email address (e.g. username@example.com) but your system may be different and will most likely use only the *username* part.)

    Select *Leap* from the *Service* drop-down list, if it is not already chosen. (If you have Moodle mobile web services enabled, then they will appear also and I believe are the default option.) This is also a required option.

    If you wish, you may restrict the IP addresses from which the *Leap User* is allowed to log in from.  If you know, for example, that the computer/server with the address `172.100.100.1` is the only server which should be accessing Moodle, then put that IP address in the **IP Restriction** box. This way, if someone does find out the username and password for this user, they still won't be able to log in unless they also gain access to the server with that IP address.

    If you wish to restrict the date until which this user can log in with this token, check the **Enable** checkbox and set the date accordingly, either with the drop-down menus or by clicking on the date-picker menu icon.  Remember that you may always create another token for this user at any time, with a longer (or no) expiry: many can run concurrently.

    Click **Save changes** when done. You will be taken back to the **Manage tokens** screen, which will now show an alphanumeric token next to the name of your user. Your token will look something like *a180245560982a0e48e43577238c0198*. Treat this token like a password, keeping it secret and known only to those who absolutely need it, as anyone who has this token potentially has full access to all the webservices you selected earlier.

    (**Note:** This admin screen, and therefore the token, is available to anyone who is an *Administrator* on your Moodle.)

    When done, return to the **Web services &rarr; Overview** screen.

11. As mentioned earlier, you may benefit from turning on **Web services documentation** but it is strongly advised to turn it off when it is no longer necessary.

    Click **9. Enable developer documentation**, check the checkbox, then click **Save settings**. Documentation will only be shown for enabled protocols.

12. There are no built-in tests within Moodle which can test the Leap web service, only a handful of Moodle's own functions. The only way to test it is to add the token to an already-configured Leap system and test to see if a user's Moodle courses are being shown.

    Log in to your **Leap** installation as an administrative user.  Click on the **Admin** dropdiown menu at the top on the right, next to your name. If you cannot see this menu, you do not have administrative rights on your Leap installation.  Select **Settings**.
    
    Scroll down the screen until you see a section called **Old settings**. (This may change in the future as the settings aspect of Leap is improved.)  Find a field called **Moodle token** and paste into this field the token Moodle generated in step 10, above.
    
    Scroll down and click *Save changes*.
    
    Accessing any student's information on Leap should now also show all courses they are enrolled on in Moodle.

    **Note:** If you experience problems with any of the above steps, please contact us via the contact options on [leap-ilp.com](http://leap-ilp.com) or by [opening an issue here on GitHub](https://github.com/sdc/moodle-local_leapwebservices/issues).

## History

* 2013-11-27, v0.3.1: Documentation changes only: how to configure Moodle to use web services. No code changes.
* 2013-08-30, v0.3.1: Removed Moodle user table fields which no longer exist, preventing stack traces in the Moodle/Apache logs.
* 2013-05-24, v0.3: Minor update as the mdl_course table has had some columns re/moved elsewhere in Moodle 2.5.
* 2012-11-20, v0.2: Initial release of the plugin.
