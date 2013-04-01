# WordPress Android Media Publication Platform #
This is a free platform that allows organisations and societies that produce newspapers, magazines and other printed media
with articles to easily customize a pre-built Android application that grabs articles(posts) published on their WordPress
website.

## Requirements ##
As mentioned above, a WordPress CMS website is required. Access to the server the website and corresponding database for
the website is also required, as a server-side python application is requred to be installed and run to respond to Android
application requests.


## Note ##
For installation and customisation instructions plese see the Documentation folder.
The application is pre-configured as an example for Trinity College Dublin's student newspaper, the University Times.

This platform was developed by Computer Science Students taking module CS3013.
Original authors:

@k3ypad - Server-side python application, infrastructure, installation script + documentation

@dwyerci - Back-end for Android application, documentation

@EoinHiggins  - Back-end for Android application

@guwere  - General design + Back-end for Android application

@bungleofsketches  - Front-end design and implementation

@matthiasgh - Front-end design and implementation

##Server Installation##


There is a script for installing the server - side application.

The basic flow of the script is as follows:

1. Ensure Python is installed.

2. Copy the application to /etc/WPAMP.

3. Run the application in a screen session.

To begin run these commands each line is a separate command:

git clone https://github.com/k3ypad/UTAndroidApp.git

cd UTAndroidApp
sh install.sh


## Installing and Setting up of Wordpress##

###Step 1: Download and Unzip the File###

Download and unzip to your computer from http://wordpress.org/download/. If downloading to a remote web server, download and unzip to your computer with a web browser.

###Step 2: Create the Database and a User###

If you are using a hosting provider, there may be either a WordPress database already set up, or an automated setup solution to do so. 
If you need to make one manually and downloading WordPress to your own server you can create one easily by running mysql from the console by following these instructions:

$ mysql -u adminusername -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 5340 to server version: 3.23.54

Type 'help;' or '\h' for help. Type '\c' to clear the buffer.

mysql> CREATE DATABASE databasename;
Query OK, 1 row affected (0.00 sec)

mysql> GRANT ALL PRIVILEGES ON databasename.* TO"wordpressusername"@"hostname"
   -> IDENTIFIED BY "password";
Query OK, 0 rows affected (0.00 sec)

mysql> FLUSH PRIVILEGES;
Query OK, 0 rows affected (0.01 sec)

mysql> EXIT
Bye
$


###Step 3: Set up wp-config.php###

You can choose to edit the wp-config.php file yourself or skip this step and let WordPress try to do it itself when you running the installation script. 
You will need to return to step 1 if you choose to edit it yourself and change the file name from wp-config-sample.php to wp-config.php and open it in a text editor.
Following these steps will show show how to edit it correctly

** The name of the database for WordPress */

define('DB_NAME', 'Database name from step 2');

/** MySQL database username */

define('DB_USER', 'Username from step 2');

/** MySQL database password */

define('DB_PASSWORD', 'Password from step 2');

/** MySQL hostname */

define('DB_HOST', 'localhost');

Save the wp-config.php file and continue.

###Step 4: Upload the files###

You will now have to choose where on your domain your WordPress powered-site will appear. 
If you choose to have it as a root directory you will need to upload your files to the web server and use and FTP client to upload all the contents of the directory, but not the directory itself, into the root directory. 
If they are already uploaded and are using console to install WordPress, move the contents to the wordpress directory.
If you choose to use a Subdirectory you need to upload your files to the web server, then rename the wordpress directory to what you would like. 
Use a FTP client to upload the directory to the desired location. If the files are already uploaded follow the same steps as above.


###Step 5: Run the WordPress Install Script###
If you placed the WordPress files in the root directory, you should visit: http://example.com/wp-admin/install.php
If you placed the WordPress files in a subdirectory called blog, for example, you should visit: http://example.com/blog/wp-admin/install.php

##Setting up the SDK (Android Development Kit)##

###Step 1: Downloading the android SDK###
You will need a computer with an unzipper program to follow these instructions. 
7zip is a free (as in speech) windows unzip program that I use.
Download the sdk from the link below. Install instructions are included below. 
It comes in a compressed portable executable. Unpack it to a folder of your choice. remember that choice.

http://developer.android.com/sdk/index.html

###Step 2: Downloading the University Times App###
Download the University Times App Project from the link below. This involves downloading a .zip from the link and unpacking it from from the .zip using a program like 7zip to a file location of your choice.
Remember that choice.

https://github.com/k3ypad/UTAndroidApp

###Step 3: Running the UT App in Eclipse###

Open up the SDK by opening the ADT-Bundle folder, opening the eclipse folder and launching the portable executable. Once in you will choose a workspace, make it anywhere you want.
Now when you are in the IDE go to file, import and navigate to where you unzipped the UTAndroidApp folder. 
Click on the android app folder and select ok. Then click on the MainActivity project that should be listed, tick copy the contents, and clcik import. 
It should be listed in the project overview tab on the left. Select it and go to to Project->Clean. Also run it in an emulator to make sure it works.
Check the Android.dev website for emulator help.

###Step 4: Editing the Functional Code###
The first section of code, and the only functional change, is the connection to your server.
This is in the ArticleManager class on line 78. Where it says “tfa.dummy.ie” swap with your Wordpress server address. 
The App should now show articles from your server in the home view.


##Aesthetics##

There are a few basic aesthetics that must be changed to make your app shippable at the most basic levels. The first is your app icon.
If you open the Android manifest and go to the Application tab at the bottom you can change the icon from there.
The next and most important part is changing the relationship with Tags. The first is changing Overview to show the tags and sections you want. Change the names and tags to actual tags on your server. 
This App will then sort it for you. This will also have to be edited in the main class and in the overview.xml so take your time and edit thoughtfully.
The more lighthearted aesthetics can be changed easily, the main Article buttons can be changed via the Java in MainActivity.
The Overview (Sections) Buttons can be edited via the overview.xml. If you want to change a particular characteristic it’s easiest to Google it.
