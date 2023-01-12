.. _section-10:

.. APPENDIX AND REFERENCES
.. =======================

Pipelines Developer Reference
-----------------------------

A pipeline is defined in a Python script, which represents its structure
(tasks and their dependencies) as code. Pipeline tasks are created by
instantiating as operator class. There are different types of operators
available as explained in the list below. These operators are used to
define a single task of the pipeline.

**Operators**
~~~~~~~~~~~~~

**PythonOperator**
^^^^^^^^^^^^^^^^^^

Use the PythonOperator to execute Python Code..

*Basic* *Parameters*
''''''''''''''''''''

-  dag: CaiDAG - Object of the CaiDAG Class

-  task_id: str - Task ID for the task (used in Dag context)

-  code_artifact: List[str] - List of Code Artifacts to be used.

-  method_id: str - Method ID for the specific Task (used in Code
      Artifact codebase context)

-  input_base_dir_path: Optional[str], "" - Base directory path for
      input files. This has to be a string

-  input_filenames_dict: Optional[Dict], {} - Relative file paths for
      input files w.r.t input base directory. To be passed in dictionary
      format.

-  output_base_dir_path: Optional[str], "" - Base directory path for
      output files. This has to be a string

-  output_filenames_dict: Optional[Dict], {} - Relative file paths for
      output files w.r.t output base directory. To be passed in
      dictionary format.

*Advanced* *Parameters*
                       

-  method_args_dict: Optional[Dict], {} - Arguments required for main
      method of the main class. To be passed in dictionary format and
      very customizable.

*Dag format*
''''''''''''

| from cai_python_plugin import CaiPythonOperator
| from cai_dag import CaiDAG
| dag = CaiDAG(
| default_args={'owner': 'ocb'},
| schedule_interval=None,
| )
| task = CaiPythonOperator(
| task_id='task_id',
| method_id='method_id',
| code_artifact=code_artifact,
| method_args_dict={},
| description='Description',
| dag=dag

)

*Example*
'''''''''

from cai_python_plugin import CaiPythonOperator

from cai_dag import CaiDAG

/# Example dag containing DSCW python operator. This uses a listed code

# artifact, input csv to analyze and produce an output csv for given
names.

#/

code_artifact = 'example_egg_path.egg'

input_file_abspath = 'example_folder/example_input_path.csv'

output_file_abspath = 'example_folder/example_output_file_path.csv'

input_folder, input_file = input_file_abspath.rsplit(‘/’,1)

output_folder, output_file = output_file_abspath.rsplit(‘/’,1)

| dag = CaiDAG(
| default_args={'owner': 'ocb'},
| schedule_interval=None,
| )

ExamplePythonAnalysis = CaiPythonOperator(

task_id='example_python_task',

method_id='example_python_task',

code_artifact=code_artifact,

input_base_dir_path=input_folder,

input_filenames_dict={

'input_data_file': input_file,

},

output_base_dir_path=output_folder,

output_filenames_dict={

'output_data_file': output_file,

},

method_args_dict={},

description='Python Analyze given input csv',

dag=dag

)

ExamplePythonAnalysis

**K8PythonOperator**
^^^^^^^^^^^^^^^^^^^^

Use the K8PythonOperator to execute Python Code over a new Kubernetes
Pod.Kubernetes.

.. _basic-parameters-1:

*Basic* *Parameters*
''''''''''''''''''''

-  dag: CaiDAG - Object of the CaiDAG Class

-  task_id: str - Task ID for the task (used in Dag context)

-  method_id: str - Method ID for the specific Task (used in Code
      Artifact codebase context)

-  code_artifact: List[str] - List of Code Artifacts to be used.

-  image: str - The python image to be used

-  name: Optional[str] - name of the pod in which the task will run,
      will be used (plus a random suffix) to generate a pod id (DNS-1123
      subdomain, containing only [a-z0-9.-]).

-  input_base_dir_path: Optional[str], "" - Base directory path for
      input files. This has to be a string

-  input_filenames_dict: Optional[Dict], {} - Relative file paths for
      input files w.r.t input base directory. To be passed in dictionary
      format.

-  output_base_dir_path: Optional[str], "" - Base directory path for
      output files. This has to be a string

-  output_filenames_dict: Optional[Dict], {} - Relative file paths for
      output files w.r.t output base directory. To be passed in
      dictionary format.

.. _advanced-parameters-1:

*Advanced* *Parameters*
                       

-  method_args_dict: Optional[Dict], {} - Arguments required for main
      method of the main class. To be passed in dictionary format and
      very customizable.

-  config_group: Optional[str] - Name of the config_group to use. If not
      given, use default group specified in Cluster config

-  namespace: Optional[str] - the namespace to run within kubernetes. If
      not given, default namespace

-  get_logs: Optional[bool] - get the stdout of the container as logs of
      the tasks.

.. _dag-format-1:

*Dag format*
''''''''''''

| from cai_k8_python_plugin import CaiK8PythonOperator
| from cai_dag import CaiDAG
| dag = CaiDAG(
| default_args={'owner': 'ocb'},
| schedule_interval=None,
| )

| task = CaiK8PythonOperator(
| task_id='task_id',
| method_id='method_id',

code_artifact=code_artifact,

   image='python_image',

   | name='k8_py_name',
   | method_args_dict={},
   | description='Description',
   | dag=dag,

)

*Examples*
''''''''''

