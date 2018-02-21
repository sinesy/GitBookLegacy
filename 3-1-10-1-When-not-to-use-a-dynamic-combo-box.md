# When not to use a dynamic combo box

A dynamic combo-box is very similar to a lookup: in both cases a list of codes is retrieved by calling a business component on the server side.  
Anyway, there are two main differences between them:  
 **combo-box**   → show one only column \(description\)  
 **lookup grid →**  can show any number of columns  
 **combo-box**  → mustn’t be used to fetch a great degree of values \(web app will crash on the client side\)  
 **lookup grid**  → no limit in the number of items  
Therefore, it is essential not to use combo-boxes when the number of items exceeds a few hundreds of records.

---



