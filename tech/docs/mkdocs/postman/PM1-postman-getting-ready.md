---
title: Getting ready with Postman 
---

First you need to install a copy of the API runner application
**Postman** (Chrome/MacOS/Windows) [Get Postman Application](http://getpostman.com)

This lets you send and receive data from the openEHR REST API or Better Ehrscape API without the need for a specific programming language.

Postman also allows you to import a preset collection of API calls which we can use to supply a copy of the Ehrscape API and associated 'environment' file, which contains settings for a specific C4H Platform domain
domain.

# A. Run Postman

Click the 'Run Postman Button' to import the Postman 'Apperta C4H openEHR REST APIs' collection and the associated 'dhi-scotland' environment.

[![Run in Postman](https://run.pstmn.io/button.svg)]({{cdr.postmanLink}})

# or B. Download Postman files from Git

Click on these links to download the files to your system:

  TBD

# or C. Download your collection files from email

If you have received an email containing the collection and environment files to use with Postman. The first step is to download these files ready to then be imported into Postman.

Find `Apperta C4H openEHR REST API.postman_collection` in
your email and download it to a folder of your choice (normally the
Download folder).

Find `<your_environment_name>.postman_environment` in your email and
download it to a folder of your choice (normally the Download folder).
Please note that for demonstration purposes we are using the `C4H Ripple
OSI` environment in this document.

# Import Downloaded files into Postman

If you have downloaded files from Github of from your email, these now need to be installed in Postman.

Open Postman and select **Import**

![Import Files into Postman](/images/ImportFilesIntoPostman.jpg)

Locate your two save files and import them. You can either use the
**Choose Files** option to import one at a time or drag and drop the files into the window

![Drop Files into Postman](/images/DropFilesInPostman.jpg)

In the top right hand corner, change the environment to your environment (in the screenshot below that’s the C4H Ripple OSI environment)

![Change environment](/images/SelectEnvironment.jpg)

On the left hand side you can now see the collection files ...

![Collection](/images/postman-collection.png)