from cai_k8_python_plugin import CaiK8PythonOperator

from cai_dag import CaiDAG

/# Example dag containing DSCW K8s python operator.This uses a listed
code

# artifact, input csv to analyze and produce an output csv for given
names.

# This python operation has the ability to use an independent Python
image

# using Kubernetes support.

#/

code_artifact = 'example_egg_path.egg'

input_file_abspath = 'example_folder/example_input_path.csv'

output_file_abspath = 'example_folder/example_output_file_path.csv'

input_folder, input_file = input_file_abspath.rsplit('/',1)

output_folder, output_file = output_file_abspath.rsplit('/',1)

dag = CaiDAG(

default_args={'owner': 'ocb'},

schedule_interval=None,

)

task = CaiK8PythonOperator(

task_id='example_k8s_python_task',

method_id='example_k8s_python_task',

code_artifact=code_artifact,

name='example',

image='python_image',

input_base_dir_path=input_folder,

input_filenames_dict={

'input_data_file': input_file,

},

output_base_dir_path=output_folder,

output_filenames_dict={

'output_data_file': output_file,

},

method_args_dict={},

description='Python K8s Analyze given input csv',

dag=dag,

)

**K8PySparkOperator**
^^^^^^^^^^^^^^^^^^^^^

Use the K8PySparkOperator to execute Pyspark Jobs over the Kubernetes
cluster.

