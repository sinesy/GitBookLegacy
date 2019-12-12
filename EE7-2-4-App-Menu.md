# AppMenu

No hierarchical menu items can be showed the menu: all menu items must be part of a unique "plain" list, showed in one of the layouts reported above. Anyway, this is not a limit at all: moble apps cannot be as complex as the web applications, since the device display size and resources are limited.

**No menu**

The app don't have a menu, the developer choose a first window and add to this window the navigation logic.

**Slide menu **

A slide menu is similar to the one proposed in Facebook or GMail app.

**Icon menu**

The icon menu has a Google icon menu style.

**Tab bar**

The tab bar menu can be anchored to the top or the bottom, according to the hosting operating system: typically it is showed on the top for Android and on the bottom for iOS.

![](http://4wsplatform.org/wp-content/plugins../../uploads/media/copiadiplatformmobilemanual/image19.png)

**Left tab bar**

The menu is blocked on the left side of the app. The root of the menù is configured like the other menu, in the no-root window you can add leaves directly from the window.

The leaves can be anchor to the top or botto of the window.

![](/assets/IMG_94E9FA5E1E2C-1.jpeg)

**Window transition**

Independently of the menu type, the transition form a window to another can happen through several events:  
through a button \(including the "Back" button used to get back to the parent window\) included in the navigation bar, automatically showed if there is at least one other button defined for the navigation bar.

![](http://4wsplatform.org/wp-content/plugins../../uploads/media/copiadiplatformmobilemanual/image20.png)

via a button included within the window; in that case, the child window will be opened from this window and some parameters can be passed forward; this scenario requires to specify the child window name and parameters through a javascript action  
through the tap \(click\) event on a row of the grid  
long click on an element of the list / button.

---



