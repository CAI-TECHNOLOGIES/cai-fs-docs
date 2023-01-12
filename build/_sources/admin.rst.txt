.. _section-11:


Additional Admin Features
-------------------------

**Spark Configuration Guide**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

| [arguments]
| master = <Master of your Kubernetes Cluster>
| jars = <Upload jars for Spark in Spark Dependency and select here>
| py-files = <Upload pyfiles and egg files for PySpark in Spark
  Dependency and select here>
| deploy-mode = cluster // Don't modify this for Kubernetes Based Spark
  cluster.
| [configurations]
| spark.scheduler.mode = FAIR
| spark.kubernetes.container.image = <spark_image_to_be_used>
| spark.kubernetes.namespace = <namespace_for_running_job:
  default=default>

**Add Input Data Source in S3 :**

-  Upload data source in S3A data lake:

-  Create a bucket in S3A (ex: DSCW-spark-k8s-test).

-  Create a folder ‘inputs’ in that bucket or at some path inside your
      bucket.

-  Upload data source file in above folder, with the key of format
      *BUCKET/.../…/inputs/<data_source_name>*
      *\ (ex : DSCW-spark-k8s-test/…/…/…/inputs/car_crashes.csv)*

-  File with the S3A URI
      *s3a://<bucket_name>/…/…/…/inputs/<data_source_name>* should be
      created (ex:
      s3://DSCW-spark-k8s-test/…/…/…/inputs/car_crashes.csv)

..

   **Code Artifacts :**

-  Upload Application jar (ex: DSCW-eda.jar) from local to *Developer ->*
      *Code Artifact* page in Workbench.

-  List the jar name in argument ‘code_artifact’ when calling the
      Kubernetes Spark Operator (implicitly set in template for EDA).

..

   **Example Test - Code Artifacts**

-  Application jar (application_jar/spark_k8_dep_test.jar): Upload
      spark_k8_dep_test.jar in *Developer -> Code Artifact* page in
      Workbench.

-  Dependency jar (dependency_jar/spark-nlp_2.12-3.3.4.jar): Upload
      spark-nlp_2.12-3.3.4.jar in *Cluster Configurations -> Spark
      Dependency* page.

-  Select the above dependency jar in jars of *Cluster Configurations ->*
      *Spark configuration* page

-  Example Pipeline (example_dag/spark_k8_test_dag.py):Create pipeline
      in *Pipeline -> Manage and Create Pipelines* with the example
      pipeline code shared below :

..

   code_artifact = 'spark_k8_dep_test.jar'

   spark_conf = "spark/spark-conf"

   data_uri =
   's3a://aws-dsofminerva-stg-s1e1sg1c1-swb-ds-001/Datastores/ds-DSCW-01/Experiments-Default/inputs/car_crashes.csv'

-  Update the input file path in the pipeline file (‘input_data_uri’
      variable - line:21) - also create bucket and input data file as
      mentioned above.

-  Update the output folder path in the example pipeline file
      (output_data_uri variable - line:23) - without trailing slash

-  Trigger the pipeline and output partitioned file should be created in
      the S3 datalake created by user (path:
      s3a://<bucket_name/<output_folder_path>/car_crashes/…
      preliminary_summary/part..csv)

**PySpark Configuration Guide**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Add Input Data Source in S3 :**

-  Upload data source in S3A data lake:

-  Create a bucket in S3A (ex: DSCW-pyspark-k8s-test).

-  Create a folder ‘inputs’ in that bucket or at some path inside your
      bucket.

-  Upload data source file in above folder, with the key of format
      *BUCKET/.../…/inputs/<data_source_name>*
      *\ (ex : DSCW-pyspark-k8s-test/…/…/…/inputs/car_crashes.csv)*

-  File with the S3A URI
      *s3a://<bucket_name>/…/…/…/inputs/<data_source_name>* should be
      created (ex:
      s3://DSCW-pyspark-k8s-test/…/…/…/inputs/car_crashes.csv)

**Code Artifacts**

-  Upload the following two application files (for example: main.py
      (code_artifact), pyspark_example_test-0.0.1-py3.9.egg
      (pyspark_dependencies)) from local to *Developer -> Code Artifact*
      page in Workbench.

-  List the ‘code_artifact’ name in argument ‘code_artifact’ and the
      ‘pyspark_dependencies’ name in argument ‘pyspark_dependencies’
      when calling the Kubernetes Pyspark Operator.

**Example Test - Code Artifacts**

-  Update all spark configurations in ‘Cluster Configurations’ for
      default group from above section **(Can be set only by Admins)**

-  Upload the following Application files in *Developer -> Code*
     *Artifacts* page in Workbench (mentioned above).

-  main.py (code artifact)

-  Pyspark_example_test-0.0.1-py3.9.egg (pyspark dependencies)

-  These two files are listed in the example pipeline (code artifact
      variable, pyspark_dependencies variable)

-  Create pipeline in *Pipeline -> Manage and Create Pipelines* with the
      example pipeline code shared below :

..

   code_artifact = 'main.py'

   spark_conf = "spark/spark-conf"

   pyspark_dependencies = ["pyspark_example_test-0.0.1-py3.9.egg"]

   input_data_uri =
   's3a://aws-dsofminerva-stg-s1e1sg1c1-swb-ds-001/Datastores/ds-DSCW-01/Experiments-Default/inputs/Tips.csv'

   output_data_uri =
   's3a://aws-dsofminerva-stg-s1e1sg1c1-swb-ds-001/Datastores/ds-DSCW-01/Experiments-Default/outputs'

-  Update the input file path in the example pipeline file
      (input_data_uri variable - line 18), also create bucket and input
      data file as prerequisites.

-  Update the output folder path in the example pipeline file (
      output_data_uri variable - line 20), without trailing slash.

-  Trigger the pipeline and output partitioned file should be created in
      the S3 datalake, created by user (path :
      <bucket_name>/<output_folder_path>/part…csv)

.. _section-13:

.. _section-14:

**Notebook Admin Control Panel**
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  The Control Panel maintains the server states

-  USER can Start/Stop only their servers (kernels)

.. image:: vertopal_09389ccfa10c4c9d9f37eba7fe242877/media/image10.gif
   :width: 2.72396in
   :height: 4in

-  ADMIN can Start/Stop all the servers, which can be created by any
   user.

.. image:: vertopal_09389ccfa10c4c9d9f37eba7fe242877/media/image60.png
   :width: 6.5in
   :height: 1.61111in

**Steps for Viewing Logs**
~~~~~~~~~~~~~~~~~~~~~~~~~~

Steps involved in viewing the logs are as follows :

1. **Choose an app name** : DSCW-logging contains the following app-name
   :

   a. **Istio-proxy** : contains the istio sidecar logs for the entire
         mesh

   b. **Vault-agent** : contains the vault sidecar logs for the entire
         mesh

   c. **Workflow-webserver** : workbench webserver logs

   d. **Workflow-worker** : Workbench Worker logs (Task logs)

   e. **Workflow-scheduler** : Workbench Scheduler Logs

   f. **Workbench-mb** : Workbench RabbitMQ

   g. **Workbench-db** : Workbench MySQL

   h. **Nb-hub** : Notebook-Server Hub

   i. **Nb-proxy** : Notebook-Server Proxy

   j. **Nb-user** : Notebook-Server Single User Pod

   k. **Pvc-logger** : Shows the usage of EFS PVCs, currently in
         development

   l. **Dump** : contains the logs for all other pods inside the mesh

2. **Set the time range** : In the upper right corner, you can see the
   selector for the time-range for which the logs will be shown.

3. **Identify the log fields associated with the application :** Each
   application has a set of valid fields that are populated using log
   processing pipelines inside fluent-bit. Find these fields and display
   them on the logs UI.

4. **Save search :** Once you find the logs you were looking for, you
   can save this search by clicking on the save button in the top right
   corner. As an example, here’s how we would search the logs of
   workflow-scheduler :

1. Choose the app name

2. Set the appropriate time range

3. Add the logfields

4. Save the search for future use

5. For logs of any other applications, follow the below steps :

1. Set app to “dump”

2. Set **kubernetes.namespace_name**

3. Set **kubernetes.pod_name**

4. Set **kubernetes.container_name**

Alternatively, you can also search for your container by using any other
kubernetes metadata such as labels or annotations :

-  Search for **kubernetes.labels** in the search field to see the
   available labels that you can query.

-  Search for **kubernetes.annotations** in the search field to see the
   available labels that you can query.

**Application Specific Log Fields** 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. **Pipeline Logs :**

..

   **Filters** : App = workflow-scheduler

   **Log Fields** : filename , line_no, loglevel, dag_id, task_id,
   run_id, state, try_number

   (Add a filter for the pipeline’s run_id and find the logs for your
   pipeline execution.)

   .. image:: vertopal_09389ccfa10c4c9d9f37eba7fe242877/media/image80.png
      :width: 5.31901in
      :height: 2.97396in

   **2. Pipeline-Tasks Logs:**

   **Filters** : App = workflow-worker

   **Log Fields** : filename , line_no, loglevel, data, offset, dag_id,
   task_id, execution_id,

   try_number, log_id

View the logs of any Pipeline :

-  Search for ‘id’ in the search box on the left.

-  This will show the fields \`dag_id\` and \`task_id`.

-  Click on dag_id and select the dag_id for your Pipeline by clicking
      on the small “+” button next to the percentage.

-  Follow the same process for task_id to separate the logs by task_id.

-  Or you can just view the logs for all the tasks together, and add
      task_id to the visible list of fields and view all those logs
      together

..

   .. image:: vertopal_09389ccfa10c4c9d9f37eba7fe242877/media/image32.gif
      :width: 5.76614in
      :height: 2.67188in

**3. Notebook Server Hub Logs :**

   **Filters** : App = couture-notebook-hub

   **Log Fields** : loglevel, hub-arg1, data

   .. image:: vertopal_09389ccfa10c4c9d9f37eba7fe242877/media/image84.png
      :width: 5.47852in
      :height: 3.35938in

   **4. Notebook Single-User Logs :**

   **Filters** : App = couture-notebook-user

   **Log Fields** : loglevel, filename , line_no, resp_code, method,
   uri_path, hub_username, action, authscopes, kernel, filepath, data

   .. image:: vertopal_09389ccfa10c4c9d9f37eba7fe242877/media/image82.png
      :width: 5.63786in
      :height: 3.51563in

   **5. Service Mesh Access Logs :**

   In any of the above queries, change the container-name filter and log
   fields as below to view the corresponding envoy proxy logs for the
   pod.

   **Filters** : App = istio-proxy

   **Log Fields** : method, uriPath, protocol, response_code,
   istio-arg1, istio-arg2, data

   .. image:: vertopal_09389ccfa10c4c9d9f37eba7fe242877/media/image36.png
      :width: 5.86394in
      :height: 3.37365in

**Users Access and Security** 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

DSCW platform comes with **Role-Based Access Control,** allowing one to
configure varying levels of access across all Users within your
Workspace (as of now only Admin can use this).

Admin can browse through the list of users and their details about the
users in the **Security->Users** tab.

.. image:: vertopal_09389ccfa10c4c9d9f37eba7fe242877/media/image3.png
   :width: 6.32669in
   :height: 1.43229in

Platform also allows him/her to view and edit the permissions for each
role that are defined for the platform.​​ This can be done from the
**Security->Roles** tab.

There are six roles created for Workflow by default: Admin, Business
Owner, Data Custodian, Data Engineer, Data Scientist, Workspace
Custodian. Each of these roles come with a given set of permissions and
can be edited by the Admin.

|image8|
~~~~~~~~

.. |image1| image:: vertopal_09389ccfa10c4c9d9f37eba7fe242877/media/image22.png
   :width: 8.10938in
   :height: 6.49803in
.. |image2| image:: vertopal_09389ccfa10c4c9d9f37eba7fe242877/media/image64.png
   :width: 7.74479in
   :height: 7.79941in
.. |image3| image:: vertopal_09389ccfa10c4c9d9f37eba7fe242877/media/image37.png
   :width: 5.94792in
   :height: 0.97917in
.. |image4| image:: vertopal_09389ccfa10c4c9d9f37eba7fe242877/media/image33.png
   :width: 6.45313in
   :height: 0.31369in
.. |image5| image:: vertopal_09389ccfa10c4c9d9f37eba7fe242877/media/image1.png
   :width: 1.58996in
   :height: 2.91493in
.. |image6| image:: vertopal_09389ccfa10c4c9d9f37eba7fe242877/media/image20.png
   :width: 3.4375in
   :height: 2.27257in
.. |image7| image:: vertopal_09389ccfa10c4c9d9f37eba7fe242877/media/image7.png
   :width: 4.86979in
   :height: 2.55393in
.. |image8| image:: vertopal_09389ccfa10c4c9d9f37eba7fe242877/media/image65.png
   :width: 6.27083in
   :height: 2.0182in