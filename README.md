# iCloud-Drive-Folder-Uploader

Python script to upload a folder and all of its contents to the iCloud Drive. 
Can be configured to run at startup to automatically backup specific folders. 

It requres https://pypi.org/project/pyicloud/
Replace drive.py in the pyicloud library with the fixed drive.py from this repo as there were a few problems with the original.
The drive.py in this library has an error where it submits the full file path to the iCloudDrive, fixed by submitting only the filename and extention.
Another problem is when mkdir() is called on a DriveNode, it's children folders do not update with the new folder.

I scheduled this script to run at startup and hardcoded the inputs.
