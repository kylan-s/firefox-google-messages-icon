# Guide

## Create a New Shortcut

1. On Windows, right click the desktop and select "New > Shortcut".
2. Either navigate to the install location of Firefox, or paste the path to the executable and hit next. For me, Firefox was installed at `C:\Program Files\Mozilla Firefox\firefox.exe`
3. Create a descriptive name for the shortcut (i.e. Google Messages), and hit finish.
4. Right click the shortcut and select "Properties". In the "Target" field, insert the command line options `-new-instance -P "google-messages" -new-window -url https://messages.google.com/web/conversations`
    * Note: `-no-remote` may be more robust than `-new-instance` and will launch a new instance by default. Feel free to experiment.
    * At this point, the full "Target" field for me was `"C:\Program Files\Mozilla Firefox\firefox.exe" -new-instance -P "google-messages" -new-window -url https://messages.google.com/web/conversations`.

## Configure Firefox settings
At this point, if you have not already created a profile named "google-messages", you will be prompted to do so upon launching the new shortcut.

0. Launch Firefox in your newly-created profile. 
1. Navigate to `about:config` in the URL bar and hit "Accept the Risk and Continue".
2. Either update the value of or - if it does not yet exist - create a new boolean key named `taskbar.grouping.useprofile` with the value `true`
3. Update the value of the key `browser.startup.blankwindow` to false.
4. Close the current window, and relaunch the newly-created shortcut. You should now see a second Firefox icon on the taskbar.
5. Right click the new Firefox icon and press "Pin to taskbar"

## Create a userChrome.css File
You should now have a working shortcut either on your desktop or taskbar which launches the chosen website with a new taskbar icon. The following will customize this profile so that there is no URL bar visible.

0. Launch Firefox from your recently-created shortcut.
1. Navigate to `about:support` in the URL bar.
2. Under the "Profile Folder" row, hit "Open Folder". A new explorer window should open to the folder `%APPDATA%\Mozilla\Firefox\Profiles\[random characters].google-messages`
3. If it does not exist, create a new folder with the name `chrome`. Inside this folder, create a blank .css file named `userChrome.css`.
4. Edit `userChrome.css` and paste the following contents:
```
/*
 * Do not remove the @namespace line -- it's required for correct functioning
 */
@namespace url("http://www.mozilla.org/keymaster/gatekeeper/there.is.only.xul"); /* set default namespace to XUL */

/*
 * Hide tab bar, navigation bar and scrollbars
 * !important may be added to force override, but not necessary
 * #content is not necessary to hide scroll bars
 */
#TabsToolbar {visibility: collapse;}
#navigator-toolbox {visibility: collapse;}
browser {margin-right: -14px; margin-bottom: -14px;}
```
5. Relaunch Firefox.

## Optional: Update Icons
1. Download the attached .ico file and save it somewhere secure, such as the Firefox install directory (for me, `C:\Program Files\Mozilla Firefox`)
2. Open the shortcut properties
    * To update a desktop icon: right click the shortcut and hit "Properties", or
    * To update a taskbar icon: right click the shortcut, right click the item above "Unpin from taskbar", and hit "Properties"
5. Hit "Change Icon..." and navigate to the location of the .ico file you just saved.

### Note: Applying Changes
You may need to either log out and log back in or restart your computer to see the changes.

### Bonus Tip: Rename Taskbar Icon
The location of the taskbar icon you are editing is in the "General" tab. Mine was `%APPDATA%\Microsoft\Internet Explorer\Quick Launch\User Pinned\TaskBar`. Here, you can rename the shortcut.

## Note: Attached Files
I have provided copies of the desktop shortcut I created, my `userChrome.css` file, and the icon file I created. Please feel free to use them.


# Reference

[Firefox hide everything except content area of the browser - community wiki - Super User](https://superuser.com/a/1269912)

[jooize - Multiple Firefox in Windows Taskbar - GitHub](https://gist.github.com/jooize/5636b9eb975bde30c38b753e9f301de4)

[How to Create a userChrome.css File](https://www.userchrome.org/)

[Firefox/CommandLineOptions - Mozilla Wiki](https://wiki.mozilla.org/Firefox/CommandLineOptions)
