  
<img style="width: 80px" src="https://image.noelshack.com/fichiers/2023/31/6/1691251956-image-2023-08-05-181236838.png">

<h1> ElectronJS repository to start ! </h1>
before continuing please install <a href="https://nodejs.org/fr">NodeJS</a><br><br>

<pre style="margin: 0 0 16px">node -v</pre>

<h1> How to use ?</h1>

<h4>(1) Create Folder 📁 </h4><br>

<h4>(2) initialize your project </h4><pre>npm init -y</pre><br>

<h4>(3) install electron </h4><pre>npm install --save-dev electron</pre><br>

<h4>(4) in your package.json do the following </h4><pre><code>{
  "scripts": {
    "start": "electron ."
  }
}</code></pre><br>

<h4>(5) create main.js </h4>
<pre>
const { app, BrowserWindow } = require('electron')
const path = require('path')
</pre>


<pre><code>function createWindow () {
  const win = new BrowserWindow({
    width: 800,
    height: 600,
    webPreferences: {
      preload: path.join(__dirname, 'preload.js')
    }
  })

  win.loadFile('index.html')
}
  
app.whenReady().then(() => {
  createWindow()

  app.on('activate', () => {
    if (BrowserWindow.getAllWindows().length === 0) {
      createWindow()
    }
  })
})
app.on('window-all-closed', () => {
  if (process.platform !== 'darwin') {
    app.quit()
  }
})</code></pre>


<h4>(6) create preload.js </h4><br>

<pre>
<code>window.addEventListener('DOMContentLoaded', () => {
  const replaceText = (selector, text) => {
    const element = document.getElementById(selector)
    if (element) element.innerText = text
  }

  for (const type of ['chrome', 'node', 'electron']) {
    replaceText(`${type}-version`, process.versions[type])
  }
})</code>
</pre>

<h4>(6) create index.html </h4>
if you want to use php, in the main.js you will have to change the <code>win.loadFile('index.html')</code> by <code>win.loadURL('http://localhost') </code>for example
