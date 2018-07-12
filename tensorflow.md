# **Machine Learning**

Machine learning is a method of data analysis that automates analytical model building. It is a branch of artificial intelligence based on the idea that systems can learn from data, identify patterns and make decisions with minimal human intervention.

Building precise models allows an organization to get a better chance of identifying profitable opportunities – or avoiding unknown risks.

Platform allows to create a model through a training of that model, starting from data.

The correct definition of the model is checked out through the testing step.

Finally, once the model has been trained opportunely, it can be used with real data to make predictions.

**                        
**

## **Fundamentals**

Before using this module, it is essential to go into depth with some concepts about machine learning and get familiar with them.

In the following sections, an explanation about the most important concepts is provided.

**                        
**

### **Training**

A model is something that must be created from scratch: the training step allows to provide data to the mode. Data consists of problems and related solutions.

Consequently, the training stage must include not only data in terms of problems, but also the solutions for these problems. This allows the model to predict the solution to other problems.

That model will be as accurate as the data provided can represent a variety of different scenarios.

What does a problem mean? A problem is something which requires a solution and can be represented by a set of features, expressed as primitive data, such as text, number, date.

These features play an essential role in the model definition and its effectiveness. Having a limited number of features could not represent the problem completely, having a wide range of features could include data not really connected with the problem and could lead to a significant amount of training problems to submit, before making the model enough efficient.

Asolutionis represented as a numeric value. A model can support a predefined range of solutions, expressed as numeric values. It means that all possible solutions must be expressed in advance and they are represented as an enumeration of values. Consequently, a model cannot be used to figure out a value coming from an infinitive number of possible choices. A model works as aclassifier: it can sort out the right value, starting from the problem data and use them to classify input data and give the most feasible solution.

The definition of a model starts with the declaration of all features and the definition of all solutions, each expressed as a integer value, starting from 0.

For example, we can define a model used to decide whether a geometric shape composed of 4 sides and having angles of 90 degrees is a square or a rectangle.

We all know that this geometric problem can be easily solved by measuring the base and height of that shape and then compare them: if they measure the same length, it means it is a square, otherwise it is a rectangle.

A model cannot work with formulas, like the one just expressed. It work with combinations of data and relative solutions and then use “deep learning” to figure out which is the right solution to new problems belonging to the same area.

In order to train a model for this type of problem, we need to define the possible solutions as well:

| 0 for a square1 for a rectangle |
| :--- |


At this point, we can train the model with a few examples:

| base=1, height=1, solution = 0 \(a square…\)base=2, height=1, solution = 1 \(a rectangle...\)base=1, height=2, solution = 1 \(a rectangle...\) |
| :--- |


This is a very poor training, composed of 3 examples only.

Starting from this point, the model could predict the solution for different combinations of the features, i.e. for base and heights. The reckoned solution could be wrong sometimes, since the model cannot always predict the right classification, it the examples are too few.

For example:

base=2, height=2 could lead the model to predict a solution = 0, since it can see that similar values for the two features leads to 0 or it could predict a solution = 1, since it can see that a base = 2 in the train example leads to a solution = 1, same for an height = 2.

Consequently, it is fundamental to provide “good” training data, in order to let the model to make the right decisions. Creating the right training data is more a form of art rather than a scientific approach, since it is important to give enough data for different combinations of the features, so that the model can notice how same values for a specific feature has lead to different solutions.

**                        
**

#### **Testing**

A way to evaluate the accuracy of a training is testing the model.

Basically, a testing process requires the same type of data: problems and related solutions.

Only problems are taken into account by the model, which is now used to predict solutions. Such solutions are then compared with the right solutions, included in the testing session.

That allows to measure the accuracy of the model.

If the accuracy of the model is not good, multiple training sessions should be carried out, in order to increase the accuracy.

Each time a training session is performed, the accuracy of the updated model can be measured through the testing step.

**                        
**

#### **Prediction**

Once the testing proved the quality of the model though a good level of accuracy \(e.g. 80-90% or more\), the model is ready to use.

It is possible to use the model and make predictions with the data provided in input, expressed through the features defined initially.

**                        
**

**                        
**

## **Neural Networks**

