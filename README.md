# Run two CICD pipelines for the given Project: on Github VM using Actions and on AWS cloud using Jenkins. 
I installed Jenkins on my Laptop (Built-In Node) and I configured Jenkins agent to run all jobs in AWS cloud (for technical details see **Jenkins_configuration.txt**). CICD pipelines were deveveloped in the following order.
* Define the project for CICD. The description of the project, in a nutshell: The class VendingMachine **(_the subclass of the class Drink_)** can be filled by Drinks **(_Jus or Datacola - other child of the class Drink_)** in two kinds of beverageContainer **(_can or bottle_)** with different numbers of days before expiration. The code see in the folder theProject: (i) The class is defined in **vendingmachine.py**; (ii) The first version of the Unit testing is in **test_vendingmachine.py**; (iii) The API is givent by **run.py**.
* Write the first CICD pipeline using Github, trigered by each "git push" to the Current repository to keep track of all Code changes in a real time. The steps are (for details see **.github/workflow/control_tests.yaml**): (i) Get access to **theProject** from the Github VM; (ii) Set up Python environment; (iii) Run the first test for all *.py files of **theProject** in order to check for errors, styles and Code complexity; (iiii) Run the second test, **Unit test** only for **test_vendingmachine.py** in **theProject**. This whole pipeline is trigered by each "git push" to the Current repository.
* Write the second CICD pipeline (for details see **Jenkinsfile**). Three stages are included: (i) Build - to launch the AWS instance (if it does not exist) and set up the working environment. I need Python and Docker (this is because latter I will use one Docker image to compile the API to the single binary file); (ii) Test - to run Unit testing and pass the result to Jenkins to be able to see it in a real time using Jenkins UI;


cluster on AWS cloud and showed some its important functionalities. 
or






triggered by each git push request to the given project
Unit Testing is done using pytest. Code is checked by flake8.  
maxAllowedNumberOfDrinksInside

# OBJECTIVE: To get familiar with Spark.
I installed Spark cluster on AWS cloud and showed some its important functionalities. 
* The file **spark_installation.txt** describes the installation procedure. This is done on top of a Hadoop YARN cluster, which I installed previously (for details see [Hadoop-Hive](https://github.com/PavelPll/Hadoop-HIVE) project in the current git repository).  
* The folder **./Scala_ETL** contains the example of ETL (Extract Transfer Load) pipeline written in Scala.
* The folder **./Java_ML** contains the example of simple machine learning pipeline in Java.
* The example of data batch processing with Spark (**./Streaming**).
> [!NOTE]
> Each project is accompained by intsruction how to run it on Spark cluster in Scala, Java or in Python environment (see the corresponding **How_to_run.txt** files).
