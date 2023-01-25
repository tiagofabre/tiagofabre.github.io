---
layout: post
title:  "Electron"
subtitle:  "Desenvolvendo aplicações que rodam nativamente nos clientes utilizando tecnologias da web"
date:   2016-12-02 20:44 -0300
comments: true
categories: "electron"
tags: "portuguese"
---

É um framework open-source para criar aplicações nativas windows, linux e OSX utilizando tecnologias web (Javascript, HTML e CSS). Por baixo dos panos o Electron combina Node.js e o Chromium em uma única aplicação e surgiu em 2013 e é o framework utilizado para o desenvolvimento do Atom editor e desde então existem muitas aplicações de grandes empresas feitas através do Electron.


### Hello World Electron

Requisitos:

```bash
npm init
npm install electron -g
```

Estrutura do projeto

```
  your-app/
├── package.json
├── main.js
└── index.html
```

 - main.js - Contem a inicialização da window e importa o html para renderização


```javascript
const {app, BrowserWindow} = require('electron')
const path = require('path')
const url = require('url')

// Keep a global reference of the window object, if you don't, the window will
// be closed automatically when the JavaScript object is garbage collected.
let win

function createWindow () {
  // Create the browser window.
  win = new BrowserWindow({width: 800, height: 600})

  // and load the index.html of the app.
  win.loadURL(url.format({
    pathname: path.join(__dirname, 'index.html'),
    protocol: 'file:',
    slashes: true
  }))

  // Open the DevTools.
  win.webContents.openDevTools()

  // Emitted when the window is closed.
  win.on('closed', () => {
    // Dereference the window object, usually you would store windows
    // in an array if your app supports multi windows, this is the time
    // when you should delete the corresponding element.
    win = null
  })
}

// This method will be called when Electron has finished
// initialization and is ready to create browser windows.
// Some APIs can only be used after this event occurs.
app.on('ready', createWindow)

// Quit when all windows are closed.
app.on('window-all-closed', () => {
  // On macOS it is common for applications and their menu bar
  // to stay active until the user quits explicitly with Cmd + Q
  if (process.platform !== 'darwin') {
    app.quit()
  }
})

app.on('activate', () => {
  // On macOS it's common to re-create a window in the app when the
  // dock icon is clicked and there are no other windows open.
  if (win === null) {
    createWindow()
  }
})

// In this file you can include the rest of your app's specific main process
// code. You can also put them in separate files and require them here.
```

 - index.html - Contem apenas a view da aplicação com os componentes de renderização


```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>Hello World!</title>
  </head>
  <body>
    <h1>Hello World!</h1>
    We are using node <script>document.write(process.versions.node)</script>,
    Chrome <script>document.write(process.versions.chrome)</script>,
    and Electron <script>document.write(process.versions.electron)</script>.
  </body>
</html>
```

Para iniciar a aplicação utiliza-se

```bash
electron main.js
```

Para fazer o build para as plataformas desejadas a comunidade do electron recomenda a utilziação do [electron-builder](https://github.com/electron-userland/electron-builder) que assim como outras ferramentas podem ser encontradas em [Electron Community](http://electron.atom.io/community/)

### Referências

 - [electron-docs](http://electron.atom.io/docs/)
