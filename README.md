# Show the world your work!
## Topics:
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
* HTTP

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

# Set up your project for deployment
## Project folder and an HTML file
1. Make a project folder.
2. Inside of your project folder, write an .html file which displays a "Hello world!" message, e.g.
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
3. Inside of your project folder, initialize a NodeJS project with the Yarn initialization command:
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
  - You now have a "package.json" file. This file let's tools like `yarn` (or `npm` or `bower`) manage the dependencies ("libraries," "modules") your NodeJS project requires. You can use this file to share your project with other developers. They can use this file to install the dependencies which fit their own development environment. The ".json" file extension indicates that this is a [JSON](https://simple.wikipedia.org/wiki/JSON) file. JSON is an acronym for JavaScript Object Notation. Your "package.json" file should now look something like this:
    ```js
    {
      "name": "DeploymentDemo",
      "version": "1.0.0",
      "description": "ngrok and http-server deployment demo",
      "main": "project_folder/helloWorld.html",
      "repository": "https://github.com/mixelpixel/ngrok_and_http-server.git",
      "author": "Patrick Kennedy",
      "license": "MIT",
      "private": false,
    }
    ```
## Instal NodeJS modules and dependencies for `http-server`
4. Your NodeJS project will _**depend**_ upon it, so add the `http-server` module. NOTE: sorry Windows users, you don't get the icons :(
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
5. Look in your project_folder/node_modules directory. You will see that there is a sub-folder named "http-server." You should also see folders for each of the `http-server` dependencies. These folders and the files within them represent hundreds of programmer hours to add all the functionality `http-server` offers. Wasn't that nice of them? Don't modify the folders and files within the node_modules directory, but do take a moment to examine them. There's useful information in the README files and otherwise there's a bunch of JavaScript you didn't have to write.
## The .lock file
6. You will also notice that you now have a file called "yarn.lock" in your project. This file allows developers to "lock" the versions of dependencies used to develop their project. Similarly, you don't want to modify this file, but do examine it. You will see that the dependencies for `http-server` are listed along with the version you are using, as well as any dependencies those dependencies depend upon. For example:
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
## The package file
7. Lastly, your "package.json" file has been updated with:
  ```js
  "dependencies": {
    "http-server": "^0.11.1"
  }
  ```
## Installing [ngrok(https://ngrok.com)]
8. Download the `ngrok` tool from https://ngrok.com/download
9. The download will deliver a compressed ".zip" file. Within the .zip file is the _binary_, _executable_ program file.
10. Decompress (or "expand") the .zip file.
11. Windows users, take the `"ngrok" file out of the .zip file.
12. You can run the command in your console directly from the directory location of the "ngrok" file, e.g. `$ cd path/to/the/ngrok/file`, i.e.:
  ```console
  $ cd ~/Downloads
  $ ls -l ngrok
      -rwxr-xr-x@ 1 mixelpix  staff  16046668 Jul 15  2017 ngrok
  $ ./ngrok help
  ```
  - NOTE: the x's on the left indicates this is an executable file.
## Your environment, PATH and `grep`
13. Each time you enter a command in your console, these are the directories your computer looks in to see if there is an executable binary whose title matches the text string of the comand name you've entered. Your console operates in an enviroment containnig _lots_ of variables and conditions. You can display your computer's environment variables with the `env` command, but the command will display _a lot_ of stuff. For example:
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

14. For now, we're just interested in the directories available through your environment's "PATH." The PATH is the collection of directories your computer looks in when a command is invoked. To limit the `env` command's return, and only displaying your PATH directories, pipe in a `grep` command. The pipe operator, `|` takes the results from the `env` command and "pipes" them into the `grep` command. The `grep` tool name is an acronym for "Global Regular Expression Print" (but I think of it as, "Get Regular ExPressions.")
15. Piping `env` into a "PATH" `grep`, you should a string of directories separated only by a colon `:`. For example, something like this:
### macOS and Linux users
```console
$ env | grep "PATH"
    PATH=/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/bin
