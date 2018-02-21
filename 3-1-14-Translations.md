# Translations

After creating one or more applications in the App Designer, it is time to define all the languages supported by the whole set of applications: this can be done through "Languages" menu item.

![](http://4wsplatform.org/wp-content/uploads/2015/12/langs-1024x438.jpg)

It allows the user to define one or more languages, identified by three codes:

* **language identifier:** such as "EN", "DE", "IT", "FR", etc.
* **language identifier to use when retrieving data from the database:**  this code could vary according to the specific database, where there can be different already existing codes, such as 1, 2, 3, etc.
* **language used for the translations of the GUI** 

Each user has a default language associated, so that the GUI is showed after the user authentication according to the language identifier linked to him.  
The App Designer allows to define up to 50 different languages.  
Translations can be divided into two categories:

* **translations about GUI components** , such as window/panel titles, button texts, column headers, labels; these translations have to be showed using the same language associated to the user
* **data coming from the database** , expressed in a specific language, the one related to the logged user.

These types of translations will be described in detail in the next two sections.

---



