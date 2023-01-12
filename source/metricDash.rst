**Metrics Dashboard**
---------------------

We have built an analytics and interactive visualization tool meant to
allow normal users/developers to monitor stacks, often used in
combination with time series databases. The GUI for metrics are scraped
by istio add-ons. We have multiple dashboards for all user needs, and an
option to create new customized complex dashboards according to user
specifications as well.

All these are visible on the metrics dashboard in **Monitor -> Metrics
Dashboard**. We have added multiple dashboards inside this tool to
maximize the information we can understand from the captured metrics.

**Dashboards**
''''''''''''''''

1. **Kubernetes Cluster Monitoring Dashboard :** View CPU, memory, and
      filesystem usage for any kubernetes nodes and namespaces, along
      with global network i/o metrics.

..

   .. image:: vertopal_09389ccfa10c4c9d9f37eba7fe242877/media/image79.png
      :width: 4.52728in
      :height: 2.58854in

2. **Istio Mesh Dashboard :** View istio component counts, request
      success rate and request sizes in bytes for workloads and services
      across all namespaces.

..

   .. image:: vertopal_09389ccfa10c4c9d9f37eba7fe242877/media/image66.png
      :width: 4.71875in
      :height: 2.70377in

3. **Istio Workload Dashboard :** Select a workload and view its metrics
      for inbound workloads and outbound services, along with some
      general metrics such as incoming success rate and TCP client
      traffic.

..

   .. image:: vertopal_09389ccfa10c4c9d9f37eba7fe242877/media/image39.png
      :width: 4.84896in
      :height: 2.77083in

   .. image:: vertopal_09389ccfa10c4c9d9f37eba7fe242877/media/image55.png
      :width: 4.8125in
      :height: 2.72676in

4. **Kubernetes Persistent Volumes :** View the storage metrics for your
      Kubernetes Persistent Volume Claims.

..

   .. image:: vertopal_09389ccfa10c4c9d9f37eba7fe242877/media/image67.png
      :width: 4.6319in
      :height: 2.67188in

5. **DSCW Dashboard :** View CPU and memory usage grouped by namespace,
      along with individual metrics for pods.

..

   .. image:: vertopal_09389ccfa10c4c9d9f37eba7fe242877/media/image42.png
      :width: 4.65104in
      :height: 2.65641in
