# Database maintenance

It is not advisable to rename PK columns in a table. The application uses the PK fields to generate unique keys as well as to set the parameters of input/output for windows and panels.

If you decide to change the primary keys fields, you have to align the data model, through the ad hoc button available in the detail model form and then manually align the input/output parameters folder of panes using that object.

