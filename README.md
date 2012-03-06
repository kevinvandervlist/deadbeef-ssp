# Screen Saver Pause plugin for DeaDBeeF**

This plugin enables you to pause DeaDBeeF automatically on 
an active screensaver. When you run ./configure, the build environment 
automatically tries to use glib bindings. The advantage of this method is that
the plugin registers itself with deadbeef's main loop. 

When you don't want / don't need glib dependency, this configure script 
falls back on a pthreaded poller. It polls all queued events once every 
second, and then goes to sleep again. 

 - Dependencies:
    - libdbus-glib-1-dev
    - libglib2.0-dev

This plugin is released under the terms of the GPLv2. 

**summary A list of known supported WM's.**

These, and possibly more, window managers are supported. Feel free to add a custom, verified version. 

    || Window Manager || Version || Signal ||
    || KDE || 4.4.5 || "org.freedesktop.ScreenSaver","ActiveChanged" ||
    || Gnome || 2.32.0 || "org.gnome.SessionManager.Presence","StatusChanged" ||
    || Gnome || 2.30.0 || "org.gnome.ScreenSaver","ActiveChanged" ||

**What to do when the plugin is not working?**

Currently, the plugin only listens for a few DBUS signals. If you need additional signals, figure it out in the following way:

 1. Finding usable signals by monitoring your DBus session:

    dbus-monitor --session

 2. Then lock your screen / put it on screensaver, and figure out what kind of event gets triggered that way. It probably is something like this:

    signal sender=:1.21 -> dest=(null destination) serial=282 path=/ScreenSaver; interface=org.freedesktop.ScreenSaver; member=ActiveChanged
    
    boolean true

 3. Add this signal to the code, and it should be working. 

If it is a common signal (for example, after a new GNOME version, or for Enlightenment or whatever, please create an issue with the same signal output as printed above. 
Also, please describe what system + window manager you are using.
