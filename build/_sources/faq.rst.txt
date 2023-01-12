.. _section-15:


FAQs
^^^^^

1. How to install the DSCW Platform? How easy is it? Are there any
      dependencies?

..

   DSCW Platform can be deployed in all three modes - Cloud-native,
   On-prem, or Hybrid. Installation can be done with either of the 2
   deployment configs:

   **On a Kubernetes Cluster** (recommended): It can be deployed with K8
   config files and container images provided in minutes on any
   cloud-managed/self-managed Kubernetes cluster. It comes with a
   unified telemetry and security configuration and can connect with any
   organization's existing Authentication protocols and Telemetry
   (Logging, Metrics, Observability, and Tracing) Infra & Dashboards.

   This is the recommended way as it also provides better
   auto-scalability and reduces server cost & management.

   **On a Docker Infra**: With a set of Docker container images
   provided, it can be deployed manually on the cluster of nodes.
   Post-installation integration with existing infra is supported with
   direct UI, as well as CLI/CI-CD pipelines. Support is there for Dev
   to Production grade deployments.

   Detailed steps of building & deployment from source code are provided
   in the build_steps markdown file.

2. Approximate time is taken for a fresh installation?

..

   The installation should be quick - maybe about a few hours. (30 mins
   post pulling all the images. Pulling /downloading images from the
   docker repository would be additional time, based upon internet
   connection speed.)

   | Next, the configurations are to be set (5 to 30 Hours).
     [Connectivity with organization's existing infra: i. Connection to
     Object storage, data lake (eg. S3, Hadoop, etc.)
   | i. Connection to Compute Cluster (spark, if any),
   | ii. Database connections
   | iii. Memory, executors.
   | iv. Connectivity of Telemetry Data with existing Logging,
     Reporting, Metrics, Auditing, etc. Systems.]

   Testing of example Pipelines (1 to 2 hours). DSCW's example Pipelines
   to test various operators eg. BashOperator, Spark, PySpark, and
   Python Operator. These can be executed to test the connectivity with
   the organization's existing infra.

   Migration of existing codebase (if any), e.g. Spark Pipelines,
   One-time/periodic update of Metadata, etc.

3. List such open-source tools that are integrated with DSCW W/B:

..

   While OSS tools utilized differ, based on what components of the DSCW
   platform have been installed and how it has been set up (docker vs
   Kubernetes), etc. High levels of components are:

   Airflow, Atlas, Boto, Docker Runtime, Druid, ElasticSearchEnvoy,
   FastAPI, Flask, FluentD, Hadoop, Ignite, Istio, JupyterHub,
   JupyterLab, Kafka, Kerberos, Kiali, KeyClock, Kubernetes, LDAP, SAML,
   OpenID Connect, LightGBM, MySql, Nifi, Okta, OpenAPI, OpenTelemetry,
   Postgres, Prometheus, PyTorch, RabbitMQ, Redis, Sentry, Spark,
   Splunk, StatsD, Superset, Tensorflow, Vault, XGBoost, Yarn,
   Zookeeper.

As part of various sub-components, we upgrade every quarter to the
latest version of OSS.

4. What are the components of this Platform?

..

   | Overall, the DSCW Platform has several components, including (but
     not limited to), AI Workbench, EDA, Visualizer, DL Training
     framework, AI Models Repo, etc. AI Workbench further consists of
     modules such as AI Workflow, DSCW Notebook server, DSCW Code
     Editors, DSCW Cluster Config Manager, etc. Each of these components
     works best together, but they are designed to function
     independently when decoupled.
   | An overview has been provided here - `CAI Platform: Overview and
     Installation
     Guide <https://docs.google.com/document/d/11m6nDePWWmrgaQGNrfu0ozn-dGMLATAcU8wRm0uLZmU/edit#heading=h.2uqfpgnrs68f>`__.

5. What is the regular maintenance activity that needs to be performed
      on this tool (by the administrator/developer)?

..

   AI Platform has self-managed capability via its
   OpenTelementry/FluentD/StatsD based open-protocol connectors to
   integrate Logging, Metrics, Observability, and Tracing integration to
   organization standard tools. There is also support for automated
   CI/CD pipelines for deployments of updates.

6. Is any downtime required?

..

   When the platform goes for major upgrades, a restart is required,
   creating downtime. This sometimes extends to the deployment period of
   the tool. This can be better managed with a parallel setup and a
   direct import-switchover feature. AI Workbench does support CLI, as
   well as APIs, as a way of backup & migration.

   Upgrading DSCW Workbench:

A. We have the Pipelines, code artifacts, and configurations all present
      as persistent volumes so it remains as is. So we can just upgrade
      the version of the Workbench using the new images &
      docker-compose.yaml file.

B. The new version may have upgraded plugins for operators, in that
      case, the Pipelines' import statements have to be changed
      accordingly to support the latest plugins.

C. kerberos_host and some other variables might have to be redefined
      again.

D. Backup of some files, variables, and components if needed
      [pre-installation step]

E. Testing using example Pipelines, default provided configurations
      [post-installation step]

..

   The DSCW team shares the README file with guidelines to set up the
   new environment (version).

7. On what platforms, this tool can be installed?

..

   Unix/Linux supported infra running either complete Kubernetes cluster
   or just the docker engine.

8. What are the advantages of using the notebooks available in the tool?

..

   DSCW Notebook server provides a within enterprise environment (viz
   Google Colab, Sagemaker) for data-scientists/data-engineers to have
   an individual notebook workspace, as well as shared team access to
   the common set of files.

9. Does the tool support real-time or streaming data?

..

   DSCW Workbench has support for both real-time, as well as Streaming
   data injection, live data-processing & real-time connectors/API for
   the responses.

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
