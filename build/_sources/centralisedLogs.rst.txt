**Centralised Logs**
^^^^^^^^^^^^^^^^^^^^

We have built a log-data visualization tool meant to allow normal
users/developers to easily understand logs generated throughout the
platform. The tool allows people to use a GUI to view the logs for any
application in its “discover” section, along with custom dashboards in
the “dashboard” section. Any user can also create new dashboards as per
his/her needs from their application logs.

These logs can be viewed in **Monitor -> Centralised Logs**. We parse
logs using regex patterns and create new fields which can be easily
queried. Each application’s logs may be a combination of such regex
patterns.

Terms used in DSCW-Logging :

1. **Log Formats** : Logs of any application have log-lines of different
      formats. Each of these formats can be read to populate new log
      fields. We can alternate between these formats in the UI by adding
      a filter with the condition “<log_field_name> exists”.

2. **Log Fields** : Each log-line has some metadata associated with it,
      which is stored in the form of key-value pairs. These are called
      fields.

..

   .. image:: vertopal_09389ccfa10c4c9d9f37eba7fe242877/media/image87.png
      :width: 4.58333in
      :height: 2.86566in

   There are some default fields which are associated with all logs,
   irrespective of their source. Some of these fields are App : Refers
   to the namespace of the application, Message : the log message,
   Timestamp, Loglevel : info/debug/warning/error/etc, Tags : a list of
   tags which can be added conditionally in fluent-bit

To find the logs of any container, the simplest way is to use filters in
the following order :

-  **Kubernetes.namespace_name :** the namespace in which the
      application is running

-  **Kubernetes.pod_name :** name of the pod

-  **Kubernetes.container_name** : name of the container

To know more information about application specific log fields, refer to
`Application specific log fields. <admin.html#application-specific-log-fields>`__

   3. **Index and Index Patterns :** An index in elasticsearch is
   basically a database. Kibana decides which indices to read depending
   on the index pattern selected. Logs are shown from all the indices
   which match the index pattern.

   4. **Viewing Logs :** Elasticsearch contains all the logs of the
   platform in different indices. To follow the steps involved in
   viewing the logs, refer to `Steps for Viewing
   Logs <admin.html#steps-for-viewing-logs>`__.