This section is not really needed in order to use Platform to make predictions through the Machine Learning module. More detailed information is given here, about how to model is implemented.

A neural network is a system able to make predictions, once trained.

Such a network can be represented like a graph, composed of nodes and edges:

![](https://lh6.googleusercontent.com/1sSCexzcLn8tzakNRFmZl-cQkECPvrMLmk1g5j067gX-TOfn0DQwn6dBb1285SU9xEy088tPcptC-O58QNWfUvHku81_K93CwUDfrrmFUQsOnTT1DdSpcxgpE52tvSy8U6PRSnNY)

A neural network can be sized along 2 dimensions:

* layers number- i.e. the number of vertical layers, each composed of a set of nodes; these layers represents the possible solutions, so there must be as many layers as the number of solutions \(or more\)

* nodes per layer- it is possible to have the same number of nodes in all layers or define a different number of nodes in each layer, as in the diagram above.

In general, the higher the number of layers/nodes is, the more accurate the model will be, even with very complex problems, that is to say, with problems described by a large number of features.

However, a model having a high number of layers/nodes requires a large amount of problems/solutions to provide during the training stage. That means it can be risky to have a large number of layers/nodes, because the network might have been trained inadequately.

It goes without saying that the number of layers/nodes must not be increased indiscriminately, since it may lead to the opposite outcome: a low accuracy, due to an insufficient number of training examples.

**                        
**

**                        
**

## **TensorFlow**

Platform Machine Learning module is based on Google TensorFlow ML engine: you can use the user interface provided by Platform to define a model, train and test it and finally, to use it on predicting solutions with your own application data.

All the complexity of TensorFlow is hidden by Platform: you can graphically configure your model and carry out training & testing sessions using CSV filesorSQL queries defined within Platform.

Finally, you can connect the defined model to the rest of your application and exploit the predictions it provides and save them along with your application data.

Optionally, you can access toTensor Board user interface, directly from Platform, in case you need to get detail information about the training sessions and the neural network under definition.

**                        
**

## **Machine Learning in Platform**

Platform App Designer includes a functionality you can use to define any number of models.

Before using it, you have to set a fewapplication settings:

* TensorFlow password, required to authenticate into a TensorFlow server installation, starting from Platform

* TensorFlow url, a public URL to a TensorFlow server installation

* TensorBoardurl, a public URL to a Platform TensorBoard server installation \(optional\)

![](https://lh3.googleusercontent.com/AzCLSTW-sIqz6IllA9PIpEB49lWa2vCQd2BnH34IEPFtk6Zo6coC3YPGUNbgMYorB53c9aYkzq8X5rShIjVnuIMI3Aa1-AujiiFSud7UrxIXNH7BDfiAK27ehnSMARsS08J2gcc5)

Once defined these settings, you can start using Services -&gt; Machine Learning Models

This list reports all models defined. These models are grouped per topic: it is possible to create a new version of a model and use it independently from the original one. All versioned copies are reported as children nodes of a model in this list.

![](https://lh5.googleusercontent.com/0s18rJPSSPwFbFdmebZjwHJaa0Ot12hNqreVW2idWobBMvZIuXUEAnC2kVUmxK1twhW1EuJyrEzZUADSzh8Hpml1Cn8T_48lAtjikuw2qs38A5BhwtsSb3zKuYtjjVIOiwmWvXTU)

Every model is uniquely identified by a “topic”. Other information reported in this list are:

* **Last training date time**

* **Last training outcome**

* **Total number of training examples**

* **Last testing date time**

* **Last testing outcome**

* **Last testing accuracy, expressed in %**

* **Last prediction date time**

* **Last prediction outcome**

* **Last prediction duration**

Through theNew Modelbutton it is possible to create a new model.

When pressing the New Model button, a wizard is prompted, in order to fill out all needed information.

In thefirst panel, some properties are required:

* **Topic**, identifying the current model; the model name is defined per tenant \(company id\), site and environment.

* **Description**

* **Total number of possible solutions** \(e.g. 2 for the geometric problem described above\)

* **Bucket name**, in Google Cloud Storage, where all CSV files will be saved, defined as a directory in Platform

* **Number of training steps**\(default value: 1000\), used to repeat multiple times the examples provided in input

* **Number of nodes per layer **\(default value: 10\)

* **Optional server-side javascript action to execute after a prediction**, for example to read the solutions just reckoned and use them somewhere, together with other application data.

![](https://lh6.googleusercontent.com/RP6hjI7szAyxAYEcEJBlAhVMUto9bzAfDwD9y5fmutkDYY8jIruiUT-SwgIZ48zzOats7mkP8m6AW-qLtpku8Yj_ULaDplfjqB9zvhXwZX7jM7jtFffcFsyqQcixFzGHfr7-fj4X)

Once filled out all required information, the wizard prompts a second panel, where a description must be provided for each solution, representing something understandable for the end user.

In the previous panel the total number of solutions has been prompted: here it is need to fill out as many descriptions as the number of specified solutions.

![](https://lh6.googleusercontent.com/GpKrK7uWsi9jfthBqKqbrFvo3sfxNg253iR6H1aXXqXerORge0IpVEIey0MoLtWz6Bnh5X0s7o7gSSMwcEME4CsnVc6BLikkf0uOr1sQHULuaaXkr-yIsnt07ANpbeAaAiIMnQr6)

Finally, the third panel in the wizard, “Data Extraction” allows to define a SQL query to use to fetch data for the training/testing, in terms of problems \(not solutions too\).

A “Test Query “ button can be used to test the correct syntax of the typed query.

![](https://lh5.googleusercontent.com/21zGoWom1lUiN5JUpBkuZUKfvsFnQE9HhD52MkasW3cCwU1t2q_AlinjQ0-MH1-yFbXU-hhukBfB3YwrL63a3-RS7_YQbWqQVZGN_o9MUAlfjuVwognH_8JVTRgoyd6KDPSCidUn)

This query is not necessary in case data for training/testing is provided through external CSV files.

Anyway, if the SQL query has been specified, then two additional fields are required:

* **main table** - this is the table containing the main data

* **identifying field** - this is a field in the main table, which identifies data for each row

Optionally, it is possible to specify also aprediction field, an additional field in the main table, where storing the prediction provided by this functionality. That is to say, when a prediction is completed and predictions are got back by TensorFlow, these will be loaded in the main table too, by setting them on the prediction field.

![](https://lh4.googleusercontent.com/kBAn5yIFNtiyc7kNfcIcnHRc3GloA24QItw-Jt32Ay2oXFdHT1bsUb6Ya8ago7ifxAzKmGfWMcMjZFFWPfS41E7ym3HDVwgukBVNbq56up8HBnB12o6XCMKl52Il9h1WlRZIvqoz)

Once completed the definition of a model through the wizard described in the previous section, it is possible to start training the model, starting from the detail window.

In the detail model window, there are 3 buttons which allow to execute the training, testing and prediction.

![](https://lh6.googleusercontent.com/KMCIwq9zo3i5LKicWdvN_Qq5GbHTBq8qtmpW2CV6R1Z8LN5Z5AkhCAm3U6LXlXQiCI1Z5-pQiyCWmllP-x1MFq2fPcJy0AmORYviadq7CHxj8vdGGBWIsPhylrrzc7Btx5zlhsq5)

**                        
**

#### **Training in action**

When pressing the training button, a Training window is displayed. Thanks to this window, it is possible to train the model any number of times, starting either from a CSV file written externally and uploaded to Platform or starting from the SQL query defined previously.

![](https://lh5.googleusercontent.com/oKeOkJV48La-a1gwFNTU0kc5QL6ATCrC1AQQT6jmULUUCb5ge1z8l9Zxa8T7FFL_7XvA6-Cs_f4nuSpNhizlNuhurV50DJPGMHCLK3H9b4tFGP0B2q_0mRqoZuB2pPt35SxRQGKg)

This wizard guides the user step by step, starting from the choice of which source to use to train the model: a CSV file or a SQL query.

In case of a CSV file, this must contain data about problems and solutions.

The CSV to provide could contain either

* **data about problems + solutions**

or

* **data about problems + solutions + an additional header row at the beginning + a counter column on the left**

In the first case, you can easily create an hand-written CSV.

In the latter case, you have to provide the real file that TensorFlow requires.

![](https://lh3.googleusercontent.com/5W3q8KFtkpqYoo00Ye9D5-cwCSuXChW9e8cvg3vwivc6yiVvTYs3kdk6QlvOvb9UEOHdzkCkXKjF59KYgRd_vWIQ6nhfpptpy0GolMPz7OI6N8crgZNAsZjKRFRuS4K7fL1lnmz5)

That file must respect the following requirements:

* the fields separator must be a comma; you can use Excel to generate it and save it as CSV with comma separator

* there must be as many columns as the number of features + a column on the right about the solution

* a solution must be an integer number in the range 0...numberofsolutions-1

For example, in case of recognizing the right geometric shape between a square and a rectangle, there are two only solutions and a CSV file could be something like:

| 1,1,02,1,11,2,1 |
| :--- |


The first column is related to the length, the second to the height, the latter is the solution \(0 = square, 1 = rectangle\).

When such a CSV file is uploaded in Platform, it will be enhanced with additional information, needed by TensowFlow:

* a initial “header” row containing: number of data rows, number of features, enumeration of solutions

* an initial column on the left, including the row index

Consequently, the real CSV file passed forward to TensorFlow would be something like:

| 3,2,0,10,1,1,01,2,1,12,1,2,1 |
| :--- |


You can choose to upload the simple CSV file described initially or the complete CSV, including the first “header” row and the row index column.

Once provided this CSV file, click on the Next button on to bottom-right, in order to pass forward that data to TensorFlow and train the model.

All training sessions are reported in the folder named “History”, available in the model detail window.

![](https://lh3.googleusercontent.com/GkxoA5vxaVAa9Is-r8WmACGDzvoHX_NlG3A8EK36beJmwc_fWSCHCI4YvNgeguTGzantiK-AWZA-QDxtywzQwNtqPYRsU6-XbfvoX45EumdiXEd4KiKuoGCo3NOicDWEnLuuJC5m)

An alternative to uploading an hand-written CSV file is reading application data through the execution of a SQL query.

![](https://lh3.googleusercontent.com/pOzTijbS86BQzad3KQHF_xK_xaoPwtWxEDXAYUFUvzis7R-awD7H-2cYEBBteO2x5IyBLdsjiUW689_mPsE1wCo_oEA6pRATLdoKBqJV4U3DFJpWHpLIQ7lmI-ER2TNgCAdI3Bh2)

In this case,the SQL query must be related to the data problem only, not the solutions.

It is possible to specify from which row starting the data reading and how many rows to read.

These two settings are helpful when you are using the same SQL query multiple times \(for multiple training sessions\), but you want to provide every time a different set of rows, otherwise the training would be the same and consequently useless.

In case of SQL Query, the next step is showing all trained data about problems and providing the right solution for each problem in a grid.

The first column in the grid is editable and represents the solution for each row \(for each problem\).

You have to fill out such column and provide the right solution.

You are free to fill out any number of rows: only the ones filled will be passed forward to TensorFlow, in order to train the model.

![](https://lh3.googleusercontent.com/7tbxjsmJfdXzbPEfAWbtvs3mVSWkFqr-1B9NN73gfk10rpwnb9NGaCO4_LnuYn4Thp1jGuyg4VjfF_Jp_Y_IiHxWbIRaBr6ub8r6QBysIGyIMCMMppgnTj0I1E7tVR5rEDIa35qn)

Again, you can see the history of all training sessions through the second folder.

**                        
**

#### **Testing in action**

When pressing the testing button on the model window, a Testing window is shown. Thanks to this window, it is possible to test the accuracy of the model any number of times, starting either from a CSV file written externally and uploaded to Platform or from a SQL query defined previously.

This window is identical to the one described for the training stage, except for the History folder in the model definition window, where the accuracy of the testing session is filled too.

This step is particularly important because it allows to figure out whether the model is enough accurate or if it requires additional training.

A typical scenario is composed of multiple sessions of training + testing, until the accuracy measured in the testing stage is acceptable.

Unfortunately, it could happen that the model has been trained with “wrong” data, i.e. data which do not lead to an efficient model and it could become hard to “fix” the model with additional data, since it has been ruined by the previous sessions.

Such a scenario can be prevented through the Copy button: thanks to this feature it is possible to duplicate the current content of a model and create a sub-version of it, completely independent from the original one. This feature comes in handy to train the model with data which could turn out to be useless, without affecting the original model.

**                        
**

#### **Prediction in action**

When pressing the prediction button on the model window, a Prediction window is displayed. Thanks to this window, it is possible to execute any number of predictions, starting from the model trained previously.

A prediction can be carried out starting either from a CSV file written externally and uploaded to Platform or from a the SQL query defined previously.

In case of CSV file, thismust contain only problem data, NOT solutions,since solutions will be predicted by TensorFlow.

In case of a SQL query, the default query provided when defining the model is prompted. You can pass it forward or change its WHERE conditions, for example by reducing the amount of records to pass forward or limit the record set.

![](https://lh6.googleusercontent.com/zmHU1-_m9Zp75Qj-NvsCkMpRezZcdetAlR2kdGi-9VTFk-KtzuIyIYTV5N0Lt_GAYPeGo_oweodPA_QK_Cmf9cuA0vBvoWe5JvASv4cjeBo-VdDjaaSGT80ihnFO_PWxha9mtbEQ)

Here the first column is about the solution, which will be sorted out automatically from the prediction activity.

After executing a prediction, solutions sorted out by TensorFlow have been gathered and stored by Platform, together with the unique identifier of each record passed in input.

In this way, it is possible to get this combination** &lt;problem id, solution&gt;** and move them to application tables.

These solutions can be moved to the application database through the optional “**Prediction field**” in the “**Extraction data**” folder of the model definition: when it is specified, the values for predictions will be stored in that field automatically.

In case of custom needs, including complex business logic to fire after a prediction, you can always specify the “**Action after prediction**” field, in the “**Model**” folder of the model definition: when it is specified, such action will be automatically invoked after setting prediction data in the table.

The server-side javascript action receive in input this attributes in the “vo” predefined object:

* **startTime** \(e.g. “2018/03/23 14:57:30”\)

* **topic**

* **duration** \(expressed in seconds\)

* **cmd** \(“prediction”\)

* **appId**

* **siteId**

* **processId**

* **fileName** \(the CSV file stored in Google Cloud Storage, containing the solutions for each row in input\)

* **env** \(Platform execution environment\)

* **companyId**

* **bucketName** \(Bucket name in the Google Cloud Storage, containing the CSV file received\)

* **success** \(true or false\)

Thanks to it, you can download the CSV file, if needed, or simply used this event to manage data already loaded in your application tables or, in any case, in the table named CON101\_TENSOR\_FLOW\_RESULTS.

**                        
**

**                        
**

#### **TensorBoard**

TensorBoard is a built-in web console available to check out how the machine learning model is working. It provides a series of diagnosis features to use in order to get more information about the accuracy of the model:

Scalars- provide a set of charts related to the accuracy of the neural network, like “Loss”, reporting the accuracy \(0..1\) along the number of steps \(e.g. 1..1000\)

![](https://lh4.googleusercontent.com/Sk8YLaCfELRoVOC5tPAkRubXWN6tRYi1JMiWjMXHZZr6vEQyvU9j19l3VwKP1FRO4aYnD4v8HAIji-kDchpvU8oc7-knWimu9ppyWQ08cj4gRNC89-nD79D5Gvt2ihRkX88ScbxY)

Graphs- a graphical representation of the neural network, as it has been defined internally by TensorFlow.

Distributions- reporting the chart for each solution defined: each solution is represented on a single chart, which is related to a specific layer of the neural network \(hidden\_layer\_xxx\) and the accuracy for each layer.

![](https://lh3.googleusercontent.com/PXVcRRJF2EUKQh9vDc7-oAlXRHbXOZdCjskdcts0IMWoXEtQ1fAaA-yxaKeQZbgG1ili5nGatTCD-yyvQ_GzyG-RcVBr3SBCJSdf6N2o-hd__JEMz5_9-0S0-6Xmr4UayhQYKg4m)

## **                 **

### 

---



