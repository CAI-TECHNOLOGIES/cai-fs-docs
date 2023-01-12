**Datasets**
^^^^^^^^^^^^

The platform supports datasets which are meant to help users do version
control, share and manage different datasets. It integrates seamlessly
in the existing ecosystem.

**How to use?**

Datasets tab can be found under the Developer tab. There are multiple
functionalities that can be performed for a dataset like creating,
adding files, downloading, archiving, deleting, publishing etc. Users
have to write code in Notebooks for each of the functionalities listed
above. To make it easier for the users, we have provided code snippets
in Notebooks under Code Snippet Explorer -> Datasets. Snippets can be
easily dragged-and-dropped for usage. Let us see examples of how few
functionalities can be implemented :

1) Creating a Dataset :

   a. From scratch :

..

   .. image:: vertopal_09389ccfa10c4c9d9f37eba7fe242877/media/image62.png
      :width: 4.24479in
      :height: 0.93739in

   .. image:: vertopal_09389ccfa10c4c9d9f37eba7fe242877/media/image44.png
      :width: 5.66827in
      :height: 2.04688in

b. By using another dataset as a base: Specify the parent datasets under
      **parent_datasets** :

..

   .. image:: vertopal_09389ccfa10c4c9d9f37eba7fe242877/media/image56.png
      :width: 6.40104in
      :height: 1.03212in

   .. image:: vertopal_09389ccfa10c4c9d9f37eba7fe242877/media/image52.png
      :width: 5.76634in
      :height: 1.75868in

c. Combining multiple datasets :

..

   .. image:: vertopal_09389ccfa10c4c9d9f37eba7fe242877/media/image6.png
      :width: 6.20313in
      :height: 0.307in

2) Add Files : Files can be added to a dataset in following ways :

   a. By uploading local files: path refers to the relative path of the
         files/folder wildcard can be used to select specific file, ex.
         wildcard="*.png" to select all .png files dataset_path is the
         path within the dataset where we want the files to be uploaded.

..

   .. image:: vertopal_09389ccfa10c4c9d9f37eba7fe242877/media/image58.png
      :width: 5.75521in
      :height: 3.43118in

b. By uploading S3 files: source_url for S3 files is in the format:
      s3://bucket-name/file-path

..

   .. image:: vertopal_09389ccfa10c4c9d9f37eba7fe242877/media/image77.png
      :width: 5.99479in
      :height: 0.45794in

c. Uploading S3 files from the non-default S3 account: source_url for S3
      files is in the format: s3://bucket-name/file-pathaws_access_key,
      aws_secret_key, & region are the AWS credentials required to
      access the S3 files of the account.

..

   .. image:: vertopal_09389ccfa10c4c9d9f37eba7fe242877/media/image69.png
      :width: 3.38021in
      :height: 1.4272in