# Goals
Complete themes have long been considered as the main reference for customization, but they faced many problems such as:
- they broke with every new release
- they had to rebundle all browser theme files (even parts the theme didn't care about)
- every part that remained unthemed by the complete theme was unusable for the user

The goal of this API is to provide extension authors a powerful and sustainable API to customize the User Interface. The API should allow:
- Changing the color/background of UI elements (toolbars, tabs, possibly more)
- Changing built in UI images
- Changing the toolbar button styling
- Changing the tab style (squared vs australis)

# Challenges
- The API should stay sustainable (should not break at every Firefox release) while staying powerful

# Possible APIs

## Dynamic theming: Theming elements globally
### Use cases
- Someone wants to apply some styling across all windows on the same element (VivaldiFox coloring of UI elements)
- An add-on that would provide 2 themes, and ability to switch between them (VivaldiFox dark vs light themes)

### Syntax
```
browser.ui.{manifest-entry}
```

Where {manifest-entry} is one of these:
- Manifest entries supported by chrome (https://developer.chrome.com/extensions/themes)
- Other possible properties that Firefox might support based on the add-on authors needs.

## Dynamic theming: Theming individual elements
### Use cases
- Color each tab based on a specific situation (eg. Colorful Tabs: https://addons.mozilla.org/en-US/firefox/addon/colorfultabs/)
### Syntax
```
browser.ui.getViewFor(el);
// el: object returned by a webextension API
// returns InterfaceElement
```
```
InterfaceElement.prototype = {
  get/set background,
  get/set color
}
```
### Example usage
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
