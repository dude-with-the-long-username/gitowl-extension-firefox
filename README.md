## GitOwl Browser Extension For Firefox

<h3 align="center">
  <b><a href="https://gitowl.dev">gitowl.dev</a></b>
  <span> • </span>
  <b><a href="https://chrome.google.com/webstore/detail/gitowl/gijnkijpbdlefjnobncjfongkbpoohdb">chrome</a></b>
  <span> • </span>
  <b><a href="https://addons.mozilla.org/en-US/firefox/addon/gitowl-open-source-insights-at/">Firefox</a></b>
</h3>

![Screenshot](screenshot.png)

This repository contains the source code for the UNOFFICIAL GitOwl Firefox browser extension.

[Firefox extension link](https://addons.mozilla.org/en-US/firefox/addon/gitowl-open-source-insights-at/)

The extension aims to interact as little as possible with the websites on which it is run.

The extension functionality is limited to:
- Creating a drawer component to display GitOwl iframe in.
- Identifying the entity (user/repository) being viewed.
- Constructing URL for GitOwl iframe.
- Creating a GitOwl iframe.
- Controlling open/closed state of the drawer.

The extension currently works on:
- GitHub
- NPM
- PyPI

## Details

### Framing

- GitOwl iframe (`I2`) is created inside another iframe (`I1`) to avoid cross-origin issues.
- Content script identifies the entity being viewed and passes it as the `path` query parameter to `I1`.
- Content script updates the `src` attribute of `I1` on URL changes.
- Content script sends messages to `I1` on drawer opening.


### Content Script & Drawer

- Content script creates the following components:
  - Drawer
  - Drawer toggle button
  - IFrame (`I1`)
  - Drawer draggable handle
- Open/Closed state and width of the drawer are stored in local storage.
- Content script listens to changes in URL and updates the `src` attribute of `I1` accordingly.


## Development

To run the extension locally

### Build the extension

```shell
$ npm install
$ npm run build
```
- In the `dist/` folder that was now created, modify the `manifest.json` file to include extension_id.
  - Add the block
  ```json
    "browser_specific_settings": {
  "gecko": {
    "id": "{insert-your-extension-uuid}"
  }
  ```
  - you can generate your uuid using [online uuid generators](https://www.uuidgenerator.net/version4)
  - be sure to enclose your id using "{}"
  - Example id:
  ```json
  "id": "{ee24b1ac-6de9-402d-bbfa-32c647b385d1}"
  ```
- navigate to `dist/` folder & run `zip -r gitowl.xpi manifest.json contentscript.js framescript.js frame.html favicon@16x16.png favicon@48x48.png favicon@128x128.png` to generate a `.xpi` extension file.

### Load the extension

- Open the Extension Management page by navigating to `about:debugging` in Firefox.
- Click `This Firefox` button on the left and then click `Load Temporary Add-on` button
- Select the `.xpi` file we generated in the previous step

---

- All images & rights reserved to original authors of the GitOwl package.
- GitOwl homepage: [link](https://gitowl.dev/)