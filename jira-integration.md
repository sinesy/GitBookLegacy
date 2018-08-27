# Jira integration

Jira Software is a cloud based service, originally born as a project tracking system.

Over time, Jira increased in popularity and features and now it includes a variety of different features, such as:

* project management and monitoring
* agile team oriented tools, including Scrum dashboards and reports, kanban, backlog, epics, sprints and user stories
* project versioning and planning 
* bug and activities tracking system

Moreover, Jira provides a powerful Rest API through which it is possible to connect Jira to external applications and tools.

Platform provides and embedded integration with Jira Software, based on the Jira Rest Cloud API.

Supported features embedded in Platform are:

* **Jira user import tool**, in order to work with the same team on both sides: Platform and Jira
* **all issues** at Project level
* **assigned issues**
* **issue creation**
* **reporting**
* **project** **dashboard**

![](/assets/j_board.png)



### How to setup Jira integration

In order to make it possible for Platform to communicate with Jira, a few settings are needed:

* open Application detail window in the App Designer and select to the Application parameters folder
* expand the JIRA group and fill out the two required parameters:
  * **JIRA\_URL** - the URL where Jira cloud is installed \(e.g. yourcompanydomain.atlassian.net\)
  * **JIRA\_PROJECT** - the Jira project name, you have previously defined in Jira

Once saved this values, reload the App Designer, in order make it visible a new menu item: Jira.



**Prerequisites**

Before connecting Platform to Jira, be sure to have a correct Jira cloud environment already available. Within this environment, you have to have defined:

* Jira users
* Jira groups \(if any\) and linked users
* a Jira project and its permission schema, where users/groups must have been assigned to such a schema

### Importing Jira users

Once you have correctly setup the Jira integration described in the previous section, you can start importing Jira users into Platform, through the new Jira menu available in the App Designer.

Here you can find the menu item named "Import Jira user".

Through it you can see all available Jira users assigned to the connected Jira project.

In that editable grid, you can assign for each row an already existing Platform user. At the end of this configuration activity, simply press "Import selected users": only rows having the Platform user filled will be taken into account.

In this way, Platform and Jira users will be connected with each other.

As an alternative, you can Import all users: in this case, Platform will also create Platform users for the rows not having a linked Platform user: for each empty cell, a Platform user will be created and linked to the Jira user. New Platform users are always created with site id = 100 and with an expiration password set to today, in order to force the user to change the expiration date.

### Project issues

There are two functionalities available.

**Assigned issues **- related to the only issues assigned to the current logge user.

**All issues**, independent from the assigned user and not necessarelly bounded to a sprint.

![](/assets/j_list.png)

On the top of the window, there is a filter panel you can use to filter the issues list:

* **board** - a board is a Jira organization of issues; typically every Jira project has a default board; optionally, additional boards can be created
* **epic** - in the agile methodology, an epic is a large amount of work, which can be split up in shorter ones, named user stories; it is optional
* **sprint** - in the agile methodology, a sprint is an amount of work, composed of user stories; typically it represents a release of a working app

Through this filters, it is possible to show only user stories \(issues\) related to a specific sprint. In such a case, an additional panel on the right is shown: it reports the epics and sprint lists for the specified board.

---

If a board and sprint has been selected, the "**Report**" button allows to open a web page where showing all available reports from Jira \(e.g. burndown chart, etc\).

![](/assets/j_report.png)

---

Very common filters you can use are also:

* **key** - the issue key you can specify, in order to find a specific issue
* **summary** - the text composing the issue you are searching for

It is possible to show the issue details by double clicking on an issue.

![](/assets/j_dett.png)

In the issue detail, you can see:

* the **issue details**
* the list of **comments**; you can add comments, in case the issue is assigned to you
* the list of **linked issues**
* the list of **attachments**; you can download attached files, if you desire
* the list of **worklogs**; you can add a worklog, in case the issue is assigned to you

Finally, there are a few commands you can execute form the issue detail window:

* **Assign to me** - allows to assign the issue to the current logged user
* **Add comment**
* **Add worklog**
* **Change state **- through it, you can change the current issue state: to do, in progress, done



