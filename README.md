# Deploy with `ngrok` and NodeJS `http-server`
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
6.
