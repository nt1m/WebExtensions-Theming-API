# Definitions
## Supported CSS properties
This includes their longhand properties:

- background
- color
- box-shadow
- text-shadow
- filter
- border/outline (border-width should be restricted to reasonable sizes)
- font (though 8px < font-size < 20px to avoid breaking Firefox)
- text-decoration/text-align/text-transform
- -webkit-text-fill-color

## Supported manifest entries
- Chrome entries: See https://developer.chrome.com/extensions/themes#manifest
- Firefox naming scheme:

```
moz.{ui-element}.[state].{css-property}
```

Where {ui-element} is:
- toolbar (default value if the values below are not defined)
- tab-toolbar
- navigation-toolbar
- bookmarks-toolbar
- toolbar-button
- tab

Where [state] is optional and corresponds to:
- hover
- active
- focus

If [state] is not defined, it targets default state.

# API1: Basic themes
Support the manifest entries above in manifest.json. See https://developer.chrome.com/extensions/themes

## Example
See https://developer.chrome.com/extensions/themes#manifest

# API2: Dynamic themes
## Use cases
- Basic theme that changes based on the time of the day.

## Syntax
```
browser.ui.{manifest-entry} // This is a getter and a setter
```

Where {manifest-entry} corresponds to one of the manifest entries above.


## Example
This example specifies a theme based on the time of the day.
```
var hour = (new Date()).getHours();
if (hour > 8 && hour < 17) {
  browser.ui.moz.toolbar.background = "white";
  browser.ui.moz.toolbar.color = "black";
  browser.ui.images.theme_frame = "images/theme_day.jpg";
} else {
  browser.ui.moz.toolbar.background = "black";
  browser.ui.moz.toolbar.color = "white";
  browser.ui.images.theme_frame = "images/theme_night.jpg";
}
```
# API3: Theming temporary/user-generated elements
## Use cases
- Color each tab based on a specific situation (eg. Colorful Tabs: https://addons.mozilla.org/en-US/firefox/addon/colorfultabs/)

## Syntax
```
browser.ui.getViewFor(el);
// el: object returned by a webextension API
// returns InterfaceElement
```
```
InterfaceElement.prototype = {
  get/set background,
  get/set color
  // ...other CSS properties, see list above
}
```

## Example usage
This example colors tabs based on their URL:

```
browser.tabs.query({currentWindow: true}).then((tabs) => {
  for (let tab of tabs) {
    let uiEl = browser.ui.getViewFor(tab);
    switch (tab.url) {
      case "https://google.com":
        uiEl.background = "blue";
        break;
      case "https://yahoo.com":
        uiEl.background = "purple";
        break;
    }
  }
});
```
