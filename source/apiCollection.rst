**API Collections (Auto API Builder)**
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Auto API builder is a tool meant to allow normal users/developers to
easily generate APIs for any of their use cases. The tool allows people
to use a GUI to create APIs which they can auto deploy, or download and
deploy on their own. It comes with proper docker support and planned k8s
support.

-  Easily create a collection of APIs and their code in different
      supported languages. Currently supported python-flask. Use a GUI
      tool to create APIs instead of directly writing the API
      specifications.

-  Allows the user to add their own custom code into the API server, as
      a module directly uploaded, and as direct code through the text
      editor in the web UI.

-  Create a docker image for the generated API server, ready to be
      deployed. Helm chart support also in progress.

.. _overview-3:

**Overview**
''''''''''''

Firstly, the GUI allows the end user to create an OpenAPI specification
file, which is the open standard for defining APIs. Then the
specification is sent to the backend which generates the API code stub,
where the actual logic goes. Then, the user can use the Web UI to edit
the specific code for an API on the browser. The UI only shows the
specific parts of the code for the API which needs to be changed. It
uses an AST parser to pick the specific part of the code on the backend
and allows it to be edited through the UI. After that, the user can add
their own requirements for their custom code, and can upload a wheel
file(python) to use their code as an uploaded module. After adding it
all, they can create a docker image for the generated server code, or
download their generated code.

.. _how-to-use-1:

**How To Use?** 
'''''''''''''''

-  The default screen opens to the editor page with a pre-existing
      example for an API collection.

-  To get the specification, one can use the import/export button (on
      the right side in the header) to download this example as either a
      json or a yaml file. To reset the page, use the delete all button
      to get rid of all the APIs. Use the save button to save after
      making any changes.

-  To start making APIs, go to the **Details** tab first. It looks as
      shown in the figure below :

..

   .. image:: vertopal_09389ccfa10c4c9d9f37eba7fe242877/media/image81.png
      :width: 4.30729in
      :height: 2.24633in

-  Add the details for the API to the appropriate fields.

-  The main field is the Server name field. Make sure to use a name
      which has not been used. To check for whether a name is in use or
      not, fill the name in the box and press enter. Already existing
      server names will turn red, while non-existing server names will
      turn black. A project screen will be added later to allow the user
      to select from their APIs.

-  After filling the details, one needs to go to the **API Editor** tab
      to make their APIs. On that page, click on the **New API path** to
      create a new API path. Next, a new API path will be created. Click
      on the newPath API to open up the GUI editor for it. It will show
      the path as /newPath. Rename the API to the desirable name.

-  Since any API can have a few HTTP methods, we need to click on the
      Add Operation button to add any method to the API. For the guide,
      we will add a POST and GET method.

-  Click once to add a GET method. To add more methods, we need to click
      on the + icon with the GET operation. Then to edit the GET method,
      we click on the toggle button next to operation, or alternatively,
      we can click on the method type (GET). This opens up the editor
      for GET which looks as follows :

..

   .. image:: vertopal_09389ccfa10c4c9d9f37eba7fe242877/media/image21.png
      :width: 5.90625in
      :height: 1.34103in

-  Once it is open, the first thing we necessarily need to do is to add
      a name to the OperationId box.

-  The next Description tab allows us to add information about the
      specific method, which is used in the generated UI interface for
      the APIs.

-  Then, one can add url parameters to our API. The i icon on the right
      redirects the specification in case someone wants to read that up
      in more detail.

..

   .. image:: vertopal_09389ccfa10c4c9d9f37eba7fe242877/media/image31.png
      :width: 5.9693in
      :height: 1.22396in

   .. image:: vertopal_09389ccfa10c4c9d9f37eba7fe242877/media/image73.png
      :width: 5.92919in
      :height: 1.94271in

-  One can add more parameters by using the + icon. The location allows
      us to choose where the parameter will go in the API.

-  The next tab is the request body tab, which is ignored for GET and
      DELETE operations.

-  Since a POST request can have many types of request body, the edit
      inline schema tool allows us to add the type of body the POST
      request accepts. Furthermore, the Media-Type allows us to choose
      mimetypes for the request body. Like for instance application/json
      for json body for the POST. To add a schema for the json, one can
      use the edit inline schema icon (in progress).

-  This allows us to define the schema for this specific request.

..

   **Note :** In case a schema is useful in many places, one can go to
   the advanced tab to define some schemas globally and then use them
   for any request via the re-use shared schema button (recycle icon).

-  The responses tab is similar to the request body tab, except it is
      used to define all the responses for an API(status codes, json
      schema).

-  There is the code tab next, but it comes later after we have a
      generated codebase. So, for now we can save the API we have made
      with the save button and go to the **API generate** tab to
      actually generate the code.

..

   .. image:: vertopal_09389ccfa10c4c9d9f37eba7fe242877/media/image4.png
      :width: 5.42684in
      :height: 2.30729in

-  Here, we use the same server name as defined in the details tab
      previously, and generate the code for the API. If the code was
      already previously generated, use the Update button instead of the
      generate button.

-  Now, we can go to the Code tab in API Editor and add our custom code.
      This gets saved in the backend when we click the update Code
      button.

..

   .. image:: vertopal_09389ccfa10c4c9d9f37eba7fe242877/media/image13.png
      :width: 5.88032in
      :height: 3.14063in

-  In addition to the update code, we can also upload user
      requirements.txt or upload the wheel file in our API generate tab.
      Deployment and generation of Docker images will be added soon.
