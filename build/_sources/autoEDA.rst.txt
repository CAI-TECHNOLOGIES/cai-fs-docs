.. _section-5:

**Auto EDA (Exploratory Data Analysis)** 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Exploratory Data Analysis (EDA) is an approach to analyzing the data
using visual techniques. It is used to discover trends, and patterns, or
to check assumptions with the help of statistical summaries and
graphical representations.

.. _overview-2:

**Overview**
''''''''''''

Auto EDA as a complete application is written with Scala, Python for the
backend, and Apache Echarts for the front end. It consists of 2 major
functionalities

-  Generate EDA analysis on a single data file/source

-  Generate Cross-File EDA analysis across two data files/sources

The application has two major pages :

-  EDA sources (Menu ⇒ Developer ⇒ Exploratory Data Analysis)

-  Pipelines - Run and Status (Menu ⇒ Pipelines)

**How To Use?** 
'''''''''''''''

Assuming the Spark Cluster configuration setup for the EDA application
has been confirmed, the general steps a user, starting at the EDA
sources page, can follow are:

STEP 1: The user needs to click the button **Upload Data** to process,
validate and then accept an approved S3A Data lake source. This source
then gets listed in a searchable Sources table below the button.

Conditions for validating the Data source’s connection URL are :

-  It should start with “s3a://”

-  It should contain AlphaNumeric ( including special characters such as
      ! - \_ . \* ' ( ) ) characters

-  File extensions can be csv, tsv, parquet, json

.. image:: vertopal_09389ccfa10c4c9d9f37eba7fe242877/media/image34.gif
   :width: 5.69271in
   :height: 2.76425in

STEP 2 (For the single data source EDA analysis) : The user clicks on
one dataset in the Sources table, causing the **Generate
Visualizations** button to be active. Clicking the button, the User is
shown the screen for customization of the Analysis based on

-  **Statistical Visualizations**: choosing charts/plots across
      different sections (Preliminary, Univariate, Bivariate, and
      Multivariate) for statistical analysis-based visualizations

-  **Textual Visualization**: choosing charts across different NLP
      concepts for visualizations of textual data

-  **Null Method**: method to tackle the Null cells in the original
      Dataset (Skip Cells or Interpolate with Mean and Mode).

When the customization form is submitted, a Pipeline with an appropriate
flash message is triggered in DSCW-Workbench. It later produces a
composite HTML in the **Processed Outputs** view on the EDA sources
page. The composite HTML (consisting of the timestamp of the trigger)
has a view and download action available.

.. image:: vertopal_09389ccfa10c4c9d9f37eba7fe242877/media/image27.gif
   :width: 5.71045in
   :height: 3.19271in

STEP 3 (For the cross data sources EDA analysis) : In contrast, when the
User clicks on two datasets in the Sources table, the button **Generate
Cross-File Visualizations** is active. Clicking the button, a Python
Pipeline, with an appropriate flash message, is triggered in
DSCW-Workbench. The composite HTML output is later visible in the
**Processed Outputs** view on the EDA sources page. Similarly, this
output also has a view and download action available.

.. image:: vertopal_09389ccfa10c4c9d9f37eba7fe242877/media/image35.gif
   :width: 6.07892in
   :height: 2.77604in

If Pipeline run breaks (look out for error message on Pipeline feature
page), logs in Audit log tag comes in handy to debug.