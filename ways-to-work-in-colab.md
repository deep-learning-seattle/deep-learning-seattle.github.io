# Ways to work in [Google Colab](https://colab.research.google.com)

## Problem

The huge problem is that in this course you supposed to change the py files.

How would you do it if you are working on your local machine? Easy! You just open py file in your favorite editor. That's It!

How would you do it if your machine in the cloud? Easy! SSH and your favourite editor. Or [%load](https://ipython.readthedocs.io/en/stable/interactive/magics.html#magic-load) magic.

How would you do it if you are in Google Collab? Looks like there are some issues!

%load magic doesn't work. You can't connect to the machine via SSH. Additionally  the kernel doesn't see any files from the GitHub or drive.

## Some ways to slove the problem

### Edit locally, upload manually

You can upload the assignments.zip to the workspace manually. And unpack it there.

This way is kind of slow. But works 100%

### Work through the GitHub
* Put you code base into GitHub repo
* Clone it in the Google Colab. Just put the following code in the cell.
```bash
# Exterminate everything
!rm -fR ./*
!rm -fR ./.git
!rm -fR ./.gitignore
# Clone repo to the current dirrectory. NOTE: We can't do 'git clone' since it can't clone to the non-empty directory
!git init
!git remote add origin https://github.com/deep-learning-seattle/cs231n-assignment_1.git
!git pull origin master
```
* clone the repo locally and edit locally
* push your changes
* Pull in Colab environment everytime you pushed
```bash
!git pull origin master
```

### Work through Google Drive
Map your Google Drive locally by executing following commands
```bash
sudo add-apt-repository ppa:alessandro-strada/ppa
sudo apt-get update
sudo apt-get install google-drive-ocamlfuse
mkdir drive
google-drive-ocamlfuse drive
```
This should prompt for acccess to your Google Drive.

Create Auth Token in you Google Console
* Go to https://console.cloud.google.com
* Create new project. Let's say "Colab"
* Open "Google Drive API"
* On the left open credentials, click Create
* Create OAuth client ID credetials of type "Other"
* Save your client ID and secret for the next step

Map your Google Drive in the Colab.
* Put all you files into google Drive.
* Open notebook in Collab.
* Execute following code in the cell:
```bash
!mkdir -p drive
!add-apt-repository ppa:alessandro-strada/ppa
!apt-get update
!apt-get install google-drive-ocamlfuse
# This will give you auth link. Please follow the instructions.
!google-drive-ocamlfuse -headless -label drive -id %YOUR ID%.apps.googleusercontent.com -secret %YOUR SECRET%
!google-drive-ocamlfuse -label drive drive
%cd /content/drive/Colab Notebooks/assignment1
```

Change files locally, and your changes will be reflected in Colab in a couple seconds.

BUT. This works till some moment. Then you'll see that file you've changed locally has different name (the original name + some hash).
Looks like the is a bug in fuse or Colab kernel locks the file, or whatever. But at this moment you need to reset the kernel and reinitialize again. Doh!

