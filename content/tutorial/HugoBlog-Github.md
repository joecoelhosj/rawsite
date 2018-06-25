---
title: "Blog using Hugo on Github"
date: 2018-06-24T16:59:11-05:00
draft: false
index: true
tag: "tutorial"
---

### How to Create a Personal Blog on Github using Hugo

Github is a popular free static hosting service for personal and project pages. Hugo is a framework for building websites. More information about Hugo can be got at https://gohugo.io/hosting-and-deployment/hosting-on-github/

The Hugo website also has instructions for creating a personal website on Github. Instructions can be got here https://gohugo.io/hosting-and-deployment/hosting-on-github/

### Step 1: Download Resources and Setup Directories
	
* Download and intall Git (https://gitforwindows.org/)

* Sign up for a Github account
* Create a \<BLOG\> repository on Github. This repository will contain Hugo's content and other source files.
* Create a \<USERNAME\>.github.io repository. This repository will hold the fully rendered version of the Hugo website.
* Instructions for downloading and installing Hugo can be found at https://gohugo.io/getting-started/installing/#windows
	
Directory Structure:

```
\Hugo
  |
  |--- bin (contains the Hugo executable)
  |--- Sites
         |--- <BLOG> (contains the blog)
         	    |--- themes (contains the theme folder)
         	    |--- public (the rendered version of the blog)

```
* (at the command prompt, change directory 'Sites')
* Give the following command:
```
hugo new site <BLOG>
```

* Change directory to \<BLOG\> directory
* Edit the config.toml file so that
		baseurl = "https://\<USERNAME\>.github.io/"
    theme = "hugo-geo"
    themesdir = "./themes/"
* Edit other parameters as necessary
* Initialize the folder for Git use
```
git init
```

### Step 2: Download Theme and Clone Repositories

* Set the \<BLOG\> repository as origin. (The BLOG clone-link is generally https://github.com/<USERNAME>/<BLOG>.git)
```
git remote add origin <HTTPS BLOG clone-link>
```

* Clone a theme for the blog. (I am using the hugo-geo theme for this example)

```
git clone https://github.com/alexurquhart/hugo-geo.git themes\hugo-geo
```

* In the \<BLOG\>/content folder create a file named about.md with the following content:
    +++
    date = "2018-06-17T08:00:00-06:00"
    draft = false
    title = "About"
    +++
    # Welcome
    Welcome to this test site.

* Map the \<USERNAME\>.github.io repository to the 'public' folder which contains the rendered pages. The clone-link will be https://github.com/\<USERNAME\>/\<USERNAME\>.github.io.git
```
git submodule add <HTTPS clone-link> public
```

### Step 3: Configure the Theme

* You will find information about configuring the theme at https://github.com/alexurquhart/hugo-geo

### Step 4: Creating Posts or Tutorials

* You can call Hugo to create blank posts or tutorials which can then be edited
```
hugo new post/<filename>.md

```
```
hugo new tutorial/<filename>.md
```
The files will be created in the 'post' / 'tutorial' folders within the 'content' folder.

### Step 5: Rendering the Pages and Updating Github repositories.

* The following commands may be saved in a batch file (.BAT) and run every time new posts have been written. (This batch file is to be saved in the 'Hugo\Sites' directory.)
```
cd <BLOG>
git add .
git commit -m "Update blog"
git push -u origin master
..\bin\hugo
cd public
git add .
git commit -m "Update rendered site"
git push -u origin master
cd ..
```

If you encounter errors especially when pushing content first time, change the flag for the 'git push' commands from -u to -f which will force a push. You should not have a problem unless the files have been modified in the Github repository directly online, in which case you will have to use the 'git pull' command to update the files stored locally.
