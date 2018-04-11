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
4.
