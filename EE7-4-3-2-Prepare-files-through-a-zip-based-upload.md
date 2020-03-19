# Prepare files through a zip based upload

Non always it is acceptable to upload manually every single image, especially when there is a huge number of images to upload.  
It is possible to exploit an ad hoc feature provided by Platform to automate the upload of all the images contained in a zip file. This .zip file will be the only file to upload.  
When definining the column/control used to upload a file, additional settings must be provided:  
application id that Platform will be use when inserting record in CON54/55  tables, for each file found within the zip uploaded file  
SQL update instruction that Platform will execute for each file foud in the zip file. The WHERE clause of that update statement must contain two binding variables: the file id and the pk of the record.

### Example

update PRODUCTS set =? where =? and …  
optional data source id used  by Platform to execute the SQL update instruction, for each image found within the zip file; this data source is the one to use when connecting to the database schema containing the table to update  
This feature can be used as long as there is already a table containing a record for each potentially linked image and having a field related to the image id and the image name corresponds exactly to the pk for that table. More precisely, the value of the pk field will be file name without its extension.

For instance, if the table PRODUCTS has the following structure:  
PRODUCT\_CODE  
DESCRIZIONE  
IMAGE\_ID

and within it there is already a record with the values:

CAPPA  
Cappa  
null

\(so no image has been linked to the product yet\), then if the zip to upload contains an imae having name "CAPPA.gif", the result will be that:  
the file will be saved on the file systtem, within the "files" subfolder of the "sync folder path" for the specified mobile app  
the file will be indexed in CON54/55 \(if not already indexed\)   
the following SQL instruction will be carried out:  
UPDATE IMAGES\_TABLE set IMAGE\_ID=? where PRODUCT\_CODE=?  
with values CAPPA.gif and CAPPA respectively.

---