*Prerequisites*
'''''''''''''''

-  Set the spark configuration appropriately. The important fields
      required are:

| [arguments]
| master = <Master of your Kubernetes Cluster>
| py-files = <Upload py-files and egg files for PySpark in Spark
  Dependency and select here>
| deploy-mode = cluster
| [configurations]
| spark.scheduler.mode = FAIR
| spark.kubernetes.container.image = <spark_image_to_be_used>
| spark.kubernetes.namespace = <namespace_for_running_job:
  default=default>

.. _basic-parameters-2:

*Basic* *Parameters*
''''''''''''''''''''

-  dag: CaiDAG - Object of the CaiDAG Class

-  task_id: str - Task ID for the task (used in Dag context)

-  method_id: str - Method ID for the specific Task (used in Code
      Artifact codebase context)

-  code_artifact: List[str] - List of Code Artifacts to be used as
      Pyspark dependencies.

-  name: Optional[str] - name of the pod in which the task will run,
      will be used (plus a random suffix) to generate a pod id (DNS-1123
      subdomain, containing only [a-z0-9.-]).

-  app_name: Optional[str], "" - Name of the Application

-  input_base_dir_path: Optional[str], "" - Base directory path for
      input files. This has to be a string

-  input_filenames_dict: Optional[Dict], {} - Relative file paths for
      input files w.r.t input base directory. To be passed in dictionary
      format.

-  output_base_dir_path: Optional[str], "" - Base directory path for
      output files. This has to be a string

-  output_filenames_dict: Optional[Dict], {} - Relative file paths for
      output files w.r.t output base directory. To be passed in
      dictionary format.

.. _advanced-parameters-2:

*Advanced* *Parameters*
                       

-  method_args_dict: Optional[Dict], {} - Arguments required for main
      method of the main class. To be passed in dictionary format and
      very customizable.

-  config_group: Optional[str] - Name of the config_group to use. If not
      given, use default group specified in Cluster config

-  namespace: Optional[str] - the namespace to run within kubernetes. If
      not given, default namespace

-  get_logs: Optional[bool] - get the stdout of the container as logs of
      the tasks.

.. _dag-format-2:

*Dag format*
''''''''''''

| from cai_k8_pyspark_plugin import CaiK8PySparkOperator
| from cai_dag import CaiDAG
| dag = CaiDAG(
| default_args={'owner': 'ocb'},
| schedule_interval=None,
| )
| task = CaiK8PySparkOperator(
| task_id='task_id',
| method_id='method_id',

code_artifact=code_artifact,

   name='k8_py_name',

   | app_name='k8_py_app_name',
   | method_args_dict={},
   | description='Description',
   | dag=dag,

)

*Example Dag*
'''''''''''''

from cai_k8_pyspark_plugin import CaiK8PySparkOperator

from cai_dag import CaiDAG

/# Example dag containing DSCW K8s Py-spark operator.This uses a listed

# code artifact, input csv to analyze and produce an output csv for
given

# names. This spark operation can handle both spark and python

# functionalities bundled inside code artifacts (ie. egg files)

#/

code_artifact = 'example_egg_path.egg'

input_file_abspath = 'example_folder/example_input_path.csv'

output_file_abspath = 'example_folder/example_output_file_path.csv'

input_folder, input_file = input_file_abspath.rsplit('/',1)

output_folder, output_file = output_file_abspath.rsplit('/',1)

dag = CaiDAG(

default_args={'owner': 'ocb'},

schedule_interval=None,

)

task = CaiK8PySparkOperator(

task_id='example_k8s_pyspark_task',

method_id='example_k8s_pyspark_task',

code_artifact=code_artifact,

name='example',

input_base_dir_path=input_folder,

input_filenames_dict={

'input_data_file': input_file,

},

output_base_dir_path=output_folder,

output_filenames_dict={

'output_data_file': output_file,

},

method_args_dict={},

description='K8s Pyspark Analyze given input csv',

dag=dag,

)

**BashOperator**
^^^^^^^^^^^^^^^^

Use the BashOperator to execute commands in a Bash shell.

*Parameters*
''''''''''''

-  bash_command: str - The command, set of commands or reference to a
      bash script (must be ‘.sh’) to be executed. (templated)

-  env: Optional[Dict], None - If env is not None, it must be a dict
      that defines the environment variables for the new process; these
      are used instead of inheriting the current process environment,
      which is the default behavior. (templated)

-  output_encoding: Optional[str] - Output encoding of bash command

-  cwd: Optional[str], None - Working directory to execute the command
      in. If None (default), the command is run in a temporary
      directory.

.. _example-1:

*Example*
'''''''''

| from cai_bash_plugin import CaiBashOperator
| from cai_dag import CaiDAG
| dag = CaiDAG(
| default_args={'owner': 'owner'},
| schedule_interval=None,
| )
| run_this = CaiBashOperator(
| task_id='task_id',
| bash_command='bash_command',
| dag=dag,
| )

**LoopableBatchOperator**
^^^^^^^^^^^^^^^^^^^^^^^^^

LoopableBatchOperator allows you to run a target dag in a loop by
passing input from a csv file in batches. You can also provide an
offset, filter_by a column to send rows which match a specific value.

.. _parameters-1:

*Parameters*
''''''''''''

-  dag: CaiDAG - Object of the CaiDAG Class

-  batch_offset: Optional[int]: Default 0

-  batch_size: Optional[int]: Size of the batch. Defaults to 10.

-  filter_by: Optional[str]: Column name to filter_by. Defaults to None,
      which means all rows will be passed.

-  filter_values: Optional[List[str]]: Values in a list with which the
      filter_by column must match against for a row to be passed to
      target dag.

-  run_dag_id: str: Dag id of the target dag.

-  metadata_file: Optional[str]: File which contains the csv rows which
      should be passed. Any valid string path is acceptable. The string
      could be a URL. Valid URL schemes include http, ftp, s3, gs, and
      file. For file URLs, a host is expected. A local file could be:
      file://localhost/path/to/table.csv.

.. _example-2:

*Example*
'''''''''

| from cai_loopable_batch_plugin import CaiLoopableBatchOperator
| from cai_dag import CaiDAG
| dag_id = '<new_dag_filename>'
| input_meta_location = '<path_to_csv>'
| dag = CaiDAG(
| default_args={'owner': 'DSCW's},
| schedule_interval=None,
| )
| task1 = CaiLoopableBatchOperator(
| dag=dag,
| run_dag_id=dag_id,
| task_id='task_id',
| batch_size=5,
| batch_offset=0,
| metadata_file=input_meta_location
| )

This dag triggers a dag with the specified run_dag_id (filename of the
new dag).

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

      
