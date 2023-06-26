# Modern-iOS-Navigation-Patterns
All the familiar navigation patterns for structuring iOS apps, like drill-downs, modals, pyramids, sequences.
# 1. Structural Navigation
### A typical iOS application has a fixed architecture—often a hierarchical tree with multiple levels. This rigid structure makes navigation options predictable. Structural navigation patterns give users confidence about where they came from, where they are in the hierarchy, and how to navigate back to where they came from.
## Drill-Down
![](https://github.com/Akhmedau/Modern-iOS-Navigation-Patterns/blob/master/Drill-Down.png)
--
The drill-down navigation pattern traverses an information tree structure as cascading lists—level by level, screen by screen.
Animated transitions imply horizontal movement between columns: Moving right goes deeper into the tree hierarchy, moving left goes back up the hierarchy.
Drill-down navigation is stateless: Traversing the hierarchy is always possible and is never interrupted by questions about whether to save state.
The Navigation Bar displays the title of the current screen.
Disclosure indicators () on list rows show that it’s possible to drill down deeper into the hierarchy.
A Back button () provides an obvious path back up the hierarchy. If space permits, it should be labeled with the title of the parent screen rather than a generic “Back”.
Swiping right from the left edge of the screen does the same as pressing the Back button.
For right-to-left languages, the drill-down direction and control layout are mirrored to match the reading direction.
The tree structure can be built dynamically to filter a database. For example: In a music player app, you can drill down from different hierarchical starting points (Artist, Album, Genre) to find the same album, as well as using a search interface.
Drill-down navigation is the one-column-per-screen variant of the macOS Finder-style Miller columns.
## Flat
![](https://github.com/Akhmedau/Modern-iOS-Navigation-Patterns/blob/master/Flat.png)
--
The flat navigation pattern divides the hierarchy at the root level and presents it as a tab bar (or as a sidebar on iPad).
The tab bar items are curated around the main capabilities of the app to shape the user’s expectations and their mental model of what the app can do.1
One of the tab bar items is always selected, and the active selection determines what’s displayed in the main content area of the app.
The currently selected tab bar item should not change programmatically (without user interaction) or indirectly (for example, by tapping a button elsewhere in the interface).
The tab bar remains visible on all screens throughout the application, except when it is temporarily covered by a modal sheet (see below).
Tabs can be used as filters or as different entry points for the same large collection of content, such as a library of music, videos, or photos.
Each section retains the navigation state for its own sub-hierarchy.
Tab bar items should behave in a predictable way; they should not bring up sheets or trigger actions.
The infamous  Hamburger menu is the tab bar’s evil sibling: Discoverability suffers when the entire navigation interface is hidden behind a small icon. Hamburger menus were in style on iOS for a few years around 2015, but app makers abandoned them when research showed that tab bars were much more discoverable.
## Pyramid
![](https://github.com/Akhmedau/Modern-iOS-Navigation-Patterns/blob/master/Pyramid.png)
--
The pyramid2 pattern allows you to quickly navigate between sibling views at the same hierarchy level without having to go back to the parent screen.
The horizontal swipe gesture is a common way to move between sibling views in a media application. Buttons can also be used, such as the  Next Message and  Previous Message chevrons in the iOS Mail app.
The iOS Photos app demonstrates the pyramid pattern: Tap a photo to open it in a full-screen view, then swipe left and right to flip through adjacent images.
Use a page control for small collections to visualize the total number of items and the current item’s position relative to its siblings.
## Hub-and-Spoke
![](https://github.com/Akhmedau/Modern-iOS-Navigation-Patterns/blob/master/Hub-and-Spoke.png)
--
The Hub-and-Spoke2 pattern is ideal for large collections of unrelated items at the top level of a hierarchy. To switch between the full-screen child views, you always return to the hub first.
The iOS Home screen—a collection of all the installed applications—serves as a hub and a reliable “neutral state” of the operating system.
The Home indicator at the bottom of the screen is an easy-to-learn and always-available “escape hatch”2 that always leads back to the familiar Home screen interface.
Note that this pattern is rarely used within apps. It is here mostly for completeness. There is hardly ever a need for a separation as strong as the one between applications at the operating system level.
# 2. Overlay Navigation
### Overlays want your attention. They can appear over any context—even on top of other overlays! Modal overlays require a user action before they go away: They switch the app into a different mode, blocking the interface behind them. Non-modal overlays—like transient notifications—do not block the app.
## High-Friction Modal
![](https://github.com/Akhmedau/Modern-iOS-Navigation-Patterns/blob/master/%20High-Friction%20Modal.png)
--
High-friction modal overlays–such as sheets and alert dialogs with multiple actions–block what’s behind them until the user makes a decision.
A decision is required to dismiss them: A decision whether to save state, whether to confirm (by tapping Done) or to destroy (by tapping Cancel) the data you’ve entered on a form.
Modals focus on completing a specific, self-contained task,1 such as composing an email or adding a calendar event.
Stateful sheets and alerts with multiple actions are typical high-friction modals.
## Low-Friction Modal
![](https://github.com/Akhmedau/Modern-iOS-Navigation-Patterns/blob/master/%20Low-Friction%20Modal.png)
--
Low-friction modals—such as sheets, menus, and popovers—block the rest of the app but do not require “either-or” decisions.
They are easy to dismiss: “Low friction” means not having to think about how to get back. Pressing the  close button or swiping down on a sheet, or tapping anywhere outside of a context menu or a popover—low-friction modals are gone with little effort.
![](https://github.com/Akhmedau/Modern-iOS-Navigation-Patterns/blob/master/Ok.png)
Alert dialogs with only an OK button are easy enough to dismiss, but low friction is not the same as no friction: Avoid single-action alerts whenever possible. They interrupt the user’s flow and can often be replaced with inline text or non-modal notifications.
## Non-Modal
![](https://github.com/Akhmedau/Modern-iOS-Navigation-Patterns/blob/master/Non-Modal.png)
--
Non-modal overlays cover a portion of the screen but do not block the interface behind them. Because they are non-blocking (i. e., modeless), they cause little or no friction.
They can appear in response to a trigger outside the app, such as a notification from the operating system.
If they disappear automatically, they should provide at-a-glance peripheral information with minimal interruption.
There may be optional interactivity in a temporary non-modal overlay, such as tapping a notification or swiping on the volume indicator to change the volume before the overlay disappears.
When an overlay doesn’t block the rest of the application and doesn’t appear/disappear automatically, 90s UI veterans call it a palette.
# 3. Embedded Navigation
### Embedded navigation patterns require special care to fit into the strict structural and spatial model of iOS. It is best to contain or embed these patterns in another view, either at a well-defined location in the app structure or in a modal overlay.
## State Change
![](https://github.com/Akhmedau/Modern-iOS-Navigation-Patterns/blob/master/State%20Change.png)
--
A view can have several states. For example, replacing the loading progress indicator of a view with the loaded items doesn’t change the position in the hierarchy.
Make sure that the state change really is neither hierarchical nor modal.
Avoid full-screen transitions for in-place state changes.
Other examples: an edit state for a list; a web brower interface; a panning map; a zoomable image.
Different view options for the same data on the same screen is also a state change that changes the screen content without changing the user’s position in the hierarchy.
## Step-by-Step
![](https://github.com/Akhmedau/Modern-iOS-Navigation-Patterns/blob/master/Step-by-Step.png)
--
The step-by-step pattern connects a series of screens in a linear flow, such as guided tours, setup flows, and onboarding tutorials. Entering a lot of data in an online store checkout also requires multiple steps.
Stepping back and forth in the sequence doesn’t change the hierarchy level. This is different from the drill-down pattern described above.
A step-by-step sequence should be contained in a modal overlay for presentation to emphasize that the Back button in this context serves a different purpose than in a hierarchical drill-down.
The step-by-step process is usually completed with a Done or  Close button, which also closes the containing modal.
The sequence can have a variable number of steps and different paths depending on the options selected.
“Wizard” and “assistant” are alternative names for this pattern.
Step-by-step processes can feel tedious. If you expect users to perform the process frequently, consider combining the steps into a single view with different states to increase the information resolution and reduce context switching.
## Content-Driven
![](https://github.com/Akhmedau/Modern-iOS-Navigation-Patterns/blob/master/Content-Driven.png)
--
Content-driven navigation3 (non-linear navigation, experience-driven navigation) means that a hyperlink or button can teleport the user to any other page or view. It’s how web navigation works in the browser.
Avoid this pattern in iOS apps, except for apps that display hypertext, immersive games, or similar non-linear content.
If you must display hypertext content in an app, consider embedding it in a browser interface with  back and forward controls. A state change of a self-contained browser interface is easier to understand than an unexpected change of location in the application hierarchy.
You can use links to navigate between applications: Deep Links2 take the user from one app or from a website deep into the hierarchy of another app (using a URL scheme or domain-bound Universal Links).

[RU]
Link: https://habr.com/ru/companies/cleverpumpkin/articles/738584/







