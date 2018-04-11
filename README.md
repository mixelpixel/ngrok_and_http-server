# Show the world your work!
##### Topics:
1. Git repository
2. Git ignore file
3. GitHub Flavored Markdown
4. HTML
5. Initializing NodeJS projects with Yarn
6. Adding NodeJS modules with `yarn add`
7. Dependency management with a "package.json" file
8. Dependency and version locking with a ".lock" file
9. Ngrok
10. Accessing binary executables through your environments PATH
11. Global Regular Expression Print

# What's going on here?
1. This Git repository comes with a README.md file, a .gitignore file and a .git folder (which may be hidden from your view by your operating system). The .gitignore file lists things which might populate your project, but which do not need to be sent up to GitHub. For example, we will be installing NodeJS modules. The directory these modules live in don't need to get sent to GitHub. We use the ".gitignore" file to tell the Git repository to ignore them, i.e. to _**not**_ track these files and directories. Note that the .gitignore file lives on the "parent" level of the project and gets applied to sub-folders.
2. The README.md is written in "markdown" format. In particular, it is written with "GitHub Flavored Markdown" (GFM - and yes, there are lots of markdown flavors). The ".md" indicates to GitHub that when displaying the page, it should be rendered according to markdown syntax rules. GitHub is also kind enough to look for files named "README.md" and display them with the GitHub repository's main page. Your text editor likely has a "Markdown Preview" option

# Set up your project for deployment
1. Make a project folder.
2. Inside your project folder, write an .html file which displays a "Hello world!" message, e.g.
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
3. Inside your project folder, initialize a Node project with the Yarn initialization command:
  ```console
  $ yarn init
      yarn init v1.5.1
      question name (project_folder): DeploymentDemo
      question version (1.0.0): 1.0.0
      question description: ngrok and http-server deployment demo
      question entry point (index.js): project_folder/helloWorld.html
      question repository url:
      question author: Patrick Kennedy
      question license (MIT): MIT
      question private: nope
      success Saved package.json
      ✨  Done in 89.54s.
  ```
  - You now have a "package.json" file. This file let's tools like `npm` or `yarn` keep track of the dependencies ("libraries," "modules") your project requires. You can use this file to share your project with other developers. They can use this file to install the dependencies which fit their development environment. The ".json" file extension indicates that this is a [JSON](https://simple.wikipedia.org/wiki/JSON) file. JSON is an acronym for JavaScript Object Notation. Your "package.json" file should now look something like this:
    ```json
    {
      "name": "DeploymentDemo",
      "version": "1.0.0",
      "description": "ngrok and http-server deployment demo",
      "main": "project_folder/helloWorld.html",
      "author": "Patrick Kennedy",
      "license": "MIT",
      "private": null,
    }
    ```
4. Add the `http-server` module
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
5. Look in the project_folder/node_modules folder. You will see that there is a folder named "http-server." You should also see folders for each of the `http-server` dependencies. These folders and the files within them represent hundreds of programmer hours to add all the functionality `http-server` requires. Wasn't that nice of them? Don't modify these files, but do take a moment to examine them. There's useful information in the README files and otherwise just a bunch of JavaScript you didn't have to write. You will also notice that you now have a file called "yarn.lock" in your project. This file allows developers to "lock" the versions of dependencies used to develop their project. Similarly, you don't want to modify this file, but do examine it. You will see that the dependencies for `http-server` are listed along with the version you are using, as well as any dependencies those dependencies depend upon. Lastly, your "package.json" file has been updated with:
  ```json
  "dependencies": {
    "http-server": "^0.11.1"
  }
  ```
6. Install the `ngrok` tool from https://ngrok.com/download
7. This will download the _binary_, _executable_ program file. The download will deliver a compressed ".zip" file
8. Decompress (or "expand") the .zip file.
9. Windows users, take the `"ngrok" file out of the .zip file.
10. You can run the command in your console directly from the directory location of the "ngrok" file, e.g. `$ cd path/to/the/ngrok/file`, i.e.:
  ```console
  $ cd ~/Downloads
  $ ls -l ngrok
      -rwxr-xr-x@ 1 mixelpix  staff  16046668 Jul 15  2017 ngrok
  $ ./ngrok help
  ```
  - NOTE: the x's on the left indicates this is an executable file.
11. macOS and linux users, you can display your computer's environment variables with the `env` command. This will display a bunch of stuff. To limit the `env` command return to only displaying your PATH directories, pipe in a `grep` command. The `grep` tool name is an acronym for "Global Regular Expression Print" but I think of it as, "Get Regular ExPressions". Using `grep` with `env` you should see somthing like this:
  ```console
  $ env | grep "PATH"
      PATH=/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/bin
  ```
  - Each time you enter a command in your console, these are the directories your computer looks in to see if there is an executable binary whose title matches the text string of the comand name you've entered. The left to right order is the order your computer looks in. As soon as it finds a match, the binary file is executed (and given any additional arguments you entered with the command).
  - Add the "ngrok" binary file to one of these directories.
12. Windows users,

# Deploy with `ngrok` and NodeJS `http-server`

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
