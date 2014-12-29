// Tagger 1.0 
// READ_ME FILE
// Created by Eric F. Johnson
// Date: December 18, 2014

If you are reading this file you have downloaded the Tagger iOS 8 Application. Thank you 
for your interest in this exciting and new developing project. This file will give you 
a brief explanation of how Tagger works, the main classes and their functions, an overview
of the Image-Classification-in-the-Cloud-and-GPU project and how exactly Tagger functions.

^ For installation instructions please see the "Installation Guide" also provided in this 
gitHub repository. Please note that this application is currently in beta and has not been
released to the iOS App Store so you must install it using the .ipa file that was provided
through gitHub. Because the application uses the Facebook API to manage user credentials 
you must be linked as a Facebook Developer account to the Tagger application in order 
your login to the app.  Please note that this is a restriction of the Facebook API and as 
such we are currently managing these requests on a case by case basis. Any application that
uses the Facebook API is managed this way in an effort by Facebook to avoid malicious apps 
from being published outside of the iOS Store.  If you are intersted in using the application
please e-mail us and we can see that you are granted beta access.

// Application Overview
Tagger is designed to replace the standalone iOS Camera application that Apple packages 
inside of its iOS platform. Although currently offered as a standalone application we 
may eventually offer Tagger's core services as an API that can plug into other applications
in the future. 

// Application Design / Functionality
As you can see on our demo video posted during the Big Data conference hosted by Prof. Li 
as well as the demo video posted on our Youtube account Tagger leverages the Caffe framework
to intelligently auto-tag and recommend key textual tags that it believes are related to
the image. Tagger is a front end UI that leverages the advanced Deep Learning technology
developed at UC Berkley. Since all of this is designed to be run on a GPU accelerated system
the actual image feature extraction and classification/clustering is done on a remote server
after the image has been sent via SFTP to the Berkley Image Research Center.  Once Caffe
has returned a recommended set of tags or key words for your image we parse the data and 
show it to you in a iOS app format.  You then select which keywords you believe are relevant 
to the image and can upload your photo to the website.

Since this app is in beta and we did not have sufficient time to run Caffe on our own server
we are using the BIRC server to do the image processing and Caffe analysis. For the next 
semester we plan to use an Amazon Web Service (AWS) implementation of Caffe that we can 
customize to store the results of your image categorization and which words you chose as
most relevant. This will really allow us to expand on the basic functionality of Caffe to
have a crowd-sourced, user feed deep learning system that is currently the main thing Caffe
is lacking.  Our hope is to make it an ad supported free-mium model so that we can help
pay for server costs using the proceeds of the app.  Thanks to the scalability of AWS we may 
not even require a GPU setup but we will still want to look into GPU options offered by AWS 
since the main benefit of a GPU implementation is the speed to the end user - 5-10x faster
turnaround then a CPU.

// introductoryView.h Class
This class manages the introductory screens that show the 4 slides about the Tagger app. 
These slides are managed using a bookmark in the CoreData of the user's phone so they will
only appear if the user is running the application for the first time on the device.  Once
you skip the introduction or complete it you will not be shown the intro again unless 
you delete and reinstall the app for any reason.

// homeProfile.h Class
This class manages the Facebook API and login credentials, prompting users with a 
"Facebook Login" button. Please note that if you have already logged into Facebook on your 
iPhone that these credentials are managed by the phone itself and it will not prompt you
with a login screen as shown in my demo.  This means that if your Facebook account is not
on our list of authorized users you will most likely get an error message.  The best way to 
avoid this would be to get on the approved list before trying to launch the app. 

// selectionPanel.h Class
This class interacts with the camera and photo selection classes to allow the user to either 
pick the camera app or photo library app to upload a picture to Caffe.

// processing.h Class
This class send the photo to the UC Berkley based Caffe instance through a SFTP connection
and listens to parse the resulting webpage that is displayed.  Once parsing the resulting
keywords it displays only the first 4 keywords (most highly) correlated for the user to chose
from. 

// selection.h Class
This page displays the results caught by the processing.h Class and allows the user to 
"Upload" the tags that they select using the radio buttons. The user has the option to 
select anywhere from 0 to 4 tag words that are returned from Caffe. Currently we have
this formatted to use hashtags in the instance of Twitter when uploading images and are 
working around the various API standards required for Facebook and Flickr. 

// Next Steps
As mentioned above this was really designed as a proof of concept.  The next major milestone
for this project will be to get our own AWS based instance of Caffe running and to allow us
to grab and catch those recommendations that the user actually choses to post to social media. 
Once we get this running and are able to publish the app to the Apple iTunes store we think 
that the deep learning technology built into Caffe will show a significant increase in 
accuracy instead of using the static libraries that they currently do for the Caffe demo 
website.  

We look forward to any potential collaboration opportunities out there so please don't 
hesitate to contact me should you be intersted in joining our team or have any feedback 
after joining our beta.  Please feel free to e-mail me at ericjohnson@gmail.com

