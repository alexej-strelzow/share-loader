[![npm](https://img.shields.io/npm/v/share-loader.svg?style=flat-square)](https://www.npmjs.com/package/share-loader)
[![npm](https://img.shields.io/npm/dm/share-loader.svg?style=flat-square)](https://www.npmjs.com/package/share-loader)
[![MIT licensed](https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square)](https://github.com/MrFrankel/share-loader/blob/master/LICENSE)

<div align="center">
  <!-- replace with accurate logo e.g from https://worldvectorlogo.com/ -->
  <a href="https://github.com/webpack/webpack">
    <img width="200" height="200" vspace="" hspace="25"
      src="https://cdn.rawgit.com/webpack/media/e7485eb2/logo/icon.svg">
  </a>
  <h1>Share Loader</h1>
  <p>The share loader allows you to share modules between webpack builds via a global namespace<p>
</div>

<h2 align="center">Install</h2>

```bash
npm i share-loader --save-dev
```
Or
```bash
yarn add share-loader --save-dev
```
<h2 align="center"><a href="https://webpack.js.org/concepts/loaders">Usage</a></h2>

webpack config of exposing app
```js
module: {
  rules: [{
          test: /\.js?$/,
          use: [{
            loader: 'share-loader',
            options: {
              modules: [/@angular/, /@uirouter\/angular/],
              exclude: [/@angular\/material/],
              namespace: 'some-name-space'
            }
          }]
        }]
}
```


webpack config of consumer apps

```js
const {Externals} = require('./share-loader');

externals: [
  Externals({
    namespace: 'some-name-space',
    modules: [/@angular/, /@uirouter\/angular/]
  })
],
output: {
  library: 'some-name-space',
  libraryTarget: 'umd'
}


Example

1. In the example folder, run npm install on each project,
2. Run npm run build:prod in the ext-app-1 root
2. Host the ext1.js file from ext-app-1 project in some localhost server
3. Change the <%path-to-server-host%> in the shell project app.state.ts
4. Run npm run serve:dev in the shell project root



Example-cli
1. In the example folder, run npm install on each project,
2. Run npm run ng run ext-app1:build-ext in the ext-app1 root
2. Host the main.js file from ext-app1 project in some localhost server
3. Change the <%path-to-server-host%> in the shell project app.state.ts
4. Run ng serve in the shell project root
5. You can also run ext-app1 in standalone mode with ng serve
```