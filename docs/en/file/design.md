# Design Principle

In JSBox we provided a lot of APIs to store/fetch files, in order to save files to disk, for example downloaded files.

As you know, iOS has an awesome mechanism called `Sandbox`, it makes each application independent.

JSBox has this ability as well, it sounds like `Sandbox in Sandbox`, it makes each script has its own file zone.

So, a script can't access all paths, it's limited, and JSBox hides all details to script developers. It is very safe and convenient.

# Shared Folder

Other than sandboxes, JSBox also provided a special folder can be shared by all scripts.

To use this folder, just use file path starts with `shared://`.

Please note all contents in this folder could be modified by all scripts.

# iCloud Drive

In addition, file system also supports read/write files in iCloud Drive Container.

To use this folder, just use file path starts with `drive://`.

Please note this folder doesn't work if user didn't turn on iCloud Drive for JSBox.

# Inbox

One more thing, all files imported by share sheet or AirDrop will be placed in a special folder.

To use this folder, just use file path starts with `inbox://`.

Please note all contents in this folder could be modified by all scripts.