# React and Electron JS App
> :rocket: :telescope: An easiest way to get started with the most powerful blend of React and Electron JS for building Stateful and Native Desktop(Installed) Application for Windows, Linux and macOS using <a href="https://github.com/electron-userland/electron-builder">Electron Builder</a>.

1) First Create React App:

```cmd
npx create-react-app my-react-electron-app
                    or
yarn create react-app my-react-electron-app
```

2) Now change directory to that project folder:

```cmd 
cd my-react-electron-app
```

3) Now install typescript as development dependency:

```cmd 
npm install --save-dev typescript
            or
yarn add --dev typescript
```

4) Now install electron as as development dependency:

```cmd
npm install --save-dev electron
            or
yarn add --dev electron
```

5) Now create electron.js file in public directory<br/>

a) Windows Users:
```cmd
notepad.exe public\electron.js //Windows Users
                or
touch public/electron.js //Linux and macOS Users 
```

6) Now paste this code in electron.js file:
```javascript
// Modules to control application life and create native browser window
const {app, BrowserWindow} = require('electron');
const path = require('path');

// Keep a global reference of the window object, if you don't, the window will
// be closed automatically when the JavaScript object is garbage collected.
let mainWindow;

function createWindow () {
    // Create the browser window.
    mainWindow = new BrowserWindow({
        width: 800,
        height: 600,
        webPreferences: {
            nodeIntegration: true
        }
    });

    // and load the index.html of the app.
    mainWindow.loadFile(`${path.join(__dirname, '../build/index.html')}`);

    // Open the DevTools and also disable Electron Security Warning.
    // process.env['ELECTRON_DISABLE_SECURITY_WARNINGS'] = true;
    // mainWindow.webContents.openDevTools()

    // Emitted when the window is closed.
    mainWindow.on('closed', function () {
        // Dereference the window object, usually you would store windows
        // in an array if your app supports multi windows, this is the time
        // when you should delete the corresponding element.
        mainWindow = null
    })
}

// This method will be called when Electron has finished
// initialization and is ready to create browser windows.
// Some APIs can only be used after this event occurs.
app.on('ready', createWindow);

// Quit when all windows are closed.
app.on('window-all-closed', function () {
    // On macOS it is common for applications and their menu bar
    // to stay active until the user quits explicitly with Cmd + Q
    if (process.platform !== 'darwin') app.quit()
});

app.on('activate', function () {
    // On macOS it's common to re-create a window in the app when the
    // dock icon is clicked and there are no other windows open.
    if (mainWindow === null) createWindow()
});

// In this file you can include the rest of your app's specific main process
// code. You can also put them in separate files and require them here.
```

7) Move dependencies react, react-dom and react-scripts to devDependencies as they are not needed in production build.
Your devDependencies section should look like this:

```json
"devDependencies": {
    "electron": "^5.0.1",
    "react": "^16.8.6",
    "react-dom": "^16.8.6",
    "react-scripts": "3.0.0",
    "typescript": "^3.4.5"
}
```

8) Add electron-dev, preelectron-pack and electron-pack scripts. Make sure your scripts section in package.json looks like this:

```json
"scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject",
    "electron-dev": "yarn run build && electron .",
    "preelectron-pack": "yarn build",
    "electron-pack": "build"
}
```

9) Add the following configuration in package.json:

```json
"main": "public/electron.js",
"homepage": "./"
```

10) Add build configuration for electron-builder to work properly:

```json
"build": {
    "productName": "React and Electron App",
    "files": [
      "build/**/*"
    ],
    "extraMetadata": {
      "main": "build/electron.js"
    }
}
```

<h3>Made with :heart: from Souleh</h3>

<h3>:clipboard: License: </h3>
Licensed under the <a href="https://github.com/soulehshaikh99/create-react-electron-app/blob/master/LICENSE">MIT License</a>.
