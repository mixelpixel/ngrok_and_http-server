# Show the world your work!
## Overview
This document goes into detail about how to set up your computer and use the tools you have to deploy an HTML file to the world wide web. In short, the commands are "simple." You'll serve up your webpage on your computer's "localhost" with a tool that was included when you installed NodeJS: [`npx`](https://github.com/zkat/npx). We'll also set up a NodeJS project and use the [http-server](https://www.npmjs.com/package/http-server) module. The port number used with the localhost gets fed to a tool we'll set up as a command in your console: [ngrok](https://ngrok.com). Once your system is configured, it takes two commands:
```console
$ npx http-server
```
and:
```console
$ ngrok http 8080
```
## Index
1. [What's going on here?](#whats-going-on-here)
2. [Set up your project for deployment](#set-up-your-project-for-deployment)
3. [Install NodeJS modules and dependencies for `http-server`](#install-nodejs-modules-and-dependencies-for-http-server)
4. [Installing ngrok](#installing-ngrok)
5. [Deploy with `http-server` and `ngrok`](#deploy-with-http-server-and-ngrok)
6. [Other Deployment Options](#other-deployment-options)
## Topics:
* localhost
* PORT
* Git repository
* Git ignore file
* GitHub Flavored Markdown
* HTML
* Initializing NodeJS projects with Yarn
* Adding NodeJS modules with `yarn add`
* Dependency management with a "package.json" file
* Dependency and version locking with a ".lock" file
* Ngrok
* Accessing binary executables through your environment's PATH
* Global Regular Expression Print
* `npx`
* URL
* HTTP/HTTPS
# What's going on here?
### This Git repository comes with a "README.md" file, a ".gitignore" file, and a ".git" project folder. Note that files and directories whose names begin with a period may be hidden from your view by your operating system. Here's how to see them in [Windows](https://support.microsoft.com/en-us/help/14201/windows-show-hidden-files). In macOS you can toggle the Finder display of invisible files with `cmd`+`shift`+`.`
1. The **README.md** file is written in "markdown" format. In particular, it is written with "[GitHub Flavored Markdown](https://help.github.com/articles/basic-writing-and-formatting-syntax/)" (GFM - one of many markdown flavors!) The ".md" indicates to GitHub that when displaying the page, it should be rendered according to markdown syntax rules. Compare the text in the README>md file to the display of it on GitHub. Pretty neat, huh? GitHub is also kind enough to look for files named "README.md" and display them with the GitHub repository's main page. Your text editor likely has a "Markdown Preview" (Atom) or "Open Preview" (VSC) option. The preview may differ some from what GitHub displays, but they should be in the same ballpark.
2. The **.gitignore** file lists things which might populate your project, but which do not need to be sent up to GitHub. For example, we will be installing NodeJS modules in this project. The directory these modules live in don't need to get sent to GitHub. We use the ".gitignore" file to tell the Git repository to ignore them, i.e. to _**not**_ track these files and directories. Note that the .gitignore file lives on the "parent" level of the project and gets applied to sub-folders. As an example, the list of items in this .gitignore file has the following effect:
  ```config
  .DS_Store        <---- now these macOS system resource files will be ignored
  node_modules     <---- the directory and it's contents will be ignored
  *.sw[a-p]        <---- VIM text editing resources will be ignored
  ```
3. The **.git** folder contains all the resources Git uses to track file changes, e.g. maintaining the history of your commits. Don't modify these files, but do take a moment to look in there and examine the contents:
  ```console
  $ ls -al .git
      total 40
      drwxr-xr-x  13 mixelpix  staff   416 Apr 11 14:14 .
      drwxr-xr-x   7 mixelpix  staff   224 Apr 11 13:37 ..
      -rw-r--r--   1 mixelpix  staff     5 Apr 11 14:14 COMMIT_EDITMSG
      -rw-r--r--   1 mixelpix  staff    23 Apr 11 10:47 HEAD
      drwxr-xr-x   2 mixelpix  staff    64 Apr 11 10:47 branches
      -rw-r--r--@  1 mixelpix  staff   137 Apr 11 10:47 config
      -rw-r--r--   1 mixelpix  staff    73 Apr 11 10:47 description
      drwxr-xr-x  13 mixelpix  staff   416 Apr 11 10:47 hooks
      -rw-r--r--   1 mixelpix  staff   536 Apr 11 14:14 index
      drwxr-xr-x   3 mixelpix  staff    96 Apr 11 10:47 info
      drwxr-xr-x   4 mixelpix  staff   128 Apr 11 10:49 logs
      drwxr-xr-x  66 mixelpix  staff  2112 Apr 11 14:14 objects
      drwxr-xr-x   4 mixelpix  staff   128 Apr 11 10:47 refs
  ```
4. While you are here, open a console and navigate to this project's directory. Enter the command `$ git log` and you will see all the commits I made while building this Git repository. You can press the `space bar` to page through the list. Pressing the `q` key will "quit" the display of the git commit history log and return you to your console.
5. You may have also noticed that **favicon.ico** file. What's all about?

<p align="right"><a href="#index">Index</a></p>

# Set up your project for deployment
## Project folder and an HTML file
6. Inside this project folder, write an HTML file which displays a "Hello world!" message, e.g.
  ```html
  <!DOCTYPE html>
  <html lang="en" dir="ltr">
    <head>
      <meta charset="utf-8">
      <title>NGROK IS COOL!</title> <!-- This will show up in the browser tab - neat! -->
    </head>
    <body>
      <h1>Hello world!</h1>
    </body>
  </html>
  ```
## Initializing a NodeJS project
7. Now initialize a NodeJS project with the Yarn initialization command:
  ```console
  $ yarn init
      yarn init v1.5.1
      question name (project_folder): DeploymentDemo
      question version (1.0.0): 1.0.0
      question description: ngrok and http-server deployment demo
      question entry point (index.js): project_folder/helloWorld.html
      question repository url: https://github.com/mixelpixel/ngrok_and_http-server.git
      question author: Patrick Kennedy
      question license (MIT): MIT
      question private: no
      success Saved package.json
      ✨  Done in 89.54s.
  ```
## The package.json file
8. Having used Yarn to initialize a NodeJS project, you now have a "package.json" file. Right now, it just contains the information you supplied from the initialization questionnaire. The package.json file can do a lot more, but for this exercise, we'll just be using it to make note of the `http-server` pakage we'll add shortly. In a NodeJS project, the package.json file let's tools like `yarn` and `npm` manage the dependencies ("libraries," "modules") your NodeJS project requires. Also, the package.json file let's developers share their projects with other developers. We can use this file to install the dependencies which fit our own particular development environment. Lastly, the ".json" file extension indicates that this is a [JSON](https://simple.wikipedia.org/wiki/JSON) file. JSON is an acronym for JavaScript Object Notation. Your "package.json" file should now look something like this:
  ```json
  {
    "name": "ngrok_and_http-server",
    "version": "1.0.0",
    "description": "demo",
    "main": "index.html",
    "repository": "https://github.com/mixelpixel/ngrok_and_http-server.git",
    "author": "mixelpixel <mixelpix@mac.com>",
    "license": "MIT",
    "private": false
  }
  ```

<p align="right"><a href="#index">Index</a></p>

# Install NodeJS modules and dependencies for `http-server`
9. Your NodeJS project will _**depend**_ upon it, so "add" the `http-server` module.
  ```console
  $ yarn add htpp-server
      yarn add v1.5.1
      info No lockfile found.
      [1/4] 🔍  Resolving packages...
      [2/4] 🚚  Fetching packages...
      [3/4] 🔗  Linking dependencies...
      [4/4] 📃  Building fresh packages...
      success Saved lockfile.
      success Saved 21 new dependencies.
      info Direct dependencies
      └─ http-server@0.11.1
      info All dependencies
      ├─ async@1.5.2
      ├─ colors@1.0.3
      ├─ corser@2.0.1
      ├─ debug@2.6.9
      ├─ ecstatic@3.2.0
      ├─ eventemitter3@1.2.0
      ├─ he@1.1.1
      ├─ http-proxy@1.16.2
      ├─ http-server@0.11.1
      ├─ mime@1.6.0
      ├─ minimist@1.2.0
      ├─ mkdirp@0.5.1
      ├─ ms@2.0.0
      ├─ opener@1.4.3
      ├─ optimist@0.6.1
      ├─ portfinder@1.0.13
      ├─ qs@2.3.3
      ├─ requires-port@1.0.0
      ├─ union@0.4.6
      ├─ url-join@2.0.5
      └─ wordwrap@0.0.3
      ✨  Done in 2.07s.
  ```
  - NOTE: sorry Windows users, you don't get the icons :(
10. Look in the node_modules directory. You will see that there is a sub-folder named "http-server." You should also see folders for each of the `http-server` dependencies. These folders and the files within them represent hundreds of programmer hours to add all the functionality `http-server` offers. Wasn't that nice of them? Don't modify the folders and files within the node_modules directory, but do take a moment to examine them. There's useful information in the README files and otherwise there's a bunch of JavaScript you didn't have to write!
  - NOTE: you could install http-server globally on your system, but this way we get to discuss some aspects of NodeJS you'll be working with a lot in the coming weeks :)
## The yarn.lock file
11. You will also notice that you now have a file called "yarn.lock" in your project. This file allows developers to "lock" the versions of dependencies used to develop their project. This doesn't matter so much for the projects we'll work on in Lambda School, but for big projects with large teams of developers which last a long time, locking in versions is mission critical! Similarly with the files in the node_modules and .git directories, you don't want to modify the yarn.lock file, but do examine it. You will see that the dependencies for `http-server` are listed along with the version you are using, as well as any dependencies those dependencies depend upon. For example:
  ```json
  http-server@^0.11.1:
    version "0.11.1"
    resolved "https://registry.yarnpkg.com/http-server/-/http-server-0.11.1.tgz#2302a56a6ffef7f9abea0147d838a5e9b6b6a79b"
    dependencies:
      colors "1.0.3"
      corser "~2.0.0"
      ecstatic "^3.0.0"
      http-proxy "^1.8.1"
      opener "~1.4.0"
      optimist "0.6.x"
      portfinder "^1.0.13"
      union "~0.4.3"
  ```
## The package.json dependency list
12. Even though a number of modules have been installed in your project, Yarn is smart enough to manage all the dependencies that `http-server` requires. Even though there's a lot of them, your "package.json" file has been updated with just the one we installed:
  ```json
  "dependencies": {
    "http-server": "^0.11.1"
  }
  ```

<p align="right"><a href="#index">Index</a></p>

# Installing ngrok
13. Download the `ngrok` tool from https://ngrok.com/download
14. The download will deliver a compressed ".zip" file. Within the .zip file is the _binary_, _executable_ program file.
15. Decompress (or "expand") the .zip file.
16. Windows users, take the `"ngrok" file out of the .zip file.
17. You can run the command in your console directly from the directory location of the "ngrok" file, e.g. `$ cd path/to/the/ngrok/file`, i.e.:
  ```console
  $ cd ~/Downloads
  $ ls -l ngrok
      -rwxr-xr-x@ 1 mixelpix  staff  16046668 Jul 15  2017 ngrok
  $ ./ngrok help
  ```
  - NOTE: the x's on the left indicates this is an executable file. The `./` tells the console to run the binary file.
## Your environment, PATH and `grep`
18. Each time you enter a command in your console, your console looks for the binary file which corresponds to the command name. Your PATH is a variable in your environment. Your enviroment contains _lots_ of variables. You can display your computer's environment variables with the `env` command. For example:
  ```console
  $ env
      TERM_PROGRAM=Apple_Terminal
      SHELL=/bin/bash
      TERM=xterm-256color
      TMPDIR=/var/folders/gv/jzhl4n_j2gz6_hjvq4f2xq9h0000gq/T/
      Apple_PubSub_Socket_Render=/private/tmp/com.apple.launchd.HkSLiQezds/Render
      TERM_PROGRAM_VERSION=404
      OLDPWD=/Users/mixelpix
      TERM_SESSION_ID=236F6B77-3B9D-4903-A9A4-C72BD0CB5E4C
      USER=mixelpix
      SSH_AUTH_SOCK=/private/tmp/com.apple.launchd.VoWn3sqmt7/Listeners
      PATH=/usr/local/bin:/Users/mixelpix/.rbenv/shims:/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/bin:/usr/local/go/bin:/opt/X11/bin
      PWD=/Users/mixelpix/Desktop/ngrok_and_http-server
      LANG=en_US.UTF-8
      XPC_FLAGS=0x0
      PS1=\# \h \d \t$
      RBENV_SHELL=bash
      XPC_SERVICE_NAME=0
      SHLVL=1
      HOME=/Users/mixelpix
      LOGNAME=mixelpix
      DISPLAY=/private/tmp/com.apple.launchd.glQCmHIFzW/org.macosforge.xquartz:0
      _=/usr/bin/env
  ```

19. For now, we're just interested in the directories available through your environment's "PATH." The PATH is the collection of directories your computer looks in when a command is invoked. To limit the `env` command's return and only display your PATH directories, pipe in a `grep` command. The pipe operator ()`|`) takes the results from the `env` command and "pipes" them into the `grep` command. The `grep` tool name is an acronym for "Global Regular Expression Print" (but I think of it as, "Get Regular ExPressions."). Using the pipe, the `grep` command looks for lines of text which match a pattern.
20. Piping `env` into a "PATH" `grep`, you should a string of directories separated only by a colon `:`. For example, something like this:
### macOS and Linux users
```console
$ env | grep "PATH"
    PATH=/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/bin
```
### Windows users with GitBash - use `\b` to constrain the grep "boundaries"
```posh
$ env | grep "\bPATH"
    PATHEXT=.COM;.EXE;.BAT;.CMD;.VBS;.VBE;.JS;.JSE;.WSF;.WSH;.MSC
    PATH=/c/Users/mixel/bin:/mingw64/bin:/usr/local/bin:/usr/bin:/bin:/mingw64/bin:/usr/bin:/c/Users/mixel/bin:/c/Windows/system32:/c/Windows:/c/Windows/System32/Wbem:/c/Windows/System32/WindowsPowerShell/v1.0:/c/Program Files/nodejs:/c/Program Files (x86)/Yarn/bin:/cmd:/c/Users/mixel/AppData/Local/Microsoft/WindowsApps:/c/Users/mixel/AppData/Roaming/npm:/c/Users/mixel/AppData/Local/Yarn/bin:/c/Program Files/Microsoft VS Code/bin:/c/Program Files/MongoDB/Server/3.6/bin:/c/Users/mixel/bin:/usr/bin/vendor_perl:/usr/bin/core_perl
```
21. The left to right order is the order your computer searches by. As soon as it finds a match, the binary file is executed (and given any additional arguments you entered with the command).
22. Copy or move the "ngrok" binary file to one of the directories in your PATH.
### macOS, Linux and GitBash users can now verify the installation of the ngrok progam and it's availability through their PATH:
23. Like so:
  ```console
  $ ngrok --version
      ngrok version 2.2.8
  ```
### Windows users with CMD or Powershell
24. You'll need to make sure the PATH to the "ngrok" binary file is available in your Advanced System Settings Environmental Variables.
  - Click on the Window icon (lower left).
  - Type "advanced system settings".
  - Click the "View Advanced System Settings" Control Panel icon.
  - Select "Environmental Variables."
  - Select "PATH" from the User Variables list (top half, NOT the System Variables on the bottom).
  - Select "Edit"
  - Is the path to the directory where you put the ngrok executable binary file in this list?
    - If so, then close the Environmental Variables and System Properties windows.
    - If not, then select "New" and add the directory.
  - NOTE: GitBash displays Windows directory paths differently than Windows. For example, in GitBash /c/Users/mixel/bin/ is the equivalent of C:\Users\mixel\bin\ in Windows. In the Advanced System Settings dialogue, to add a new path, use the Windows syntax.
  - Now that the ngrok file can be found through your PATH, the ngrok command is available to CMD and Powershell.
  - You may need to launch a new shell for the new PATH directory to be recognized.
  ```posh
  PS C:\Users\mixel> ngrok --version
      ngrok version 2.2.8
  ```

<p align="right"><a href="#index">Index</a></p>

# Deploy with `http-server` and `ngrok`
25. Use the [`npx`](https://github.com/zkat/npx) command to serve up the project on a local port. The `npx` tool gets installed with the NodeJS installation.
  ```console
  $ npx http-server
      npx: installed 23 in 5.588s
      Starting up http-server, serving ./
      Available on:
        http://127.0.0.1:8080

        http://192.168.88.236:8080
      Hit CTRL-C to stop the server
  ```
26. Make note of the port number. In another console, feed the port number to ngrok's http method:
  ```console
  $ ngrok http 8080
  ```
27. You should see something like this:
  ```console
  ngrok by @inconshreveable                               (Ctrl+C to quit)

  Session Status                online
  Session Expires               7 hours, 57 minutes
  Version                       2.2.8
  Region                        United States (us)
  Web Interface                 http://127.0.0.1:4040
  Forwarding                    http://202c6e30.ngrok.io -> localhost:8080
  Forwarding                    https://202c6e30.ngrok.io -> localhost:8080

  Connections                   ttl     opn     rt1     rt5     p50     p90
                                0       0       0.00    0.00    0.00    0.00
  ```
28. Congratulations, you are serving up your HTML file to the world!
29. Copy one of the "Forwarding" URLS, e.g. `https://202c6e30.ngrok.io`
30. Paste the URL into your browser to see how it looks from the world wide web.
31. Share with your friends :)
32. Note that as people visit your website, ngrok will display information about the HTTP requests being made.
33. Your HTML page is now visible at this URL: https://202c6e30.ngrok.io/project_folder/helloWorld.html
34. Add another header element to your HTML file and save the file.
35. Did your web page update on the fly? How cool is that!!

<p align="right"><a href="#index">Index</a></p>

# Other Deployment Options
- Netlify: https://www.netlify.com/blog/2016/09/29/a-step-by-step-guide-deploying-on-netlify/
- GitHub Pages: https://pages.github.com/
- GH: https://help.github.com/articles/configuring-a-publishing-source-for-github-pages/
- Heroku: https://devcenter.heroku.com/articles/getting-started-with-nodejs#introduction
  - https://devcenter.heroku.com/articles/mongolab
  - https://forum.freecodecamp.org/t/guide-for-using-mongodb-and-deploying-to-heroku/19347
- MLab (for MongoDB hosting): https://mlab.com/signup/?gclid=EAIaIQobChMIrLP4p4Kc2gIVlLjACh0cFgTiEAAYASABEgJyJ_D_BwE
  - MongoDB Atlas: https://www.mongodb.com/cloud/atlas/lp/general
- Digital Ocean: https://www.digitalocean.com/
- Microsoft Azure: https://azure.microsoft.com/en-us/free/search/
- AWS free tier: https://aws.amazon.com/free/
- Google Cloud free tier: https://cloud.google.com/free/
- Python
  - From the command line, `cd` to the directory containing your HTML files and run:
  ```console
  $ python -m SimpleHTTPServer
      Serving HTTP on 0.0.0.0 port 8000 ...
  ```
  - For python3
  ```console
  $ python3 -m http.server
      Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
  ```
  - Then, in another console, run ngrok with the port number python serves up.

# BONUS: favicon.icon
1. Add this link in the head `<head>` section of your HTML file:
  ```html
  <link href="/favicon.ico" type="image/x-icon" />
  ```
2. If it wasn't already showing up, now the favicon.ico file will get displayed in the browser tab for your web page!
3. NOTE: if you named your HTML file, "index.html" ngrok is smart enough to know to display the file.
4. If you change the name of your HTML to something other than "index.html," ngrok will display the directory contents - gve it a try!

<p align="right"><a href="#index">Index</a></p>
