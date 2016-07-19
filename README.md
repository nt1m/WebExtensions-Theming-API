# WebExtensions theming API
Proposal for a possible theming API for WebExtensions.

If you'd like to skip the reading and check the API proposal directly, click [here](https://github.com/nt1m/WebExtensions-Theming-API/blob/master/Proposal.md).

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
- More here: https://docs.google.com/document/d/10DXgMZuO3_LQrs5IQOxn3ErBheRZvIKc3ZHWVBvpI5E/edit#

# How do I contribute ?
You can give feedback by filing issues or provide possible solutions to the existing issues.

