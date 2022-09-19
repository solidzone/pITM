# [pITM  - v1.1.0](https://github.com/JohnKearney1/pITM/releases)
pITM ("Packs In The Mail") is a python email script designed specifically by audio professionals for effective, *informal*, email marketing in the music industry. 
This project seeks to be a no-nonsense, lightweight solution for free, open source e-mail marketing with the bells and whistles, but no frills.

pITM takes in a list of emails and first names, then composes personalized emails using custom templates to reach out to every contact individually.
Using CC and BCC is easy and fast, but largely ineffective in the music industry, as a feeling of *inexclusivity* towards material is discouraging for producers, artists, and engineers.
i.e: When hundreds of audio professionals all get the same email, they immediately realize they were 1/800 people to recieve the same six loops or beats and don't even look at them. This project circumvents that for you.

**WARNING: THIS PROJECT IS A WORK IN PROGRESS USE AT YOUR OWN RISK. BUGS EXIST.**


# Developers: First Time Setup
> 1. Add your [client_secret.json](https://developers.google.com/gmail/api/auth/about-auth) to `pITM/data/auth/`
> > **Note:** Do not edit the contents of the file if you aren't sure what's what.  
> > **Note:** File must be named `client_secret.json`, rename the file if it is not by default.
> 2. Edit the `Contacts.txt` to include your contacts and names
> > **Note:** They should be specified in the format `<email> <firstName>`


## Release Notes - v1.1.0
This version focuses primarily on error handling and logging. I've added logging methods to all three python files to 
print verbose output to `data/log.txt`.

You can log something like this: `log("This will appear in the log with a timestamp!")`

I've also surrounded a good majority of the code in exception handling blocks with log output to help debug issues.
Missing or misconfigured files, connection errors and more are all handled with this update although as more execution 
flow possibilities are discovered more may be added.

I've also updated the templates guide, Readme (duh), and added an example client_secret file for dev purposes.
No API keys are in the example file.

The `data/files/` folder now has some extra logic to skip over any files that begin with a `.` to prevent hidden directories
from being accidentally attached. There are two included test files for dev purposes. 
DO NOT keep any files you DO NOT want attached in this folder during actual usage.

# Architecture

01 pITM/  
02 ├─ data/  
03 │  ├─ auth/  
04 │  │  ├─ client_secret.json  
05 │  │  └─ token.pickle  
06 │  ├─ files/  
07 │  ├─ templates/  
08 │  │  ├─ TEMPLATES GUIDE.md  
09 │  │  └─ Templates.json  
10 │  ├─ Contacts.txt  
11 │  └─log.txt  
12 ├─ README.md  
13 ├─ DOCS.md  
14 ├─ main.py  
15 ├─ Google.py  
16 ├─ templateParser.py  
17 ├─ requirements.txt  
18 ├─ .gitignore  
19 └─ .gitattributes  


## 01 - Root Folder

`pITM/` is the root folder of the project. All directory or file references in the script are *relative* locations
and treat this folder as the root.

## 02 - Data Folder
`data/` stores **user provided** assets the program needs to run. Templates provided.
1. `auth/`  
2. `files/`  
3. `templates/`  
4. `Contacts.txt`  

## 03 - Authorization Folder
`auth/` holds two files:
1. `client_secret.json` (user provided)
2. `token.pickle` (autogenerated)

## 04 - Client Secret (Google Developer Console)

The user must add their own (properly configured) `client_secret.json` file in this folder.
Google Developer Console (get the client_secret): https://console.developers.google.com/start/api?id=gmail.  
For info on the formatting of this file see https://developers.google.com/api-client-library/dotnet/guide/aaa_client_secrets.

The client_secret.json file is your "password" for your initial authentication flow for the Gmail API and OAuth2.
See: https://developers.google.com/gmail/api/auth/about-auth. This allows you to trigger a "consent" screen in the web browser.

## 05 - Credential Cache
`token.pickle` is autogenerated for you provided you have supplied the `client_secret.json`. 
This is a cached credential so you don't have to authenticate every single time.

## 06 - Files Folder
`files/` is a **user populated** folder that holds all the attachments to be assigned to a single email.
i.e. ALL files in this folder will be attached to EVERY email that is sent in a single run. 

**Files have a 24.5mb size limit, and can be of any type.**

## 07 - Templates
`templates/` stores two files that handle and help with crafting your emails.

## 08 - Templates Guide
`TEMPLATES GUIDE.md` is a file that explains the syntax of your templates file, and explains how to write your emails.

## 09 - Templates File
`Templates.json` is a file that holds ALL of your email templates.
A template is a preformatted message and subject that holds some variables that can be changed at runtime.
Do not delete the "default" entry, but you can add as many custom-named templates as you like (CaSE SeNsITivE).

## 10 - Contacts File
`Contacts.txt` holds the email addresses and names of everyone in your contact list arranged in the format:

`<email address>,<name>`

Enter one contact per line, no spaces, comma separated string.

## 11 - log.txt
`log.txt` prints out more verbose console dialouge and full error messages with exact timestamps.
The log only saves the results of the last run, change the filename to something other than `log.txt` to retain the file.


## 12 - Readme
You did it!

## 13 - Docs
`DOCS.md` holds the method APIs for 
1. `main.py`
2. `Google.py`
3. `templateParser.py`

## 14 - main.py

Holds the main logic of the program, user interaction, output etc. Execute program from `main.py`:`main()`

## 15 - Google.py

Custom implementation of a Google class that creates the service necessary to send the email. 
Called from `main.py`:`sendEmail()`.

## 16 - templateParser.py

Holds the logic responsible for pulling templates, substituting in variables, and reading in the `Contacts.txt` file.

## 17 - requirements.txt

`pip install -r dependencies.txt`

This is an incomplete list of dependencies, I haven't implemented setupTools yet for proper dependency mapping,
so you may have to debug. Sorry!

## 18 - Git Ignore (.gitignore)

GitIgnore specifies which directories and files not to pass to Git. 

In this repository, `data/auth/` is excluded for security purposes.

## 19 - Git Attributes (.gitattributes)
Autogenerated file.