```
### Windows users with GitBash - use `\b` to constrain the grep "boundaries"
```gitbash
$ env | grep "\bPATH"
    PATHEXT=.COM;.EXE;.BAT;.CMD;.VBS;.VBE;.JS;.JSE;.WSF;.WSH;.MSC
    PATH=/c/Users/mixel/bin:/mingw64/bin:/usr/local/bin:/usr/bin:/bin:/mingw64/bin:/usr/bin:/c/Users/mixel/bin:/c/Windows/system32:/c/Windows:/c/Windows/System32/Wbem:/c/Windows/System32/WindowsPowerShell/v1.0:/c/Program Files/nodejs:/c/Program Files (x86)/Yarn/bin:/cmd:/c/Users/mixel/AppData/Local/Microsoft/WindowsApps:/c/Users/mixel/AppData/Roaming/npm:/c/Users/mixel/AppData/Local/Yarn/bin:/c/Program Files/Microsoft VS Code/bin:/c/Program Files/MongoDB/Server/3.6/bin:/c/Users/mixel/bin:/usr/bin/vendor_perl:/usr/bin/core_perl
```
15. The left to right order is the order your computer looks in. As soon as it finds a match, the binary file is executed (and given any additional arguments you entered with the command).
## Copy or move the "ngrok" binary file to one of these directories.
### macOS, Linux and GitBash users can now verify the installation of the ngrok progam:
17. Like so:
  ```console
  $ ngrok --version
      ngrok version 2.2.8
  ```
### Windows users with CMD or Powershell
18. You'll need to make sure the PATH to the "ngrok" binary file is available in your Advanced System Settings Environmental Variables.
  - Click on the Window icon (lower left).
  - Type "sdvanced system settings".
  - Click the "View Advanced System Settings" Control Panel icon.
  - Select "Environmental Variables."
  - Select PATH from the User Variables list (top half, NOT the System Variables on the bottom).
  - Select "Edit"
  - Is the path to the directory where you put the ngrok executable binary file in this list?
  - If so, then close the Environmental Variables and System Properties windows.
  - If not, then select "New" and add the directory.
  - NOTE: GitBash displays Windows directory paths differently than Windows. For example, in GitBash /c/Users/mixel/bin/ is the equivalent of C:\Users\mixel\bin\ in Windows. In the Advanced System Settings dialogue, to add a new path, use the Windows syntax.
  - Now that the ngrok file can be found through your PATH, the ngrok command is available to CMD and Powershell.
  - CMD:
  ```dosbatch
  C:\Users\mixel>ngrok --version
      ngrok version 2.2.8
  ```
  - Powershell:
  ```posh
  PS C:\Users\mixel> ngrok --version
      ngrok version 2.2.8
  ```

# Deploy with `ngrok` and NodeJS `http-server`
19. Use the [`npx`](https://github.com/zkat/npx) command to serve up the project on a local port. The `npx` tool gets installed with the NodeJS installation.
  ```console
  $ npx http-server
      npx: installed 23 in 5.588s
      Starting up http-server, serving ./
      Available on:
        http://127.0.0.1:8080

        http://192.168.88.236:8080
      Hit CTRL-C to stop the server
  ```
20. Make note of the port number, and in another console, feed it to ngrok's http method:
  ```console
  $ ngrok http 8080
  ```
21. You should see something like this:
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
22. Congratulations, you are serving up your HTML file to the world!
23. Copy one of the "Forwarding" URLS, e.g. `https://202c6e30.ngrok.io`
24. Paste the URL into your browser to see how it looks from the world wide web.
25. Share with your friends :)
26. Note that as people visit your website, ngrok will display information about the HTTP requests being made.
27. Your HTML page is now visible at this URL: https://202c6e30.ngrok.io/project_folder/helloWorld.html
28. Add another header element to your HTML file and save the file.
29. Did your web page update on the fly? How cool is that!!

#### Other Deployment Options
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
