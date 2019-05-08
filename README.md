# React and Electron JS App
> :rocket: :telescope: An easiest way to get started with the most powerful blend of <a target="_blank" href="https://reactjs.org/">React<a/> and <a target="_blank" href="https://electronjs.org/">Electron JS</a> for building Stateful and Native Desktop(Installed) Application for Windows, Linux and macOS using <a target="_blank" href="https://github.com/electron-userland/electron-builder">Electron Builder</a>.

<h3>Use this boilerplate:</h3>

```cmd
git clone https://github.com/soulehshaikh99/create-react-electron-app.git
cd create-react-electron-app

yarn install
yarn global add concurrently wait-on electron electron-builder
    or
npm install
npm i -g concurrently wait-on electron electron-builder
```

**Note:** If you wish to use npm over yarn then modify package.json by replacing 'yarn' with 'npm' in electron-dev and preelectron-pack scripts.
But I strongly recommend using <em>yarn</em> as it is a better choice when compared to <em>npm</em>.

<h3>Scripts Instructions:</h3>

**1) For running app in development mode**

```cmd
yarn run electron-dev
        or
npm run electron-dev
```

**2) For packaging app using electron-builder**

```cmd
yarn run electron-pack
        or
npm run electron-pack
```

<h3>Manual Setup using <a href="https://github.com/facebook/create-react-app">CRA</a>(create-react-app)</h3>

**1) First Create React App**

```cmd
yarn create react-app create-react-electron-app
                    or
npx create-react-app create-react-electron-app
```

**2) Change directory to that project folder**

```cmd 
cd create-react-electron-app
```

**3) Install electron and typescript as development dependency**

```cmd 
yarn add --dev electron typescript
            or
npm install --save-dev electron typescript
```

**4) Create .env file to write React Advance Configuration**

```cmd
// Windows Users
notepad.exe .env

// Linux and macOS Users 
touch .env
```

**5) Paste this line of code in .env file to disable opening react development output in browser**
```text
BROWSER=none
```

**6) Create electron.js file in public directory**

```cmd
// Windows Users
notepad.exe public\electron.js

// Linux and macOS Users
touch public/electron.js
```

**7) Paste this code in electron.js file**

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
        },
        icon: `${path.join(__dirname, 'favicon.ico')}`,
        show: false
    });

    // This block of code is intended for development purpose only.
    // Delete this entire block of code when you are ready to package the application.
    if(!app.isPackaged) {
        mainWindow.loadURL('http://localhost:3000/');
    } else {
        //Do not delete this statement, Use this piece of code when packaging app for production environment
        mainWindow.loadFile(`${path.join(__dirname, '../build/index.html')}`);
    }

    // Open the DevTools and also disable Electron Security Warning.
    // process.env['ELECTRON_DISABLE_SECURITY_WARNINGS'] = true;
    // mainWindow.webContents.openDevTools();

    // Emitted when the window is closed.
    mainWindow.on('closed', function () {
        // Dereference the window object, usually you would store windows
        // in an array if your app supports multi windows, this is the time
        // when you should delete the corresponding element.
        mainWindow = null
    });

    // Emitted when the window is ready to be shown
    // This helps in showing the window gracefully.
    mainWindow.once('ready-to-show', () => {
        mainWindow.show()
    });
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

**8) Move dependencies react, react-dom and react-scripts to devDependencies as they are not needed in production build.
Your devDependencies section should look like this**

```json
"devDependencies": {
    "electron": "^5.0.1",
    "react": "^16.8.6",
    "react-dom": "^16.8.6",
    "react-scripts": "3.0.0",
    "typescript": "^3.4.5"
}
```

**9) Install necessary global packages**

```cmd
yarn global add concurrently wait-on electron electron-builder
            or
npm i -g concurrently wait-on electron electron-builder
```

**10) Add electron-dev, preelectron-pack and electron-pack scripts. Make sure your scripts section in package.json looks like this**

```json
"scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject",
    "electron-dev": "concurrently \"yarn start\" \"wait-on http://localhost:3000 && electron .\"",
    "preelectron-pack": "yarn build",
    "electron-pack": "build"
}
```

**11) Add the following configuration in package.json**

**Note:** build configuration is used by electron-builder, modify it if you wish to add more packaging and native distribution options for different OS Platforms.
```json
"main": "public/electron.js",
"homepage": "./",
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

**Result**

![Result](https://user-images.githubusercontent.com/39525716/57184177-102d3b80-6ed5-11e9-9af6-828e853632a5.PNG)

<h3>Made with :heart: from Souleh</h3>

<h3>:clipboard: License: </h3>
Licensed under the <a href="https://github.com/soulehshaikh99/create-react-electron-app/blob/master/LICENSE">MIT License</a>.
