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

### How to setup Jira integration

In order to make it possible for Platform to communicate with Jira, a few settings are needed:

* open Application detail window in the App Designer and select to the Application parameters folder
* expand the JIRA group and fill out the two required parameters:
  * **JIRA\_URL** - the URL where Jira cloud is installed \(e.g. yourcompanydomain.atlassian.net\)
  * **JIRA\_PROJECT** - the Jira project name, you have previously defined in Jira

Once saved these values, reload the App Designer, in order allow Platform to add a new menu items about Jira.

**Prerequisites**

Before connecting Platform to Jira, be sure to have a correct Jira cloud environment already available. Within this environment, you have to define:

* Jira users
* Jira groups \(if any\) and linked users
* a Jira project and its permission schema, where users/groups must have been assigned to such a schema

An **agile** setup inside Jira is recommended, in order to use all the amazing features provided by Jira and included in Platform as well.





### Importing Jira users

Once you have correctly setup the Jira integration described in the previous section, you can start importing Jira users into Platform, through the new Jira menu available in the App Designer.

Here you can find the menu item named "**Import Jira users**".

Through it, you can see all available Jira users assigned to the already connected Jira project.

In the prompted editable grid, you can assign for each row an already existing Platform user. At the end of this configuration activity, simply press "**Import selected users**": only rows having the Platform user filled will be taken into account.

In this way, Platform and Jira users will be connected with each other.

As an alternative, you can **Import all users**: in this case, Platform will also create Platform users for the rows not having a linked Platform user: for each empty cell, a Platform user will be created and linked to the Jira user. New Platform users are always created with site id = 100 and with an expiration password set to today, in order to force the user to change the expiration date.



### User authentication

Once configure what reported above, a Platform user \(which is also a Jira user\) can use any of the functionalities related to Jira in the App Designer. The first time he does it, an input dialog is showed, prompting for the password:

* in case Platform has been connected to a Cloud Jira installation, the password is the auth token, specific for each user, which can be accessed following the web page reported in foreground
* in case of a Server \(local\) installation of Jira, the password is NOT the one used by the Jira user to access it, but it is the API password. Each user can generate it by accessing the first time Jira, go to User Profile and press Set Password to specify it.



### Project issues

There are two functionalities available.

**Assigned issues **- related to the only issues assigned to the current logge user.

**All issues**, independent from the assigned user and not necessarelly bounded to a sprint.

![](/assets/issues.png)

This window includes a series of very helpful views, organized hierarchically, from top to bottom:

**Boards** - a board is a Jira organization of issues; typically every Jira project has a default board; optionally, additional boards can be created.

**Epics** - in the agile methodology \(Scrum\), an epic is a large amount of work, which can be split up in shorter ones, named user stories; when selecting a boards, the list of epics are filtered by the current board.

Epics are optional and it is possible to simply arrange a single board directly to a set of sprints, which represents a very common scenario.

![](/assets/epics.png)

**Sprints** - in the agile methodology \(Scrum\), a sprint is an amount of work, composed of user stories; typically it represents a release of a working app, at the end of a period of time, called iteration.

The agile methodology involves an iterative and incremental approach, where deliveries are planned at the end of each iteration, where a working app is released.

When selecting a board, the list of sprints are filtered by the currently selected board.

![](/assets/sprints.png)

**Backlogs** - in the agile methodology, a backlog represents a list of features or technical tasks which the team maintains and which, at a given moment, are known to be necessary and sufficient to complete a project or a release. Basically, a backlog reports the list of stories not started \(to do\), in progress and completed \(done\).

This view shows the backlog related to the current selected sprint. If not selected, the "active" sprint is used as default setting.

![](/assets/backlog.png)

**Versions** - This view reports all defined application versions, i.e. planned deliveries.

![](/assets/versions.png)

**Project issues** - This is the list of issues, filtered by the current selected sprint, which is filtered by the current selected board.

The last panel includes a few filter conditions, used to additionally apply filtering values to the issues list:

* **issues state**: to do, in progress, done - the default setting allows to show all issues but not the ones already closed \(done\)
* **issue key** - helpful when searching for a specific issue by its key

---

If a board and sprint has been selected, the "**Report**" button allows to open a web page where showing all available reports from Jira \(e.g. burndown chart, etc\).

![](/assets/j_report.png)

---

It is possible to show the issue details by double clicking on an issue.

![](/assets/issue.png)

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
* **Set a version**

---

Starting from the issues list or from the menu bar, it is also possible to create a new issue from scratch.

![](/assets/newissue.png)

You have always to specify:

* an issue type
* a priority
* a summary
* a description

Optionally, in case you are defining user stories in a sprint, you can also define:

* a sprint to use to link the issue \(the user story\) to that sprint
* the story points for that user story



