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

## Proposal 1: CSS Variables based system
### Syntax
browser.ui.setThemeVariable(variable, value);

Possible variables that could exist:
- Toolbar styles: navigation-bar-background, navigation-bar-color, tab-bar-background, ...
- Toolbar button styles: toolbarbutton-background, toolbarbutton-border-color, ...
- Australis vs Squared tabs: tab-selected-start-clip-path, tab-selected-end-clip-path, ...

The limited subset of variables would target areas that are not subject to frequent changes/removals in Firefox.
The API would simply override the specified Firefox built-in CSS variable (see [this](https://dxr.mozilla.org/mozilla-central/source/browser/themes/windows/browser.css#18) for a current list of variables).

### Benefits
- Simple API

### Issues
- Variable names are a bit arbitrary

## Proposal 2: 
### Syntax
browser.ui.getViewFor(el);
// el: object returned by a webextension API
// returns InterfaceElement

InterfaceElement.prototype = {
  get/set background,
  get/set color
}

### Benefits
- Powerful API that provides the ability to color each UI element individually (on a case per case basis), something chrome extensions or complete themes can't do.

### Issues
- A bit more complicated API
- Needs an easy way to style multiple things at once

### Example usage
This example colors tabs based on their URL:
browser.tabs.query({currentWindow: true}).then((tabs) => {
  for (let tab of tabs) {
    let uiEl = 
});
