
import os
import sys

from pyicloud import PyiCloudService

def upload(path, apidir):

    curFolder = os.path.basename(path)
    print("Current folder: {}".format(curFolder))

    # First, we need to check if the folder exists in the drive, and then move into it
    # List of all files/folders in the current apifolder
    files = apidir.dir()

    if curFolder not in files:
        apidir.mkdir(curFolder)
        print("Created folder {} in iCloud".format(curFolder))

    # Move into the current folder
    apidir = apidir[curFolder]

    files = apidir.dir()

    # Loop through all folders within the local folder
    # If there is another folder, recurse, otherwise upload the file
    for filename in os.listdir(path):
        if os.path.isdir(os.path.join(path, filename)):
            upload(os.path.join(path, filename), apidir)

        # If the file is not already in the iCloud, upload it
        elif filename not in files:
            with open(os.path.join(path, filename), 'rb') as file:
                apidir.upload(file)
                print("Uploaded file: {}".format(filename))

                file.close()
            
if __name__ == "__main__":

    user = input("Enter iCloud username: ")
    password = input("Enter iCloud password:")

    api = PyiCloudService(user, password)

    if api.requires_2fa:
        code = input("Enter the 2fa code: ")
        result = api.validate_2fa_code(code)
        
        if not result:
            print("Failed to 2fauthenticate. Exiting.")
            exit(1)

        if not api.is_trusted_session:
            print("Requesting trusted session...")
            result = api.trust_session()
            print("Session trust result {}".format(result))

    print("Succesfully logged in.")

    upload(sys.argv[1], api.drive)
